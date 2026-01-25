# Global File Filter Implementation Plan

## Overview
Implement a global file filter feature that shows all files across all repositories when "Global" mode is selected, with a search bar for glob pattern filtering and expandable file details.

## User Requirements
- **Scope**: Show ALL files from ALL repositories in authorship.json
- **Display**: File path, line count, author info, with expandable content
- **Layout**: Flat list with indentation for folder structure
- **Interaction**: Clicking a file shows its details (code segments with authorship)

## Current State Analysis

### Data Loading
- Authorship data is currently loaded per-repository on-demand via `window.api.loadAuthorship(repoName)` (api.ts:300-308)
- Each repo's authorship.json is an array of FileResult objects with: path, fileType, lines, authorContributionMap
- Data stored in `window.REPOS[repoName].files`

### UI Structure
- Summary header (c-summary-header.vue) contains the "Global/Local" filter mode dropdown
- Current authorship view (c-authorship.vue) shows files for a single author in a single repository
- Two-panel layout exists (c-resizer.vue) with left/right resizable panels

### Filtering Patterns
- Existing glob filtering uses `minimatch` library with options: `{ matchBase: true, dot: true }`
- File type filtering via checkboxes
- Search bar pattern in c-authorship.vue (lines 47-57)

## Implementation Plan

### 1. Create Global File Browser Component
**New file**: `/Users/sky/CS3281/RepoSense/frontend/src/components/c-global-file-browser.vue`

**Features**:
- Search bar with glob pattern filtering (using minimatch)
- File list display with:
  - Hierarchical indentation for folder structure
  - File path with visual nesting
  - Line count badge
  - Author contribution info
  - Expandable/collapsible file details
- When file is expanded: show code segments with authorship (reuse c-segment-collection.vue)
- Empty state when no files match

**Data structure**:
```typescript
interface GlobalFileEntry {
  repoName: string;
  path: string;
  fileType: string;
  lineCount: number;
  authors: string[];  // gitIds of contributors
  authorContributionMap: Record<string, number>;
  active: boolean;  // expanded state
  segments?: AuthorshipFileSegment[];  // loaded on expand
}
```

### 2. Modify Summary State Management
**File**: `/Users/sky/CS3281/RepoSense/frontend/src/views/c-summary.vue` (or main view component)

**Changes**:
- Track current filter mode state: "global" vs "local"
- When "global" mode is activated:
  - Load authorship.json for ALL repositories (if not already loaded)
  - Aggregate all files into a unified list
  - Store in Vuex store or component state
- Show/hide global file browser based on filter mode

### 3. Update Filter Mode Selection
**File**: `/Users/sky/CS3281/RepoSense/frontend/src/components/c-summary-header.vue`

**Changes**:
- Modify computed property `fileFilterScope` (line 12) to emit mode changes
- Add event handler to notify parent when mode switches to "global"
- Parent component responds by:
  - Showing global file browser in left panel
  - Hiding/collapsing summary charts

### 4. Layout Integration
**Files**: Main view component (c-home.vue or c-summary.vue)

**Changes**:
- Conditionally render global file browser when mode is "global"
- Layout options:
  - **Option A**: Replace left panel summary charts with file browser
  - **Option B**: Use existing two-panel layout (c-resizer.vue)
    - Left panel: global file browser
    - Right panel: selected file details
- Add CSS for panel transitions

### 5. Data Loading Strategy

**File 1**: `/Users/sky/CS3281/RepoSense/frontend/src/types/window.ts`

Add import at the top and update the `Api` interface (line 20-34):
```typescript
// Add at the top with other imports:
import { GlobalFileEntry } from './types';

// Update the Api interface:
interface Api {
  loadJSON: (fname: string) => Promise<unknown>;
  loadSummary: () => Promise<...>;
  loadCommits: (repoName: string, defaultSortOrder: number) => Promise<User[]>;
  loadAuthorship: (repoName: string) => Promise<AuthorshipSchema>;
  loadAllAuthorship: () => Promise<GlobalFileEntry[]>;  // NEW: Add this line
  setContributionOfCommitResultsAndInsertRepoId: (dailyCommits: AuthorDailyContributions[], repoId: string) => void;
}
```

