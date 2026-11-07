# The Flourish Plan: DSA Recovery + Full-Stack Dev Growth

_A 90-day system built on top of your existing Omarchy + opencode setup, your neetcode tracker, your task/priority tracker, your typing practice, and your Neovim learning._

---

## 0. Mindset Framing (read this first)

You are not "behind." You already have infrastructure most learners never build: a custom Linux environment, a tracker app, a task/priority system, and you're building muscle memory in Nvim and typing speed _while_ learning to code. That's rare. The goal of this plan is not to cram more in — it's to **connect the tools you already built into one loop** so nothing you learn leaks out again.

Three rules to actually flourish instead of burning out:

1. **Never skip the review queue to do something "more fun."** Reviews are non-negotiable; new problems and new projects are optional if time runs out.
2. **One System, Not Five Systems.** Your task tracker, neetcode tracker, and dev-skill tracker should feed one daily dashboard — not three tabs you have to remember to check.
3. **Ship visible progress weekly.** A commit streak with no visible artifact (a working screen, a passing test suite, a demo gif) is invisible progress. Every week should end with something you can look at.

---

## 1. Upgrade Your Existing Neetcode Tracker Instead of Rebuilding It

You already built a tracker — good. Don't replace it, extend it into a real spaced-repetition engine.

### 1.1 Add fields it's probably missing

|Field|Why|
|---|---|
|`pattern_tag` (Two Pointers, Sliding Window, BFS/DFS, DP-1D, etc.)|Lets you review by _pattern_, not just by problem — this is what actually transfers|
|`confidence_score` (1–5, self-rated after each attempt)|Feeds the interval math instead of a flat schedule|
|`time_to_first_working_solution`|Tracks whether you're getting faster, the real signal of mastery|
|`last_reviewed_at`, `next_review_at`, `interval_days`, `ease_factor`|The actual SM-2 state|
|`failure_reason` (forgot pattern / syntax slip / edge case / misread problem)|Diagnostic — tells you _what kind_ of forgetting is happening|

### 1.2 Replace the fixed Leitner schedule with SM-2-lite

Fixed intervals (1/3/7/21) are a fine start but overreview things you know cold and underreview things you barely passed. Use this instead:

```
if confidence_score >= 4:
    interval_days = round(interval_days * ease_factor)
    ease_factor = min(ease_factor + 0.1, 2.5)
else:
    interval_days = 1
    ease_factor = max(ease_factor - 0.2, 1.3)
```

Start every problem at `interval_days = 1`, `ease_factor = 2.0`. This is a simplified SM-2 — plenty accurate for ~150-300 problems and easy to implement in whatever your tracker is already written in.

### 1.3 The Diagnostic Audit — do this exactly once, this week

Go through every problem you've marked "done" in your tracker:

- Cover the solution. Give yourself 3 minutes to state: **pattern name → time complexity → the one trick that makes it work.**
- Log the result as `confidence_score`. Don't re-code anything yet — this pass is pure classification, and it should take one sitting, not days.
- Anything scoring ≤2 goes into the active queue at `interval_days = 1`.

This single pass replaces "should I restart the roadmap" with actual data. Most people who feel like they "forgot everything" find it's really 20-30% of problems, concentrated in 2-3 patterns.

### 1.4 Pattern-level dashboard, not just problem-level

Add a view to your tracker that aggregates by `pattern_tag` and shows average `confidence_score` per pattern. This is the single highest-leverage feature you can add — it tells you "Sliding Window: 4.2 avg, DP-2D: 1.8 avg" instead of a flat list of 150 rows. Attack your weakest pattern first, always.

---

## 2. Fold In the Task/Priority Tracker (one dashboard, not two)

Since you already have a task/priority tracker, don't run it parallel to the neetcode tracker — make the neetcode tracker **emit tasks into it**.

- Every morning, the neetcode tracker should push "today's due reviews" as high-priority tasks into your existing task tracker automatically (a cron job, a systemd timer, or a shell hook — whatever your task tracker already exposes as an API/CLI).
- Dev-skill practice (TUI/Web/Desktop milestones below) also becomes tasks with priorities, so you have **one place** you check each morning, not three.
- If your task tracker supports tags/projects, use three: `#dsa-review`, `#dsa-new`, `#dev-track`.

This is the actual fix for "I wasn't reviewing on a schedule" — the schedule has to _surface itself_ to you without relying on memory or willpower.

---

## 3. Nvim + Typing Speed: Make Them Part of the Loop, Not a Side Quest

You're already practicing both — stop treating them as separate hobbies and route your daily coding through them.

