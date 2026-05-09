# AGENTS.md — Before it Breaks

## What This Directory Is

Marketing/demo site for bespoke single-file business tools. Static site, own git repo, deployed separately from NOFNWAY.

## Files

- `index.html` — main marketing site
- `dispatch.html` — Septic Dispatch demo
- `law-demo.html` — legal workflow demo
- `caylie-simple.html`, `caylie-standard.html`, `caylie-complex.html` — planner/demo variants
- `sync.sh` — deploy helper

## Constraints

- Static HTML/CSS/JS only. No framework or build step.
- Demo pages should stay self-contained.
- Keep the site generic and portfolio-oriented rather than tied to private client specifics.

## Deploy

- Use `bash sync.sh` from this directory.

## Agent Sync

- Read `SYNC.md` before starting work.
- Update `SYNC.md` after meaningful changes so Codex and Claude share current state.