**Note**: You already added `loadAllAuthorship: () => Promise<any[]>;` on line 33, but it should be `Promise<GlobalFileEntry[]>` instead of `Promise<any[]>` once the GlobalFileEntry interface is defined.

**File 2**: `/Users/sky/CS3281/RepoSense/frontend/src/utils/api.ts`

**New method**: `loadAllAuthorship()`
```typescript
async loadAllAuthorship(): Promise<GlobalFileEntry[]> {
  const allFiles: GlobalFileEntry[] = [];

  for (const repoName in window.REPOS) {
    // Load authorship if not already loaded
    if (!window.REPOS[repoName].files) {
      await this.loadAuthorship(repoName);
    }

    // Aggregate files with repo context
    const files = window.REPOS[repoName].files;
    files.forEach(file => {
      allFiles.push({
        repoName,
        path: file.path,
        fileType: file.fileType,
        lineCount: calculateTotalLines(file),
        authors: Object.keys(file.authorContributionMap),
        authorContributionMap: file.authorContributionMap,
        active: false,
      });
    });
  }

  return allFiles;
}
```

**File 3**: `/Users/sky/CS3281/RepoSense/frontend/src/types/types.ts`

Add the `GlobalFileEntry` interface (add after line 80, near other file-related interfaces):
```typescript
export interface GlobalFileEntry {
  repoName: string;
  path: string;
  fileType: string;
  lineCount: number;
  authors: string[];
  authorContributionMap: Record<string, number>;
  isBinary: boolean;
  isIgnored: boolean;
  active: boolean;
  lines?: { lineNumber: number; author: { gitId: string }; content: string; isFullCredit: boolean }[];
  segments?: AuthorshipFileSegment[];
}
```

Then update api.ts to import and use this type:
```typescript
import { GlobalFileEntry } from '../types/types';

// In the loadAllAuthorship method:
async loadAllAuthorship(): Promise<GlobalFileEntry[]> {
  const allFiles: GlobalFileEntry[] = [];  // Explicitly type the array
  // ... rest of implementation
}
```

### 6. File Expansion Logic
**In c-global-file-browser.vue**:

When user clicks to expand a file:
1. Check if segments already loaded (`file.segments`)
2. If not loaded:
   - Fetch from `window.REPOS[file.repoName].files.find(f => f.path === file.path)`
   - Extract line data and build segments (similar to c-authorship.vue logic)
   - Store in file.segments
3. Toggle `file.active` state
4. Render segments using c-segment-collection component

### 7. Search/Filter Implementation
**In c-global-file-browser.vue**:

```typescript
computed: {
  filteredFiles() {
    return this.allFiles.filter(file =>
      minimatch(file.path, this.searchPattern || '*', {
        matchBase: true,
        dot: true
      })
    ).sort((a, b) => a.path.localeCompare(b.path));
  }
}
```

### 8. Hierarchical Display
**Rendering approach**:
- Calculate indentation level based on path depth (number of `/` separators)
- Add CSS padding-left based on depth
- Group files by directory prefix for visual hierarchy
- Example:
  ```
  src/
    components/
      Button.vue
      Input.vue
    utils/
      api.ts
  ```

## Critical Files to Modify

1. **types/types.ts** - Define `GlobalFileEntry` interface
2. **types/window.ts** - Add `GlobalFileEntry` import and update `loadAllAuthorship()` return type from `any[]` to `GlobalFileEntry[]`
3. **utils/api.ts** - Add `GlobalFileEntry` import and `loadAllAuthorship()` implementation
4. **c-summary-header.vue** - Add mode change emission (line 12-13)
5. **c-summary.vue** or **c-home.vue** - Layout switching logic
6. **New: c-global-file-browser.vue** - Main implementation component
7. **store.ts** (if needed) - Global file state management

## Optional Enhancements

- Add loading spinner during authorship data loading
- Persist search pattern in URL hash
- Add file type filter checkboxes (similar to c-authorship.vue)
- Sort options (by path, line count, file type)
- Pagination or virtual scrolling for large file lists

## Verification Steps

1. Start dev server: `npm run serve`
2. Navigate to summary view
3. Select "Global" from filter mode dropdown
4. Verify:
   - Left panel shows global file browser
   - Search bar accepts glob patterns (e.g., `*.vue`, `src/**/*.ts`)
   - Files are displayed with correct indentation
   - File paths, line counts, and author info are shown
