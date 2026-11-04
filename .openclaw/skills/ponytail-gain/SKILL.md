---
name: ponytail-gain
description: "Show ponytail measured impact as a scoreboard: less code, less cost, more speed, from the agentic benchmark averages. One-shot display."
homepage: https://github.com/DenislavVelichkov/ponytail
license: MIT
---

# Ponytail Gain

Never substitute figures from any file in the user's repo. Refreshing the figures is maintainer work in the
plugin repo.

The figures are the published agentic benchmark of Ponytail 5: headless Claude
Code (Opus 5.5, default effort) on 39 tasks (feature tickets in a real FastAPI +
React repo, bug fixes, security and privacy cases, small apps), 5 runs each,
against the same agent without the skill. 18 of the tasks have hidden checks
for correctness and safety. Each figure is the geometric mean of the per-task
medians. They are measured, not computed from the current repo.
The plugin repo publishes them in `benchmarks/results/2026-10-07-agentic.md`
and its README.

## Scoreboard

When invoked, print this block exactly as written, inside a code fence:

```
  ponytail gain           benchmark 2026-10-07 · 39 tasks × 5 runs · Opus 5.5

  no-skill        ████████████████████  100%
  Lines of code   █████████···········   47%   ▼ 53%
  Output tokens   ███████████·········   55%   ▼ 45%
  Cost            ███████████████·····   74%   ▼ 26%
  Time            ████████████········   59%   ▼ 41%
  Hidden checks passed   97%  (no-skill 96%)
  Tasks with a test where logic needed one   98%  (no-skill 68%)

  This repo:  /ponytail-debt  (shortcuts you deferred)
              /ponytail-audit (what's still cuttable)
```

## Honesty boundary

These are benchmark averages, not this repo. Never print a per-repo savings
number ("you saved X lines/tokens here"): the unbuilt version was never
written, so there is no real baseline to subtract from in a live repo. The
only real per-repo figures come from `/ponytail-debt` (a counted ledger), and
this card points there instead of inventing one.

## Boundaries

One-shot display. Edits nothing, writes no flag files, persists nothing, and
leaves the active Ponytail mode unchanged.