- **Do every review problem and every project session in Nvim, no exceptions**, even when it's slower than your old editor. Speed comes from reps under real conditions, not from typing drills alone.
- Add a **weekly typing-speed checkpoint using real code**, not prose — type out a previously-solved algorithm from memory (a natural byproduct of your review queue) and time it. This merges two practices into one exercise and gives you a second signal on retention: if you can't type it fluently, you don't know it as well as you think.
- Learn Nvim motions in this order for max coding leverage: `hjkl` + `w/b/e` → `di(` / `ci"` / `dw` text objects → `.` repeat → macros (`qa...q`, `@a`) → LSP bindings (go-to-def, rename, hover) → multiple buffers/splits. Don't front-load plugins — motions first, plugins later.
- Milestone: by the time you finish Tier 1 below (TUI), you should be writing your TUI project's code entirely in Nvim with LSP working for your chosen language. That's the checkpoint that Nvim has "clicked."

---

## 4. Dev Skill Roadmap — Sequenced, With Real Exit Criteria

Same TUI → Web → Desktop order as before, but each tier now has a **concrete exit test** so you don't linger or leave gaps, and each tier's project is a real feature added to your own tools (so you're not building throwaway toy apps).

### Tier 1: TUI (Weeks 1–4)

- **Framework choice:** pick one and commit — don't survey all three.
    - Python + `Textual`: fastest to a working UI, best if you want to move to Web with FastAPI later.
    - Go + `Bubbletea`: cleanest architecture (Elm-style), best if you want strong typing and single-binary distribution.
    - Rust + `Ratatui`: steepest curve, best if you want systems-level control and don't mind slower iteration.
- **Project:** turn your existing neetcode tracker's CLI/script into a real TUI dashboard — due-today list, pattern-confidence view, and a "start review" action that opens the file in Nvim.
- **Exit criteria:** you can navigate the whole dashboard with only the keyboard, state is stored in SQLite (not flat JSON), and the app launches Nvim on your review file directly from a keypress.

### Tier 2: Web (Weeks 5–10)

- **Core path:** HTML/CSS + vanilla JS first (no framework) → pick **one** backend (FastAPI if you used Python for the TUI, Express if JS, or Go's `net/http`) → **one** frontend framework only once vanilla JS feels limiting (React or Svelte — Svelte is a gentler jump from vanilla JS).
- **Project:** rebuild the TUI dashboard as a local web dashboard with charts (pattern-confidence over time, problems-solved streak, review-queue burn-down).
- **Exit criteria:** the web dashboard reads from the _same_ SQLite database the TUI writes to (don't fork your data model), and you've implemented at least one real REST endpoint from scratch (not scaffolded) that you can explain end to end.

### Tier 3: Desktop (Weeks 11–13)

- **Tauri over Electron** for you specifically: smaller binaries, Rust backend option if you want to reuse Ratatui-adjacent skills, and much lighter resource use, which matters more on a personal dev machine than on a corporate laptop.
- **Project:** package the web dashboard as a native app with system tray notifications when a review is due — this is the first project where your app is doing something for you passively, in the background, which is a genuinely different and valuable skill (OS integration, notifications, background processes).
- **Exit criteria:** the app runs from your app launcher (not a terminal command), and it notifies you without you opening it.

---

## 5. Daily & Weekly Execution (unchanged core, tightened)

**Daily (1.5–2 hrs), driven entirely by what your task tracker surfaces each morning:**

|Block|Time|What|
|---|---|---|
|Warmup|30–45 min|Clear due reviews first, always. If none due, one new problem. Log confidence score before you look anything up.|
|Main|45–75 min|Current tier's project, in Nvim, committed to git at the end of the session no matter how small the diff.|

**Weekly:**

- One retro: look at the pattern-confidence dashboard — is anything trending down? That pattern gets extra new-problem reps next week, not just reviews.
- One "ship" moment: a screenshot, a gif, or a demo of something new the tracker/app can do. Post it somewhere you'll see it later (a personal log file counts).

**Every 3 weeks:** re-audit any pattern still below confidence 3. If a whole pattern is consistently weak, spend one full session doing 2–3 _new_ problems in that pattern instead of reviews — reviews alone can't fix a pattern you never understood well in the first place.

---

## 6. 90-Day Milestones

- **Day 7:** Diagnostic audit complete. Tracker upgraded with pattern tags + confidence scores. Task tracker wired to surface daily reviews automatically.
- **Day 30:** TUI tier shipped and in daily use. Review queue is fully driven by SM-2-lite intervals, not manual tracking.
- **Day 70:** Web dashboard live locally, sharing the same database as the TUI. At least one pattern that was weak on Day 7 now averages confidence ≥4.
- **Day 90:** Desktop app packaged with notifications. You can look at the pattern dashboard and see zero patterns below confidence 3.

---

## 7. Today's Checklist

1. Run the diagnostic audit pass on your existing tracker data (Section 1.3) — one sitting, no re-coding.
2. Add `pattern_tag` and `confidence_score` columns to your tracker's data model.
3. Pick your Tier 1 language/framework and initialize the project repo.
4. Wire one thing — even a five-line script — that pushes tomorrow's due reviews into your task tracker automatically.
5. Do your first review-in-Nvim session today, however short.