5. Click a file to expand
6. Verify:
   - File content/segments load
   - Code is displayed with authorship coloring
   - Can collapse the file again
7. Test edge cases:
   - Empty search results
   - Binary files
   - Files with no authorship data
8. Switch back to "Local" mode
9. Verify original summary view is restored

## Questions/Decisions

- Should binary files be included in the global view?
- Should the search be case-sensitive?
- Maximum number of files to display before pagination?
- Should file tree be collapsible by folder?

---

## Implementation Progress & Change Justification

### Changes Made (Before Interruption)

#### 1. Added `GlobalFileEntry` Interface (types/types.ts:85-97)

**What was added:**
```typescript
export interface GlobalFileEntry {
  repoName: string;           // NEW: Track which repo the file belongs to
  path: string;               // File path within the repo
  fileType: string;           // File extension/type
  lineCount: number;          // Total lines in file
  authors: string[];          // NEW: Array of author gitIds
  authorContributionMap: Record<string, number>;  // Author -> line count mapping
  isBinary: boolean;          // Whether file is binary
  isIgnored: boolean;         // Whether file is ignored
  active: boolean;            // NEW: Expansion state for UI
  lines?: { lineNumber: number; author: { gitId: string }; content: string; isFullCredit: boolean }[];
  segments?: AuthorshipFileSegment[];  // NEW: Loaded on-demand when expanded
}
```

**Justification:**
- **Problem**: The existing `AuthorshipFile` interface is designed for single-repository views and lacks repo context
- **Solution**: Create a new interface that extends the concept with cross-repository awareness
- **Key differences from AuthorshipFile**:
  - `repoName`: Essential for distinguishing files from different repos with same paths
  - `authors[]`: Pre-computed list of contributors for quick display without processing authorContributionMap
  - `active`: UI state management for expandable file list
  - `segments`: Lazy-loaded authorship data to avoid loading all file contents upfront
  - `lines`: Optional detailed line data that can be loaded on-demand
- **Why not reuse AuthorshipFile?**: Mixing repository metadata into per-repo files would break existing single-repo views

#### 2. Created Global File Browser Component (c-global-file-browser.vue)

**What was added:**
A complete Vue component (~160 lines) with:

**Template Structure:**
```pug
#global-file-browser
  .header
    h3 Global File Browser
    .search-container
      input.search-input      // Glob pattern search
      .file-count            // Show filtered count

  .file-list
    .file-item              // Expandable file entries
      .file-header          // Click to expand
        .caret              // Visual indicator
        .file-path          // With hierarchical indentation
        .file-info          // Badges: repo, lines, binary, authors
      .file-content         // Expanded view
        c-segment-collection  // Reuse existing authorship display

  .empty-state             // No matches feedback
```

**Script Logic:**
```typescript
- data: searchPattern (string)
- computed: filteredFiles()
  // Uses minimatch for glob filtering, sorts alphabetically
- methods:
  - getIndentLevel(path): Calculate visual nesting depth
  - toggleFile(file): Expand/collapse files
  - loadFileSegments(file): Lazy-load authorship segments on expand
```

**Justification:**

**Why a new component?**
- Existing `c-authorship.vue` is tightly coupled to single-author, single-repo views
- Global view has different requirements: multi-repo, all files, different layout
- Clean separation of concerns maintains code clarity

**Key design decisions:**

1. **Lazy Loading Segments** (loadFileSegments method):
   - **Why**: Loading authorship data for ALL files from ALL repos upfront could be 1000s of files
   - **How**: Only load `segments` when user expands a file
   - **Benefit**: Fast initial render, memory efficient

2. **Hierarchical Indentation** (getIndentLevel):
   ```typescript
   getIndentLevel(path: string): number {
     const depth = (path.match(/\//g) || []).length;
     return depth * 16; // 16px per level
   }
   ```
   - **Why**: User requirement was "flat list with indentation for folder structure"
   - **Visual clarity**: Files at `src/utils/api.ts` indent more than `src/api.ts`
   - **Alternative considered**: Full tree with collapsible folders (more complex, not requested)

