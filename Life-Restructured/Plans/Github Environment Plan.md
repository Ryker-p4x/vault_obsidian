# The GitHub Environment Plan

_How to structure repos, commits, and boards so your daily work (reviews, Tier 1–3 projects) is visible, organized, and eventually portfolio-ready — without turning git hygiene into another thing to procrastinate with._

---

## 0. Philosophy

Git here serves three separate jobs, and conflating them causes most of the mess people run into:

1. **A daily habit log** — proof you showed up, tied to the "commit at the end of every session" rule from the execution plan.
2. **A working history** — so you can actually roll back, branch, and not fear breaking something.
3. **A portfolio** — what a future collaborator, mentor, or (eventually) employer sees when they click your profile.

Job 3 only works if jobs 1 and 2 are done well — a portfolio full of "asdf" commit messages and one giant repo undermines it more than having no portfolio at all. So: solid daily habits first, curation later.

---

## 1. Repo Structure — Separate Repos, Not a Monorepo

Given you have genuinely distinct projects (neetcode tracker, TUI project, web dashboard, desktop app, plus neetcode solutions themselves), keep them as **separate repos**, not folders in one giant repo:

|Repo|Contents|Visibility|
|---|---|---|
|`neetcode-solutions`|Your actual problem solutions, organized by pattern, plus your confidence-score/review data if it's just flat files|Public (unless you're worried about future employers pattern-matching solutions — not a real risk at your stage, but your call)|
|`neetcode-tracker`|The tracker app itself (currently vibecoded, evolving into your Tier 1–3 project)|Public once it's not embarrassing, private until then — no shame in private-while-learning|
|`dev-dotfiles`|Your Nvim config, Omarchy setup, aliases — the environment plan from before, as actual config files|Public — dotfiles repos are genuinely useful to share and to look back at|
|One repo per Tier project as it matures (e.g. `neet-tui`, `neet-web`, `neet-desktop`)|If Tier 2/3 end up being full rewrites rather than iterations on the same codebase, give each its own repo|Public once past scaffold stage|

**Why separate over monorepo:** at your stage, separate repos give you clean READMEs per project (better for portfolio skimming), simpler CI per project, and no risk of one broken tier blocking commits to another.

**If instead each tier is really the _same_ app evolving** (TUI → same logic exposed as Web → same logic packaged as Desktop, which is how the plan is structured), then **one repo (`neet-tracker`) with the tiers as directories or branches** makes more sense than three separate repos — don't force separation if the code is genuinely one evolving project. Use your judgment here based on how much the codebase actually shares.

---

## 2. Branching — Keep It Simple

You don't need GitFlow at this scale. Use:

- `main` — always working, always what a reviewer would see first.
- `feature/<short-name>` branches for anything that takes more than one sitting (a new tier feature, a tracker upgrade like the SM-2 rework) — merge back via PR even solo, so you get the habit of reviewing your own diff before it lands.
- Trivial fixes (typo, one-line bug) can go straight to `main`.

**Exit test:** you should never be scared to experiment on `main` because anything risky lives on a branch until it works.

---

## 3. Commit Habits

- **Conventional Commits** format: `feat: add pattern-confidence dashboard`, `fix: interval calc resets ease_factor wrong`, `docs: update README`, `chore: bump dependencies`. This costs nothing extra and makes your history skimmable later — useful when you forget why you changed something three weeks ago.
- **Commit at the end of every session**, per the daily execution plan, even if the diff is small. A tiny honest commit ("wip: harpoon keymap, not tested yet") beats no commit.
- **Write the message yourself.** This is one of the "learning" tasks from the vibecoding conversation — a commit message forces you to articulate what you did and why, which is a real comprehension check, not just plumbing. Don't let OpenCode generate these.
- **Don't game the contribution graph.** Committing broken code just to keep a green square is worse than an honest gap — the graph is a byproduct of real work, not a target.

---

## 4. README Standard (per repo)

