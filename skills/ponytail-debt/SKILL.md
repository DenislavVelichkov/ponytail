---
name: ponytail-debt
description: "Lists every `shortcut:` comment (and older `ponytail:` ones) as a debt ledger. One-shot report, changes nothing. Use for \"ponytail debt\", \"what did ponytail defer\", \"list the shortcuts\", /ponytail-debt. Not for a full quality audit (use ponytail-audit)."
---

This collects every deliberate `shortcut:` comment (older code may say
`ponytail:`) into one ledger so a deferral can't quietly become permanent.

## Scan

Run the scan from the repository root (`git rev-parse --show-toplevel`), or
from the root the user names when there is no Git. Grep for comment markers,
skipping `.git` and everything `.gitignore` files ignore:

`git grep --no-index --exclude-standard -nE '(#|//|/[*]+|--|;|<!--|%|^[[:blank:]]+[*])[[:blank:]]*(shortcut|ponytail):'`  (add prefixes for other comment or continuation styles in the files scanned, e.g. `REM`, `'`, `{-`)

No `git` on the machine: run the same pattern with `rg -n --hidden --no-require-git -g '!.git' -e '<pattern>'`, which also skips ignored files.

If the user names their own marker word (`/ponytail-debt TODO`), put it in place of
`(shortcut|ponytail)` and keep the comment-prefix guard.

The pattern matches a comment's opening line and indented ` * ` block-comment
continuation lines.

Each hit is one ledger row. Skip hits in prose files (.md, .txt) that are not
comments, such as indented Markdown `*` bullets, and hits that are not a
deferral, like a note about a keyboard shortcut.

## Output

One row per marker, grouped by file:

`<file>:<line>, <what was simplified>. ceiling: <the limit named>. upgrade: <the trigger to revisit>.`

`<what was simplified>` summarises the code line or block the comment
annotates. The convention is `shortcut: <ceiling>, <upgrade path>`, so pull the
ceiling and the trigger straight from the comment. A block comment can continue
on the next lines; read up to its closing `*/`. A hit without that
`<ceiling>, <upgrade>` shape (common with custom markers) goes whole under
`<what was simplified>`, and any hit without that shape or a named upgrade
trigger gets a `no-trigger` tag: those are the ones that silently rot.

Leave owners out unless the user asks for them. Then take each row's owner from
the `author` line of `git blame --porcelain -L<line>,<line> -- <file>`. A file
Git does not track gets `owner: untracked`.

Before reporting, check that each kept hit has exactly one row, each ceiling and
upgrade matches its comment, and both totals match the rows. Correct once; report
any gap left as `Incomplete ledger:`.

End with `<N> markers, <M> with no trigger.` Nothing found: `No shortcut debt. Clean ledger.`
A `git grep` or `rg` exit status of 1 means no matches, which is a clean
ledger. If the scan fails any other way or a path can't be read, report
`Incomplete scan:` with the error instead of a clean ledger.

## Boundaries

Reads and reports only. Save the ledger to a file only when the user requests
it, using their path or `PONYTAIL-DEBT.md`. This one-shot report leaves the
active Ponytail mode unchanged.