3. **Glob Pattern Filtering**:
   ```typescript
   filteredFiles() {
     return this.files.filter(file =>
       minimatch(file.path, pattern, { matchBase: true, dot: true })
     )
   }
   ```
   - **Why**: Reuses existing pattern from c-authorship.vue for consistency
   - **matchBase: true**: Allows `*.vue` to match `src/components/foo.vue`
   - **dot: true**: Includes hidden files like `.gitignore`

4. **Reusing c-segment-collection**:
   - **Why**: Don't reinvent authorship visualization
   - **Benefit**: Consistent coloring, formatting, and behavior
   - **Implementation**: Build segments from lines using same algorithm as c-authorship.vue

5. **File Information Badges**:
   - Repo name badge: Distinguish files from different repos
   - Line count: Quick size indicator
   - Binary/Ignored badges: Show special file states
   - Author count: Collaboration indicator

**CSS Styling Decisions:**
- Border highlights on expanded files for clarity
- Hover effects for interactivity feedback
- Monospace font for file paths (standard for code paths)
- Color-coded badges (blue=repo, yellow=binary/ignored, green=authors)

### What Still Needs to Be Done

1. ✅ **c-summary-header.vue** - COMPLETED: Added fileFilterScope prop, emit, and computed property
2. **c-summary.vue** - Integrate the component, handle mode switching, call `loadAllAuthorship()`
3. **Layout integration** - Conditionally show global file browser vs regular summary view
4. **Testing** - Verify end-to-end functionality

### Final Integration Steps for c-summary.vue

**Required changes:**

1. **Import the component** (add to imports section around line 70-73):
   ```typescript
   import cGlobalFileBrowser from '../components/c-global-file-browser.vue';
   ```

2. **Register the component** (add to components section around line 97-102):
   ```typescript
   components: {
     cErrorMessageBox,
     cSummaryCharts,
     cFileTypeCheckboxes,
     cSummaryHeader,
     cGlobalFileBrowser,  // ADD THIS
   },
   ```

3. **Add data properties** (add to data() return around line 127-146):
   ```typescript
   fileFilterScope: 'local' as 'global' | 'local',
   globalFiles: [] as GlobalFileEntry[],
   ```

4. **Add v-model binding** (update c-summary-header around line 3-27):
   Add this line to the c-summary-header props:
   ```pug
   v-model:file-filter-scope="fileFilterScope",
   ```

5. **Add conditional rendering in template** (after c-summary-header, before c-summary-charts around line 28-42):
   ```pug
   c-global-file-browser(
     v-if="fileFilterScope === 'global' && !isWidgetMode",
     :files="globalFiles"
   )

   c-summary-charts(
     v-if="fileFilterScope === 'local'",
     ...existing props...
   )
   ```

6. **Add watcher to load global files** (add to watch section around line 189-220):
   ```typescript
   fileFilterScope: {
     async handler(newValue: 'global' | 'local') {
       if (newValue === 'global' && this.globalFiles.length === 0) {
         this.$store.dispatch('incrementLoadingOverlayCount', 1);
         try {
           this.globalFiles = await window.api.loadAllAuthorship();
         } catch (error) {
           console.error('Failed to load global authorship:', error);
         } finally {
           this.$store.dispatch('incrementLoadingOverlayCount', -1);
         }
       }
     },
     immediate: false,
   },
   ```

7. **Import GlobalFileEntry type** (add to imports around line 75-82):
   ```typescript
   import { GlobalFileEntry } from '../types/types';
   ```

### Type Safety & Quality

**TypeScript Benefits:**
- `GlobalFileEntry` interface provides compile-time safety
- PropType validation ensures correct data passed to component
- Prevents runtime errors from mismatched data structures

**Code Quality:**
- Follows existing patterns (Vue 3 composition API, Pug templates, SCSS)
- Reuses existing utilities (minimatch) and components (c-segment-collection)
- Clear method names and comments
- Handles edge cases (null checks, empty results)

### Why This Approach?

**Alternatives considered:**

1. **Modify existing c-authorship.vue**
   - ❌ Would create complex conditional logic
   - ❌ Couples two different use cases
   - ✅ Our approach: Separate component, clear responsibility

2. **Load all authorship data upfront**
   - ❌ Poor performance with many repos/files
   - ❌ High memory usage
   - ✅ Our approach: Lazy loading on expand

3. **Full tree view with collapsible folders**
   - ❌ Not requested by user
   - ❌ More complex to implement
   - ❌ Doesn't match user's "flat list with indentation" requirement
   - ✅ Our approach: Flat list with visual hierarchy via indentation

