# AI Production Studio

An extremely efficient production studio for creating AI-assisted software products.

## Purpose

This project defines the methodology, tools, workflows, and standards used to plan, design, build, review, test, and maintain software with AI coding agents.

## Related Repositories

Each is listed by its GitHub name and the local folder that holds it, because the two differ.

- `project-template`, in `Projects\project-template`, provides the reusable foundation for new projects.
- `autohotkey-menu`, in `Projects\1AutoHotkey`, automates starting, arranging, restoring, and stopping the production environment, and is the pilot project for studio practices.
- `hearforreal`, in `Projects\2hearforreal`, is the primary software product currently being developed through the studio.
- `Claude-Global-File-History`, in `C:\Users\ariel\Claude-Global-File-History` and without a GitHub remote, holds recoverable version history for the authoritative Claude communication files.

`design/architecture.md` explains how these parts relate and where each agent's communication configuration lives.

## Documentation

Project-wide documentation is located in `design/`.

Journey-specific documentation is located in `design/journeys/`.

A coding agent beginning work on a journey should start with that journey's `handoff-code-map.md`.
