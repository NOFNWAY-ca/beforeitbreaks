---
name: scaffold
description: Scaffold a new client tool. Use when starting work on a bespoke single-file HTML tool for a client. Sets up the correct structure and reminds about key constraints.
argument-hint: "[client name and description of what the tool needs to do]"
user-invocable: true
---

# Scaffold a Client Tool

## Constraints (Always)

- Single HTML file. This is the whole product -- the client gets one file.
- No frameworks, no build step, no external dependencies.
- Data stays local. Nothing leaves the browser unless the client explicitly needs it.
- Must work offline.
- Must work when opened directly from the filesystem (no server required).

## Process

1. Confirm the tool name and client before creating any files
2. Create a single `.html` file with an appropriate name
3. All CSS in `<style>`, all JS before `</body>`
4. If the client has branding (colors, logo), ask before assuming
5. localStorage for any data persistence unless told otherwise

## Before Delivering

- Open the file in a browser and test the core workflow manually
- Confirm there are no external resource calls that would break offline
- Check that data export (if any) works correctly

## Delivery

Single HTML file sent directly. No deployment. No repo access needed by client.

## Status Note

After scaffolding, update this project's CLAUDE.md status field.
If this becomes active client work, add client name and contact details there.
