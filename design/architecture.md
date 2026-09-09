# architecture.md

Project: AI Production Studio
Journey: none, this is a main project file

## Purpose

How the parts of the Production Studio relate: which repository owns what, where
each agent's communication configuration lives, and how the global Claude files
are protected.

## Technology Stack

- Documentation, in Markdown. This repository holds no product code.
- Per-project stacks are recorded in each project's own `architecture.md`.

## Project Architecture

### Repositories

Each is listed with its GitHub name and the local folder that holds it, because
the two differ and an agent needs the folder to find anything on disk.

- **ai-production-studio** — GitHub `ai-production-studio`, folder
  `C:\Users\ariel\Projects\ai-production-studio`. The authoritative explanation
  of the studio: purpose, cross-agent working principles, and this map.
- **project-template** — GitHub `project-template`, folder
  `C:\Users\ariel\Projects\project-template`. The reusable structure and files a
  new project starts from. It carries project-level requirements only, and
  points here for anything studio-wide.
- **1AutoHotkey** — GitHub `autohotkey-menu`, folder
  `C:\Users\ariel\Projects\1AutoHotkey`. The pilot project. It automates
  starting, arranging, and stopping the production environment, and it is where
  studio practices are proven before they are generalized.
- **2hearforreal** — GitHub `hearforreal`, folder
  `C:\Users\ariel\Projects\2hearforreal`. The primary software product being
  developed through the studio.
- **Claude-Global-File-History** — no GitHub remote, folder
  `C:\Users\ariel\Claude-Global-File-History`. Recoverable version history for
  the three authoritative Claude files described below.

### Where each agent's communication system lives

Agent-independent principles are in `design-behavior-details.md`. What follows
is where each agent's own system is configured. The systems are named here, not
restated, so there is nothing to fall out of date.

- **ChatGPT.** Discussion mode and engineering mode. Configured inside ChatGPT
  itself, which no repository can hold, so this entry records the concepts and
  their location and nothing more.
- **Claude Code.** Three files, all under `C:\Users\ariel\.claude`:
  - `CLAUDE.md` — how Claude may work with Ariel across every project: the
    `just talk` and `read only` modes, ending `just talk`, and the authorization
    boundaries.
  - `output-styles\decision-first-plain-english.md` — how Claude writes:
    selection, ranking, density, completion reports, hazards, and handoffs.
    Selected by the `outputStyle` field in `settings.json`.
  - `communication-examples.md` — the paired examples and dated corrections
    behind those writing rules. Not loaded into any session; read when a rule
    needs a concrete example or a message has been rejected.

  Working modes are in `CLAUDE.md` rather than in the output style because
  permissions and writing style are different things, and mixing them would make
  the always-repeated writing rules carry authorization text. Claude Code's
  memory holds remembered corrections and working context; it is deliberately
  not an authoritative layer, so a lesson worth keeping graduates into one of the
  three files above.
- **Gemini.** Not established. Nothing has been designed for it, and inventing a
  system before use would produce rules with no evidence behind them.

### Production Studio implementation rules

`design/implementation-rules.md` is the single authority for Studio-wide
implementation rules. Claude Code loads it through
`C:\Users\ariel\.claude\rules\production-studio-implementation-rules.md`, whose
only content is the absolute import of that canonical file. Codex has no
reliable import mechanism, so `C:\Users\ariel\.codex\AGENTS.md` carries one
marked synchronized copy; the existing project-conventions regression compares
that copy with the authority.

Projects do not copy Studio implementation rules. Their always-loaded cards
hold only project-specific constraints or justified project exceptions.

To change a Studio implementation rule, edit the canonical file, synchronize
the marked Codex copy, and run the owning validation. A fresh coding-agent
conversation is the safest way to guarantee newly changed standing instructions
are loaded. Claude Cowork's current external user-scope-import limitation is
outside this Claude Code delivery path.

Codex's 24,576-byte standing-instruction limit is a hard ceiling, not a target.
It covers everything this project requires a fresh Codex conversation to read:
Codex global AGENTS.md, project AGENTS.md, and
how-we-work/work-block-instructions.md. Preserve useful headroom beneath it.

Claude's automatically delivered standing context is measured separately. This
change establishes no Claude ceiling; record the measured post-change load as a
baseline to reduce over time rather than an allowance to fill.

### Why the Claude files are centralized rather than copied per project

The three files are loaded in every project on this machine from one location.
A copy placed in each project diverges from every other copy, and nothing
detects the divergence: each project would then teach the agent something
slightly different, and correcting a rule would mean finding every copy. One
authority and short pointers elsewhere is what keeps 20 to 50 projects
consistent. Every repository that needs to mention the system names the file
instead of summarizing it.

### Claude-Global-File-History

The three authoritative Claude files sit under `C:\Users\ariel\.claude`, outside
every project repository, so nothing versioned them. They are edited by agents
as well as by Ariel, which makes a bad automated edit the realistic threat: a
good version could be overwritten with no way back to it.

`snapshot.js` in that repository copies the three files and commits when any of
them has changed. A `Stop` hook in `C:\Users\ariel\.claude\settings.json` runs it
at the end of every Claude Code turn in every project, so a new version is
committed within one turn of being written, before a later edit can replace it.
When nothing has changed it reads the three files and exits without running git.

What it deliberately is not:

- **Not a machine backup.** The history is on the same drive as the files, so
  losing the machine loses both.
- **Not a configuration source.** Nothing reads configuration from it. It exists
  to restore a file that was damaged, using `git show <commit>:<path>` and a copy
  back into `C:\Users\ariel\.claude`.
- **Not complete.** A version created and overwritten by hand with no Claude Code
  turn in between is never seen by the hook and is not captured. That limit was
  accepted rather than answered with a permanently running watcher.
- **Not extended to memory.** Claude Code's memory folder is not protected,
  because memory is working context rather than authoritative configuration.
