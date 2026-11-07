2# Neovim + Omarchy Workflow Guide

## Part 1: Keyboard Bindings Reference

Shortcuts are tapped sequentially, not simultaneously — press Spacebar, release, then the next key.

|Binding|Action|What it does|
|---|---|---|
|`Space`|Leader key|Master prefix that arms Neovim to catch the rest of the sequence.|
|`Space o c`|Toggle OpenCode AI|Opens or hides the floating AI panel. Sessions stay alive in the background while hidden.|
|`Space n s`|New Scaffold|Prompts for a problem name and language tag (`py`, `go`, `rs`, `cpp`), creates the file, and injects a test harness.|
|`Space r t`|Run Tests|Runs the test suite for the active file in a floating overlay.|
|`Space t k`|Tracker Hook|Reads the active filename and sends `mytracker start <name>` to the tracking CLI.|
|`Ctrl \`|Toggle Terminal|Opens or hides a bash pane at the bottom of the workspace.|
|`Space e`|Toggle File Tree|Opens or hides the folder explorer on the left edge.|
|`Space p n`|Jump: Neetcode|`cd` to `~/Work/Projects/neetcode/`.|
|`Space p t`|Jump: TUI repo|`cd` to `~/Work/Projects/tui-app/`.|
|`Space p w`|Jump: Web app repo|`cd` to `~/Work/Projects/web-app/`.|
|`ysiw)`|Yank Surround Word|Wraps the word under the cursor in parentheses.|
|`cs")`|Change Surround|Swaps surrounding double quotes for parentheses.|
|`gcc`|Toggle Comment|Comments or uncomments the current line.|

---

## Part 2: Multi-Language Test Runner (`Space r t`)

`Space r t` detects the active file's language and launches the matching harness:

- **Python (`.py`)** — floating pane running `pytest <current_file>`
- **Go (`.go`)** — floating pane running `go test -v <current_file>`
- **Rust (`.rs`)** — runs `cargo test`, handling compilation checks in the background
- **C++ (`.cpp`)** — compiles and runs via `g++ -std=c++17 <current_file> -o temp_test && ./temp_test && rm temp_test`; on a failed `assert()`, it stops and highlights the failing line

---

## Part 3: AI Assistant Framework

The floating AI cockpit (`Space o c`) runs on **OpenCode**, configured with two distinct profiles so the tool doesn't become a crutch: one for mechanical setup work, one for actual problem-solving help.

### Strategy A — Test Assembler (file-writer mode)

**Purpose:** offload manual entry of edge-case test values for array/struct-heavy problems.

**How to use it:** reference the active file with `@` and ask OpenCode to append test cases without touching your logic.

**Example prompt:**

> Generate 4 distinct edge-case test values matching the structural input for this problem. Append them as `assert()` values in my active harness at `@three_sum.cpp` (or `.py`). Do not touch or modify my implementation.

### Strategy B — Socratic Tutor (`/coach`)

**Purpose:** a locked-down tutoring persona that is not allowed to write or reveal solution logic. It only asks questions, names general technique categories, and interrogates your reasoning until you find the gap yourself.

**How to use it:** inside OpenCode, run the `/coach` command. This calls the saved tutor persona directly — no need to type out `@guide` by hand every time.

**Example:**

> `/coach` I'm building an indexing pointer loop inside `@two_sum.py` but my pointers are skipping elements. Don't give me the fix — help me trace through my logic.

**The persona configured behind `/coach`:**

```
You are a Socratic programming coach helping a developer strengthen their
own problem-solving process — not solve the problem for them. Your default
mode is active interrogation: you don't just wait to be asked before
offering a hint, you continuously probe the user's reasoning until it's
either solid or visibly broken.

STRICT CONSTRAINTS:
1. Never output code, code blocks, or pseudocode, in any language, at any point.
2. Never state a full sequence of algorithmic steps, even in plain English.
   Narrating the solution in prose is still giving the solution.
3. If the user asks directly for the answer, the full approach, or says
   something like "just tell me" — do not comply. Acknowledge their
   frustration briefly, then redirect with a question or a smaller
   conceptual nudge instead.
4. Before offering any hint, first ask what they've tried and where it
   broke down. Don't suggest techniques in a vacuum.
5. Hints should stay at the level of: clarifying questions, naming a
   general category of technique ("this smells like a two-pointer
   problem"), or explaining why that category might apply — never the
   specific sequence of steps to implement it.
6. If they're debugging broken code, don't identify the bug for them.
   Ask questions that lead them to notice it themselves (e.g., "what do
   you expect this variable to be at this point, and what is it actually?").
7. When discussing time/space complexity, only analyze the complexity of
   the approach they've proposed — don't introduce complexity comparisons
   for approaches you haven't been asked about.

CONTINUOUS INTERROGATION:
8. After every claim the user makes about their approach, ask them to
   justify it before you move on ("how do you know that?", "what happens
   if...?", "walk me through that with an example").
9. Push for concrete tracing over abstract reasoning — have them trace
   their approach by hand against a specific input.
10. Use counterexamples instead of corrections. Ask what their approach
    would do on a tricky input rather than telling them it fails.
11. Do not let vague or unverified reasoning pass unchallenged.
12. Treat confidence as a starting point for a question, not proof of
    correctness.

GOAL: Success looks like the user reaching "oh, I see the problem" through
their own tracing and reasoning — not through you explaining it.
```

`@guide` remains available as a direct alias if you want to address the persona mid-conversation without invoking the slash command.

---

## Part 4: Configuration Isolation

Dotfiles are kept pristine and firewalled through dedicated environment paths:

- **`vk`** (or plain `nvim`) — loads the vanilla `~/.config/nvim` install, a lightweight Kickstart.nvim baseline.
- **`vlazy`** — loads the full LazyVim setup: Catppuccin Mocha theme and the custom workflow layer, isolated to `~/.config/lazyvim`, `~/.local/share/lazyvim`, and `~/.cache/lazyvim`.

---

## Part 5: Everyday Workflow

1. Launch the environment: `vlazy`
2. Jump to the working directory: `Space p n`
3. Scaffold the problem: `Space n s` (e.g. name `four_sum`, extension `cpp`)
4. Generate test cases: `Space o c` → `Generate test cases matching problem rules inside @four_sum.cpp` → `Space o c` to close
5. Write the solution by hand.
6. If stuck: `Space o c` → `/coach [your question]` → `Space o c` to hide.
7. Run the tests: `Space r t`
8. Log the session: `Space t k`