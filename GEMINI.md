# GEMINI.md — Before it Breaks project context

This file provides guidance to Gemini CLI when working in the `beforeitbreaks/` directory.

## What This Is

Marketing and demo site for Gerry's bespoke single-file business tools. Deployed as a separate git repository.

## Files

- `index.html`: Main marketing site.
- `dispatch.html`: Septic Dispatch demo.
- `law-demo.html`: Legal workflow demo.
- `caylie-*.html`: Planner and demo variants.
- `sync.sh`: Deployment helper script.

## Constraints

- **Stack:** Pure static HTML/CSS/JS. No frameworks or build steps.
- **Self-Contained:** Demo pages must be self-contained single-file HTML tools.
- **Generic:** Focus on portfolio value and general utility. Avoid specific private client details in the public-facing demos.

## Deployment

- Run `bash sync.sh` from this directory.

## Agent Sync

- Read `SYNC.md` before starting.
- Update `SYNC.md` after changes.
