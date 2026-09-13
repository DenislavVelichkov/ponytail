# Ponytail repository guidance

## Source and installation

- This is the `DenislavVelichkov/ponytail` fork. Read the root `.codex-plugin/plugin.json` for the Codex plugin identity and exposed skills.
- The personal Codex catalog lives in `DenislavVelichkov/dv8-codex`. Its marketplace manifest owns the source URL and ref; this repository owns Ponytail's implementation and packaging.
- Make durable changes in this source checkout. Installed caches and marketplace snapshots are consumers. Preserve other platforms' manifests and installation behavior unless the task includes them.
- Check the current branch and worktree changes, then use the smallest relevant existing check for the files changed. Preserve unrelated work.

## Implementation approach

Lazy means efficient, not careless. Understand the request and trace the relevant behavior before choosing the first option that works:

1. Decide whether the requested outcome needs new code.
2. Reuse code that already exists in the repository.
3. Use the standard library.
4. Use a native platform feature.
5. Use an already-installed dependency.
6. Use a one-line implementation when it is sufficient.
7. Otherwise, write the minimum code that works.

For bug fixes, search callers with `rg`, trace the shared behavior, and fix the cause at the appropriate common point. Verify affected callers instead of patching only the reported path.

- Prefer deletion and direct code. Add abstractions only when explicitly requested, and avoid new dependencies and boilerplate when existing tools suffice.
- Choose the shortest correct change after understanding the problem. For equally small approaches, prefer the one that handles edge cases correctly.
- Clarify complex requirements when a simpler interpretation could satisfy the user; an explicit requirement still governs the work.
- Mark deliberate shortcuts with a `ponytail:` comment stating the limitation and upgrade path.
- Preserve input validation at trust boundaries, protection against data loss, security, accessibility, hardware calibration, and explicitly requested behavior.
- For nontrivial logic, provide the smallest runnable check that would fail if the change were wrong. Reuse existing tests or use a small self-check; trivial edits do not need new tests.

These implementation rules also apply when working on Ponytail itself.
