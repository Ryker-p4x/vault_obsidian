# The Nvim Environment Plan

_A complete setup for your Omarchy box, covering the Tier 1–3 dev roadmap (TUI/Go/Rust/Python, Web/TS, Desktop/Tauri) and daily neetcode practice — built in layers so you install what you need when you need it, not all at once._

---

## 0. Philosophy

Two traps to avoid:

- **Plugin hoarding** — installing 40 plugins because a YouTuber's config had them. Every plugin here earns its place for a specific tier or workflow below.
- **Config as procrastination** — tweaking your config instead of doing reviews. Build it in the four layers below, in order, over your first two weeks, then stop touching it except to add what a new tier actually requires.

Since you're still building motions (per the earlier plan — `hjkl`/`w/b/e` → text objects → `.`/macros → LSP → splits), don't install anything in Layer 3+ until those are comfortable. Plugins amplify existing motion skill; they don't substitute for it.

---

## Layer 1: Core Foundation (Day 1)

| Component        | Choice                                                                                                                                       | Why                                                                                                             |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Plugin manager   | `lazy.nvim`                                                                                                                                  | Lazy-loads on filetype/command, fast startup, the current standard                                              |
| Config structure | Lua, split into `init.lua` + `lua/plugins/*.lua` per plugin                                                                                  | Keeps each plugin's config isolated — easy to disable one without breaking others                               |
| Colorscheme      | Anything with good diff/diagnostic contrast (`catppuccin`, `gruvbox`, `tokyonight`)                                                          | You'll stare at LSP diagnostics and git diffs all day — pick for legibility, not looks                          |
| Statusline       | `lualine.nvim`                                                                                                                               | Shows LSP status, git branch, diagnostics count at a glance                                                     |
| `vim.opt` basics | relative numbers, persistent undo, `ignorecase`+`smartcase`, sensible tabs (`expandtab`, `shiftwidth=2` or 4 per language), `updatetime=250` | Relative numbers matter most for you right now — they're what make motion practice (`5j`, `3dw`) actually click |

**Exit test for Layer 1:** you can open Nvim, it loads in under ~100ms, and you're not thinking about the config anymore.

---

## Layer 2: Navigation & Editing (Days 2–4)

This is the layer that makes Nvim actually faster than a normal editor for you day to day — prioritize it before LSP.