### Important Design Insight: Author Information

**User feedback**: Author information may not be important in global file search since we're not targeting a specific author.

**Current implementation includes:**
- Author count badge in file list
- Full authorship segments with color-coding when file is expanded

**Considerations for simplification:**

1. **Remove author-related display in file list:**
   - Remove `.authors` badge showing author count
   - Keep: repo name, file path, line count, file type badges
   - Benefit: Cleaner, more focused UI

2. **File content display options:**
   - **Option A (Current)**: Show full authorship segments with color-coding
     - Pro: Reuses existing component, consistent with authorship view
     - Con: May be visual overkill for file browsing

   - **Option B (Simplified)**: Show plain file content without authorship coloring
     - Pro: Simpler, faster rendering, focuses on file content
     - Con: Loses authorship information entirely

   - **Option C (Hybrid)**: Show plain content by default, with option to "Show Authorship"
     - Pro: Best of both worlds - simple by default, detailed when needed
     - Con: More complex implementation

**Decision**: Hide author badges for initial implementation to focus on core file browsing functionality. Will keep authorship segment loading capability for potential future use.

**Quick refinement to make after basic functionality works:**
- Comment out or remove `.authors` badge from file list template
- Keep segment loading logic intact (no code changes needed)
- Can easily add back later if users request it

### Summary

The changes establish the foundation for the global file filter feature by:
1. **Type system**: Defining proper interfaces for cross-repo file data
2. **UI component**: Creating a complete, reusable file browser with search and expansion
3. **Performance**: Using lazy loading to handle large codebases efficiently
4. **Consistency**: Reusing existing patterns, components, and libraries
5. **Flexibility**: Can easily simplify author display based on user feedback

The implementation follows Vue.js best practices, TypeScript type safety, and the existing codebase patterns for maintainability.

---

## Issues Found

### Critical Syntax Error in api.ts

**Location**: `/Users/sky/CS3281/RepoSense/frontend/src/utils/api.ts:347`

**Error Message**:
```
Expected ")" but found "return"
/Users/sky/CS3281/RepoSense/frontend/src/utils/api.ts:349:4
```

**Root Cause**:
The `loadAllAuthorship()` method has a missing closing parenthesis for the `.forEach()` call on line 326.

**Current Code (Broken)**:
```typescript
// Line 326
repoNames.forEach((repoName) => {
  const files = window.REPOS[repoName].files;
  if (!files) {
    return; // Skip if still undefined (shouldn't happen)
  }

  files.forEach((file) => {
    const totalLines = file.lines ? file.lines.length : 0;
    allFiles.push({
      repoName,
      path: file.path,
      fileType: file.fileType,
      lineCount: totalLines,
      authors: Object.keys(file.authorContributionMap || {}),
      authorContributionMap: file.authorContributionMap || {},
      isBinary: file.isBinary || false,
      isIgnored: file.isIgnored || false,
      active: false,
      lines: file.lines,
    });
  });
}  // ❌ WRONG: Missing closing parenthesis for forEach

return allFiles;  // Line 349 - Parser expects ) before this
```

**Fix Required**:
Line 347 should be `});` instead of just `}` to properly close the `forEach()` call.

**Corrected Code**:
```typescript
repoNames.forEach((repoName) => {
  const files = window.REPOS[repoName].files;
  if (!files) {
    return;
  }

  files.forEach((file) => {
    const totalLines = file.lines ? file.lines.length : 0;
    allFiles.push({
      repoName,
      path: file.path,
      fileType: file.fileType,
      lineCount: totalLines,
      authors: Object.keys(file.authorContributionMap || {}),
      authorContributionMap: file.authorContributionMap || {},
      isBinary: file.isBinary || false,
      isIgnored: file.isIgnored || false,
      active: false,
      lines: file.lines,
    });
  });
});  // ✅ CORRECT: Closes the forEach with );

return allFiles;
```

### Additional Potential Issues (After Syntax Fix)

Once the syntax error is fixed, there may still be ESLint warnings:

1. **c-summary-header.vue:55** - Unused emit declaration
   - The `filterModeChanged` emit might be flagged as defined but never used
   - This could be a false positive if the emit is actually being used by parent

