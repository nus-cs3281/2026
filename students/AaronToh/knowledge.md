### Tool/Technology 1

#### Github Copilot 

- The model used matters. Claude models are much more effective and understanding large code bases and the relationships between different components.
- Context matters. Conversations that drag for too long tend to hallucinate and give inaccurate answers.

### Tool/Technology 2

### Claude Code
I familiarised myself with key claude commands that enable me to manage the context window of a conversation and learnt to plug local LLMs into Claude Code.

#### Context Management
- **Auto-compaction** triggers at ~95% usage, summarising older history automatically
- **`/compact`** — manually compress at ~80–90%; run at logical task breakpoints
- **`/clear`** — full wipe; use when switching to an entirely new task

#### `/resume` and `/rewind`
- **`/resume`** — returns to a previous session via an interactive picker; or use `claude --resume` / `claude -c` from the terminal
- **`/rewind`** — rolls back to any prior turn; choose to revert conversation only, code only, or both. Trigger with `/rewind` or double-tap `Esc`

#### `/model`
Switch models mid-session without restarting. Use `Option+P` / `Alt+P` as a shortcut while composing.
- `/model opus` — most capable, slowest
- `/model sonnet` — balanced default
- `/model haiku` — fast and lightweight

To use **Gemma 4** locally, connect Claude Code to Ollama's Anthropic-compatible API. Gemma 4 (26B MoE, 3.8B active) supports 256K context with zero API cost.

#### `@` File References
- Type `@<filepath>` to inject a file's content directly into context. Claude Code autocompletes the path — faster than describing the file or waiting for Claude to find it.

### Tool/Technology 3

#### Upgrading Encryption Stack

- AES-GCM vs AES-ECB: AES-GCM is an authenticated encryption mode providing both confidentiality and integrity in one primitive, whereas AES-ECB is deterministic and unauthenticated — the same plaintext always produces the same ciphertext, making it vulnerable to pattern analysis.

- Non-deterministic encryption: AES-GCM uses a random IV per encryption call, so the same plaintext produces a different ciphertext each time. This breaks any code that compares ciphertexts directly and requires a decrypt-then-compare approach instead.

- SHA-1 vs SHA-256: SHA-1 is considered cryptographically weak by modern standards. Upgrading to SHA-256 provides stronger collision resistance and a larger 256-bit output.

- Key separation: Using the same key for both AES encryption and HMAC is bad practice as cross-algorithm interactions can theoretically leak key material. Separate independently generated keys should be used for each purpose.

### Tool/Technology 4

#### Schema Management

- **Liquibase change logs** - should be the source of truth. Liquibase logs all changes, its authors, time etc and includes rollbacks. Hibernate `update` is unreviewable and untraceable.
- **Hibernate `validate`** — switch from `update` to `validate` so Hibernate verifies the schema matches entities on startup instead of silently patching it. Makes schema drift visible immediately rather than masking missing migrations.
- **Separation of concerns** — Liquibase owns the schema; Hibernate only verifies it.

#### Migration Workflow

- **`liquibase-hibernate` as `referenceUrl`** — reads the desired schema directly from entity annotations, eliminating the need to spin up a server on a reference branch just to materialise its schema for diffing.