| Component            | Choice                                                                     | Why                                                                                                                                                         |
| -------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fuzzy finder         | `telescope.nvim` (+ `fzf-native` extension for speed)                      | File search, live grep across a project, LSP symbol search — one tool, many uses                                                                            |
| File tree            | `neo-tree.nvim` (or skip it — many people are faster with Telescope alone) | Optional; don't install both a tree and rely only on Telescope, pick one                                                                                    |
| Quick file switching | `harpoon2`                                                                 | **This is your neetcode multiplier** — mark 3-4 files (today's review problems) and jump between them with one keystroke instead of fuzzy-finding each time |
| Treesitter           | `nvim-treesitter`                                                          | Real syntax highlighting + powers text objects (`daf` = delete a function, `dab`/`dib` for blocks) — install language parsers for every language you touch  |
| Surround             | `nvim-surround`                                                            | `cs"'`, `ysiw)` etc. — you'll use this constantly editing code                                                                                              |
| Comment toggle       | `Comment.nvim` (`gcc`)                                                     | Trivial but constant                                                                                                                                        |
| Autopairs            | `nvim-autopairs`                                                           | Closes brackets/quotes automatically                                                                                                                        |
| Git signs            | `gitsigns.nvim`                                                            | Inline diff markers + hunk stage/undo without leaving the buffer                                                                                            |
| Which-key            | `which-key.nvim`                                                           | Shows available keybinds as you type a prefix — makes learning your own config's shortcuts painless                                                         |

**Exit test for Layer 2:** you can open any file in a project without touching the mouse or a file tree, in under 2 seconds, using Telescope or Harpoon.

---

## Layer 3: LSP, Formatting, Debugging (Days 5–7)

This is the big one — it's what makes Nvim a real IDE instead of a text editor.

| Component                            | Choice                                               | Why                                                                                                        |
| ------------------------------------ | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| LSP config                           | `nvim-lspconfig`                                     | Standard way to wire language servers into Nvim's built-in LSP client                                      |
| LSP/tool installer                   | `mason.nvim` + `mason-lspconfig.nvim`                | Installs language servers, formatters, linters, and debuggers without touching your system package manager |
| Autocomplete                         | `nvim-cmp` + `cmp-nvim-lsp` + `LuaSnip`              | Completion popup wired to whatever LSP is active                                                           |
| Formatting                           | `conform.nvim`                                       | Format-on-save per filetype (`black`/`ruff` for Python, `gofmt` for Go, `rustfmt`, `prettier` for JS/TS)   |
| Linting (where LSP doesn't cover it) | `nvim-lint`                                          | For things like `ruff` or `eslint_d` as a separate linter pass                                             |
| Diagnostics UI                       | `trouble.nvim`                                       | A clean list view of all errors/warnings in a project — much better than hunting through buffers           |
| Debugging                            | `nvim-dap` + `nvim-dap-ui` + `nvim-dap-virtual-text` | Real breakpoint debugging inside Nvim — genuinely useful once your projects get past trivial size          |

### Language servers to install via Mason, by tier

- **Neetcode (whatever language you solve in):** `pyright` or `ruff` (Python), `gopls` (Go)
- **Tier 1 (TUI):** `pyright`(Textual)/`gopls`(Bubbletea)/`rust_analyzer`(Ratatui) — whichever you pick
- **Tier 2 (Web):** `tsserver`/`ts_ls`, `html`, `cssls`, `tailwindcss` (if used), `eslint`
- **Tier 3 (Desktop/Tauri):** `rust_analyzer` (Tauri backend) + your Tier 2 web servers (frontend)

**Exit test for Layer 3:** go-to-definition, hover docs, rename-symbol, and format-on-save all work in whatever language you're currently using, and you can set a breakpoint and step through code with `nvim-dap`.

---

## Layer 4: Workflow Glue — Neetcode + Your Tools (Days 8–10)

This is the layer that actually connects to the plan from before — making Nvim the single place you do reviews and dev work, not just an editor.

| Component                        | Choice                                                                                                                                                              | Why                                                                                                                                      |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Terminal                         | `toggleterm.nvim`                                                                                                                                                   | Floating/split terminal inside Nvim — run tests, launch OpenCode, run your tracker's CLI without alt-tabbing                             |
| Snippets for problem scaffolding | `LuaSnip` custom snippets, or a small shell/Lua function bound to a keymap                                                                                          | One keystroke should generate a new problem file from a template (function signature + test harness) in your neetcode language of choice |
| Test runner                      | `neotest` (with the adapter for your language) _or_ a `toggleterm` command that just runs `pytest`/`go test`/`cargo test` on the current file                       | You want "run tests on this file" to be one keybind, always                                                                              |
| Project switching                | `telescope-project.nvim` or a simple `cd` keymap per project (neetcode repo, TUI project, web project)                                                              | You'll be jumping between your review queue and your Tier project daily — make it instant                                                |
| Tracker integration              | A custom keymap that shells out to your tracker's CLI (e.g. `:!mytracker start <problem>` or a `toggleterm` job) to mark a review started/done without leaving Nvim | Closes the loop: Nvim opens the file _and_ updates the tracker                                                                           |

### The actual daily keybind you want

Bind one key (e.g. `<leader>rr`) to: pull today's next due review from your tracker → open the file via Harpoon/Telescope → drop you into insert mode at the function body. This is the single highest-value custom binding in this whole setup — it's the difference between "the schedule exists" and "the schedule runs itself when I sit down."

**Exit test for Layer 4:** from a cold Nvim start, you can start today's first review with one keybind, run its tests with one keybind, and mark it reviewed without ever leaving Nvim or touching a mouse.

---

## Layer 5: OpenCode Integration

Since OpenCode is part of your workflow, wire it in deliberately rather than alt-tabbing:

- Run OpenCode inside a `toggleterm` split bound to a dedicated key (e.g. `<leader>oc`) so it's one keystroke away and closes just as fast.
- Per the earlier plan's rule: use this integration heavily for Tier-2/3 plumbing and vibecoded tooling, and hold off on it for the specific code you're trying to learn (Section 4 exit-criteria code, review-queue logic) — write that yourself in a normal split first, then pull up OpenCode alongside to review it.

---

## Layer 6: Per-Project Overrides (ongoing, as needed)

Use `.nvim.lua` (local config, loaded via `exrc`) or per-project `.editorconfig` for things that differ by project:

- Indent width differences between your Go TUI project and your JS/TS web project.
- Project-specific test commands if `neotest` needs per-project setup.
- A Tauri project needs both `rust_analyzer` (src-tauri/) and your web LSPs (src/) active in the same session — configure `nvim-lspconfig` root patterns so both attach correctly when you open the project root.

---

## Suggested Install Order (checklist)

1. **Day 1:** lazy.nvim, colorscheme, lualine, core `vim.opt` settings.
2. **Days 2–4:** Telescope, Harpoon, Treesitter, surround, comment, autopairs, gitsigns, which-key.
3. **Days 5–7:** mason + lspconfig + cmp + conform + nvim-lint + trouble. Install LSPs for whatever you're actively using _right now_ (don't install every language server day one — add Go/Rust/TS servers when you actually reach that tier).
4. **Days 8–10:** toggleterm, neotest (or a simple test keymap), the tracker-integration keymap, the problem-scaffolding snippet.
5. **As needed:** nvim-dap once you hit your first bug worth stepping through; per-project `.nvim.lua` once you have 2+ project types open regularly.

Don't install Layer 3+ language servers for a tier you haven't started — e.g. don't install `tsserver` in Week 1 if you're still on Tier 1 TUI work. Add each layer's language tooling exactly when that tier's plan section says to start it.