2. **c-summary.vue** - Unused imports
   - `cGlobalFileBrowser` and `GlobalFileEntry` might be flagged as unused
   - Likely a false positive since they're used in the template and type annotations

These are linting warnings and won't prevent the code from running.

---

## ESLint Errors to Fix

### Error 1: types.ts Array Type and Delimiter Issues

**Location**: `/Users/sky/CS3281/RepoSense/frontend/src/types/types.ts:95-101`

**Errors**:
1. Line 95: Array type using `T[]` is forbidden for non-simple types - should use `Array<T>`
2. Lines 96-99: Missing semicolons after each property
3. Line 101: Array type using `Array<T>` is forbidden for simple types - should use `T[]`

**Current Code (Broken)**:
```typescript
lines?: {
  lineNumber: number;
  author: { gitId: string };
  content: string;
  isFullCredit: boolean
}[];
segments?: Array<AuthorshipFileSegment>;
```

**Issues**:
- The `lines` property has a complex object type array `{ ... }[]` which ESLint requires to be `Array<{ ... }>`
- Properties inside the object type are missing semicolons (lines 96-99)
- The `segments` property uses `Array<AuthorshipFileSegment>` but `AuthorshipFileSegment` is a simple type, so ESLint requires `AuthorshipFileSegment[]`

**Fix Required**:
```typescript
lines?: Array<{
  lineNumber: number;
  author: { gitId: string };
  content: string;
  isFullCredit: boolean;
}>;
segments?: AuthorshipFileSegment[];
```

**Explanation**:
- Complex object types in arrays must use `Array<{ ... }>` syntax
- All properties inside interface/type definitions need semicolons as delimiters
- Simple types (like `AuthorshipFileSegment`) should use `T[]` syntax for consistency

### Error 2: c-global-file-browser.vue Array Type and Import Order

**Location**: `/Users/sky/CS3281/RepoSense/frontend/src/components/c-global-file-browser.vue`

**Errors**:
1. Line 49: Import order - `minimatch` should come before local imports
2. Line 70: `GlobalFileEntry[]` should be `Array<GlobalFileEntry>` (return type)
3. Line 107: `AuthorshipFileSegment[]` should use `Array<AuthorshipFileSegment>` (needs verification)

**Current Import Order (Broken)**:
```typescript
import { defineComponent, PropType } from 'vue';
import { GlobalFileEntry, AuthorshipFileSegment } from '../types/types';
import cSegmentCollection from './c-segment-collection.vue';
import { minimatch } from 'minimatch';  // ❌ External import after local imports
```

**Fixed Import Order**:
```typescript
import { defineComponent, PropType } from 'vue';
import { minimatch } from 'minimatch';  // ✅ External imports before local
import { GlobalFileEntry, AuthorshipFileSegment } from '../types/types';
import cSegmentCollection from './c-segment-collection.vue';
```

**Array Type Issues**:
- Return types and parameters should follow the same array type rules as interfaces
- Need to check line 70 and 107 for consistency

### Error 3: c-summary.vue Unused Variables

**Location**: `/Users/sky/CS3281/RepoSense/frontend/src/views/c-summary.vue`

**Errors**:
1. Line 74: `cGlobalFileBrowser` is defined but never used
2. Line 82: `GlobalFileEntry` is defined but never used

**Analysis**:
These are likely **false positives** because:
- `cGlobalFileBrowser` is used in the template (line 35: `c-global-file-browser`)
- `GlobalFileEntry` is used in the data type annotation (line 137: `globalFiles: GlobalFileEntry[]`)

**Potential Fixes**:

**Option A**: Remove explicit return type annotation from `data()` function
```typescript
// Current (with explicit return type)
data(): {
  // ... long type annotation including GlobalFileEntry[]
} {
  return { ... }
}

// Simplified (let TypeScript infer)
data() {
  return {
    globalFiles: [] as GlobalFileEntry[],  // Type assertion here instead
    // ...
  }
}
```

**Option B**: Add ESLint ignore comments
```typescript
// eslint-disable-next-line @typescript-eslint/no-unused-vars
import cGlobalFileBrowser from '../components/c-global-file-browser.vue';
```

**Recommended**: Option A - removes the long return type annotation and uses inline type assertions where needed. This is cleaner and matches modern TypeScript/Vue patterns.
