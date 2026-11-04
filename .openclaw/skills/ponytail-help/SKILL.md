---
name: ponytail-help
description: "Quick reference for ponytail's modes, skills, and commands. One-shot display."
homepage: https://github.com/DietrichGebert/ponytail
license: MIT
---

# Ponytail Help

Display the sections from Levels through More verbatim when invoked.
One-shot, do not change mode, write flag files, or persist anything.

## Levels

| Level | Trigger | What changes |
|-------|---------|-------------|
| **Lite** | `/ponytail lite` | Build what was asked, name the smaller option in one line. |
| **Full** | `/ponytail` | The smallest complete change, a check where the logic needs one, and a reply that names what was skipped and any risk. Default. |
| **Ultra** | `/ponytail ultra` | Also questions the request and pushes back before building. |

Level sticks until changed or session end.

## Skills

| Skill | Trigger | What it does |
|-------|---------|--------------|
| **ponytail** | `/ponytail` | Lazy mode itself: least new code, clear replies that name skipped work and risks. |
| **ponytail-review** | `/ponytail-review` | Quality review of a diff: bugs, security, load, missing tests, speed, what to cut. Each finding says what goes wrong and how to fix it. |
| **ponytail-audit** | `/ponytail-audit` | The same quality review for the whole repo, ranked. |
| **ponytail-debt** | `/ponytail-debt` | Harvest `shortcut:` comments into a tracked ledger. |
| **ponytail-gain** | `/ponytail-gain` | Measured-impact scoreboard: less code, less cost, more speed. |
| **ponytail-help** | `/ponytail-help` | This card. |

In Codex CLI and the IDE extension, invoke any of the six skills as
`$ponytail:<skill-name>`, for example `$ponytail:ponytail-review`. Claude Code and OpenCode use the
slash-command forms above (OpenCode ships all six as slash commands).

## Deactivate

Say "stop ponytail", "normal mode" or `/ponytail off`. Resume anytime with `/ponytail`.

## Band (Claude Code)

`/ponytail band` hides or shows the band above the prompt.
`/ponytail band on` and `/ponytail band off` set it directly. The level stays.
`/ponytail band import` adds your past Claude Code sessions (cost, agent time, tokens) to the board.

## Configure Default Mode

Default mode = `full`, auto-active every session. Change it:

**Environment variable**:
```bash
export PONYTAIL_DEFAULT_MODE=ultra
```

**Config file** (`~/.config/ponytail/config.json`, Windows: `%APPDATA%\ponytail\config.json`):
```json
{ "defaultMode": "lite" }
```

Set `"off"` to disable auto-activation on session start, activate manually
with `/ponytail` when wanted.

Resolution: env var > config file > `full`.

## Update

Enable auto-update once: open `/plugin`, go to Marketplaces, pick ponytail, Enable auto-update. Claude Code then pulls new versions at startup (run `/reload-plugins` when it prompts).

Manual update: run `/plugin`, open ponytail on the Installed tab and choose
Update now, or run `claude plugin update ponytail@<marketplace>` in your shell
(`claude plugin list` shows that full name). Then run `/reload-plugins` and
recheck the version with `claude plugin list`.
`/plugin marketplace update ponytail` only refreshes the marketplace listing;
if the version did not change, run the plugin update above.

If `/plugin` is not recognized, first check for a non-interactive session
(`claude -p`): `/plugin` does not run there, so use the `claude plugin` shell
commands above. Otherwise check the version with `claude --version` and update
Claude Code with the method you installed it with (`claude update` for the
native install, `npm install -g @anthropic-ai/claude-code@latest` for npm,
`brew upgrade claude-code` for Homebrew), then restart. Other hosts use their own update flow.

## More

Full docs + examples: https://github.com/DietrichGebert/ponytail