Every repo — even the vibecoded ones — gets a README with:

1. **One-sentence description** of what it does.
2. **Why it exists** (2-3 sentences — "spaced-repetition tracker for neetcode practice, built to fix X problem" reads far better than nothing).
3. **Current status** (actively developed / stable / archived) — honest status beats a stale README.
4. **How to run it** (even if it's just `python main.py`).
5. **What's next** (optional, but shows intent — useful for you too, as a running TODO you'll actually see).

This takes 10 minutes per repo and is the single biggest lever on whether a repo reads as "a real project" versus "a folder that happens to be on GitHub."

---

## 5. GitHub Projects — Wire It to Your Task Tracker, Don't Duplicate It

You already have a task/priority tracker doing the daily-surface job (Section 2 of the earlier plan). Don't run a second, competing task system in GitHub Projects. Instead:

- Use **GitHub Issues** as the backlog for each dev project specifically (Tier 1/2/3 features, tracker upgrades) — things that are code-shaped, not daily-review-shaped.
- Optionally use **one GitHub Project board** per active tier project, with columns `Backlog / In Progress / Done`, fed by those issues — useful for tracking a multi-week feature (like the Tier 2 rebuild) without cluttering your daily task tracker with dev sub-tasks.
- Keep the **daily review queue entirely in your existing tracker/task-tracker loop** — GitHub Issues are for "build this feature," not "review this problem today." Mixing them defeats the "one dashboard" principle from before.

---

## 6. CI — Minimal, Not Enterprise-Grade

A single GitHub Actions workflow per project once it has tests worth running:

```yaml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: <install deps>
      - run: <run tests>
      - run: <run formatter --check / linter>
```

- Add this **once you have real tests**, not before — CI on an empty test suite is theater.
- This also gives you a natural forcing function for the `neotest`/test-runner setup from the Nvim plan: if you're testing locally in Nvim already, wiring the same command into CI is a 10-minute add.

---

## 7. Dotfiles Repo — Version Your Environment Itself

Given how much the Nvim environment plan builds up over 10 days, **version it from day one**:

- `dev-dotfiles` repo containing your `nvim/` config, relevant Omarchy/Hyprland config, shell aliases, and the tracker's shell integration hooks (Section 4 of the Nvim plan).
- Symlink from `~/.config/nvim` etc. into the repo (a simple `install.sh` that symlinks everything is enough — no need for `stow` or anything fancier at this stage).
- This means when you inevitably break your config experimenting, you `git checkout` back to working instead of rebuilding from memory — and it becomes genuinely useful/portfolio-relevant later ("here's my dev environment" is a real thing people share).

---

## 8. Portfolio Layer (do this after 4–6 weeks, not now)

Once Tier 1 is done and Tier 2 is underway, curate rather than expose everything raw:

- **Pin 4–6 repos** on your GitHub profile: dotfiles, the tracker (once it's not embarrassing), your best Tier project, and 1-2 strong neetcode-solutions write-ups.
- **GitHub Pages** for the eventual Tier 2 web dashboard — free static hosting straight from the repo, and a live demo link is worth far more than a README screenshot.
- **Profile README** (a repo named exactly your GitHub username) — a short "currently learning X, building Y" — low effort, high signal, and easy to update as you move through tiers.
- Don't do this curation step early — a portfolio built before you have 4-6 weeks of real work just advertises an empty pipeline. Let Sections 1-7 run first.

---

## 9. Checklist to Set Up This Week

1. Decide monorepo-vs-separate for the tracker specifically (Section 1) — this is the one structural decision worth making deliberately before you build much more on top of it.
2. Create `dev-dotfiles` and move your Nvim config into it today, before it grows further.
3. Add a README to every existing repo, even the messy ones — 10 minutes each.
4. Switch to Conventional Commits starting with your next commit.
5. Create one GitHub Issue for the next real feature on your current tier project, and start using branches for anything beyond a one-line fix.