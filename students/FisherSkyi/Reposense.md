## Use RepoSense

```bash
java -jar RepoSense.jar --repo https://github.com/yannismontreuil/Time_Series_L2D.git
python3 -m http.server 8080
# goto http://localhost:8080/ in browser
```

# Issue 2512

[Plan By Claude](week2.md)

## Key Files:
- frontend/src/components/c-summary-header.vue - The UI component with the filter input field
- frontend/src/views/c-summary.vue - Parent component that manages the filter state
- frontend/src/views/c-authorship.vue:635-647 - Contains the actual filtering logic using minimatch library for glob pattern matching

## Global File Filter Implementation Plan
### Overview: 
Implement a global file filter feature that shows all files across all repositories when "Global" mode is selected, with a search bar for glob pattern filtering and expandable file details.
User Requirements

- Scope: Show ALL files from ALL repositories in authorship.json
- Display: File path, line count, author info, with expandable content
- Layout: Flat list with indentation for folder structure
- Interaction: Clicking a file shows its details (code segments with authorship)

### Current State Analysis
- Data Loading: Authorship data is currently loaded per-repository on-demand via window.api.loadAuthorship(repoName) (api.ts:300-308)
- Each repo's authorship.json is an array of FileResult objects with: path, fileType, lines, authorContributionMap

UI Structure

Summary header (c-summary-header.vue) contains the "Global/Local" filter mode dropdown
Current authorship view (c-authorship.vue) shows files for a single author in a single repository
Two-panel layout exists (c-resizer.vue) with left/right resizable panels

Filtering Patterns

Existing glob filtering uses minimatch library with options: { matchBase: true, dot: true }

- 'update:file-filter-scope'
Purpose: Updates the parent component's fileFilterScope prop value
Pattern: This follows Vue's v-model convention (two-way binding)
What it does: Syncs the selected value ("global" or "local") back to the parent component (c-summary.vue)
- 'get-filtered'
Purpose: Triggers the parent to refresh/refilter the data
Pattern: Side-effect event (action trigger)
What it does: In your PR, when the scope changes to "global", this triggers the watcher in c-summary.vue that loads all authorship data and opens the file browser tab

1. User switches file filter scope to "global" in c-summary-header.vue
1. ***c-summary-header.vue*** emits `update:file-filter-scope`
1. ***c-summary.vue***'s `fileFilterScope` data updates (via v-model)
1. The watcher on `fileFilterScope` triggers (c-summary.vue:218-233)
1. It loads the global files and emits `view-file-browser` with the files data
2. `c-home.vue` listens for `view-file-browser` and reemit
3. `app.vue` receives the event and calls openFileBrowser(files)
4. openFileBrowser calls activateTab('file-browser')
5. c-home.vue receives tabType='file-browser' as a prop
6. The global file browser renders in the right panel