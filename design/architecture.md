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
  not an authoritative layer, so a lesson worth keeping graduates into its
  authoritative owner, which for Claude's own working and writing rules is one of
  the three files above.
- **Gemini.** Its interaction system is not established. Do not invent one in advance. Record Gemini's interaction model once it has been used seriously enough to know what it needs.

### Production Studio implementation rules

`design/implementation-rules.md` is the single authority for Studio-wide
implementation rules. Claude Code loads it through
`C:\Users\ariel\.claude\rules\production-studio-implementation-rules.md`, whose
only content is the absolute import of that canonical file. Codex has no
reliable import mechanism, so `C:\Users\ariel\.codex\AGENTS.md` carries one
marked synchronized copy; the existing project-conventions regression compares
that copy with the authority.

`C:\Users\ariel\.codex\AGENTS.md` has no version history. It sits outside every
repository, and `Claude-Global-File-History` does not copy it. Its synchronized
block can be rebuilt from `design/implementation-rules.md`; its Codex-only
sections have no other durable copy.

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

## BRAINSTORM - Bounded Knowledge Delivery and Capability Discovery

*Saved preliminary thinking from the September 2026 instruction-capacity and
capability-discovery investigation. This section is not authoritative design,
a requirement, an implementation instruction, or implementation authorization.
Any part may change or be rejected when this subject receives dedicated design.
Everything above this heading remains the current architecture.*

### Problem the future design would address

The Production Studio is intended to keep accumulating rules, proven solutions,
reusable methods, project knowledge, generators, checks, and other capability
across many projects while later work becomes better engineered and faster.

The current delivery model makes too much accumulated learning compete for
always-loaded context. Repeated compression can create temporary headroom but
does not provide a way for total Studio knowledge to grow indefinitely.

A second problem appears before implementation: an agent can fail to discover
that a requested result is already solved, deliberately unsupported, owned by
an accepted human prerequisite or refusal, or substantially covered by an
existing capability. A rule found only after an approach has already been
chosen is too late to prevent unnecessary design.

`INV-010A` in the AutoHotkey Project Proven Solutions Library
(`C:\Users\ariel\Projects\1AutoHotkey\project-proven-solutions-library`)
preserves the verified evidence and boundaries behind these concerns. This
section preserves only the current proposed direction. Deferred Work `D-080`,
`D-081`, and `D-082` in the AutoHotkey ledger own the future work.

### Current synthesis

A future architecture may separate total Studio knowledge from the smaller
working context needed for one task.

Possible cooperating parts are:

1. **A deliberately bounded universal kernel.** Keep always-loaded only the
   obligations that genuinely must govern reasoning before narrower delivery
   can occur, such as authorization boundaries, settled-context protection, and
   a requirement to establish that a real unsolved need exists before declaring
   a gap or offering new machinery.

2. **Task identity before broad discovery.** Where a reliable source already
   knows the repository, operation, journey, phase, or affected area, use that
   identity to narrow what guidance and capability could matter before asking
   the model to search semantically.

3. **Capability discovery before solution choice.** Start by asking what already
   exists at the project, journey, visible-behavior/UA, implementation, and
   proven-evidence levels. Consider accepted human prerequisites, refusals,
   unsupported cases, existing workflows, helpers, generators, templates,
   checks, and provider-native operations as capabilities, not only reusable
   functions.

4. **Scoped delivery of detailed rules.** Guidance that applies only to a
   recognizable task, phase, file area, command, journey, or lifecycle moment
   may be delivered only when that scope applies rather than being loaded in
   every conversation.

5. **Mechanical enforcement where it is cheaper and stronger than prose.**
   Checks, hooks, validators, generators, CI, native refusals, or other
   deterministic mechanisms may own obligations that do not require the model
   to reason from the complete prose rule beforehand.

6. **Learning and promotion.** A new lesson should not automatically become
   another standing instruction. Its cheapest durable form might instead be a
   scoped rule, Library record, check, capability owner, helper, generator,
   template, or nothing permanent. Mature instructions that repeatedly describe
   how to create the same correct result may sometimes graduate into reusable
   executable capability.

The intended effect is that total Studio knowledge can keep growing while the
agent's active task context stays bounded and increasingly focused.

Three cooperating systems emerged from the discussion: rule delivery answers
what governs this work now; capability discovery answers what already exists
that solves or nearly solves the problem; learning and promotion answers what
durable form a lesson should take so later projects inherit working capability
rather than only instructions.

### Possible reliability order

Where several delivery mechanisms could fit, the current thinking is:

1. deterministic code, check, refusal, hook, or policy where a miss is
   unacceptable and the condition is mechanically knowable;
2. universal kernel where the rule must govern reasoning before task-specific
   delivery can reliably happen;
3. deterministic task, event, path, or generated-request delivery where scope
   can be identified reliably;
4. skill, playbook, or other on-demand procedure for a recognizable recurring
   task;
5. semantic retrieval for supporting knowledge;
6. memory for low-authority working context.

This is a brainstorming hierarchy, not a settled requirement. A narrow
procedural rule should not enter the kernel merely because semantic retrieval
might miss it; its delivery trigger should be fixed instead.

### Possible use of existing Studio structure

The Studio may already contain enough hierarchy to avoid inventing a separate
hand-maintained capability catalog:

- Studio and project ownership identify the broad scope.
- Journey Scope and Purpose files identify what each journey does.
- Intended-behavior headings and UA titles name visible behaviors, agreements,
  prerequisites, refusals, and recovery boundaries.
- Code maps identify implementation once the behavior is known.
- KP, INV, and TECH metadata expose proven evidence and reusable methods.
- Existing generators, templates, helpers, checks, and project-template assets
  hold reusable capability.

A future generated navigation index could derive names and pointers from these
authoritative owners without becoming another semantic authority. Whether such
an index is worthwhile, what it contains, and whether it remains inside the
settled no-component-catalog boundary are open questions.

### Candidate delivery mechanisms to evaluate later

Possible mechanisms raised during the investigation include:

- coding-agent prompt-submit hooks that receive deterministic task identity
  before the model reasons;
- task identity carried in ChatGPT-relayed prompts, so relevant material can
  arrive before the agent reasons;
- pre-tool or other event hooks that deliver rules before an applicable edit,
  command, commit, or irreversible action;
- a small delivery map read by machinery rather than loaded into model context;
- Claude Code path-scoped rules;
- skills for recognizable recurring procedures;
- generated requests that already carry their operation-specific procedure;
- checks or Git hooks that enforce artifact-state rules;
- generators and templates that embody proven conventions rather than asking
  each agent to reconstruct them.

These mechanisms are unproven for the proposed Studio architecture. Provider
hook behavior, failure handling, context-size limits, Codex patch/file identity,
and the actual maintenance cost must be verified before any is adopted.

### Kernel admission and graduation idea

If the future design uses a kernel, admission should be difficult rather than
the default home of every important rule.

A possible rule belongs there only when missing it before narrower delivery can
occur would create material wrong work and no reliable narrower mechanism owns
that earliest moment.

A kernel rule should also be able to leave later if a narrower reliable
delivery or executable owner is proven. Importance alone should not make kernel
membership permanent.

The current 24,576-byte Studio Codex ceiling could eventually serve as one
architectural pressure against kernel growth rather than merely a recurring
compression trigger. That use is not yet approved.

### Capability reuse and the separate validity question

Finding an existing capability is not sufficient by itself. A previously proven
solution may have been valid only under an earlier environment or scope.

The separate future discovery question is how to determine whether the
solution's proven assumptions still cover the present task and whether the
correct response is direct reuse, generalizing its owner, superseding it for a
broader case while preserving its narrower proof, or using something different.

That question should use the Project Proven Solutions Library's existing Proven
Scope and Supersession model rather than inventing a competing evidence system.
Its exact policy remains undesigned.

### Pilot before generalization

If a bounded-knowledge architecture is later approved, `1AutoHotkey` is the
natural first implementation because this architecture already identifies it as
the Production Studio pilot where Studio practices are proven before they are
generalized.

The pilot should establish through real work whether the system actually:

- discovers existing capability before unnecessary machinery is designed;
- delivers the applicable rules at the required moment;
- preserves authorization and other high-consequence obligations;
- reduces standing-context pressure rather than merely moving it elsewhere;
- reduces rediscovery, agent effort, user review, rework, and mental overhead;
- allows accumulated knowledge to improve later work without requiring every
  lesson to be loaded every time.

No pilot work is authorized by this section.

### Open design questions

Dedicated future design would still need to settle at least:

- exact kernel admission and graduation criteria;
- which guidance requires deterministic delivery and which may rely on
  recognition;
- whether Studio-wide hooks are justified;
- provider-specific failure behavior when delivery machinery fails;
- whether an irreversible first action should ever be refused until applicable
  guidance arrives;
- task-identity format and who owns it;
- whether generated navigation is useful and how it stays derived rather than
  authoritative;
- module ownership, boundaries, and size;
- Claude memory's remaining role;
- cross-project capability-discovery reach;
- how new learning is classified into prose, evidence, enforcement, reusable
  executable capability, or nothing permanent;
- how the AutoHotkey pilot should measure whether quality rises while production
  cost falls.

When this subject becomes active design, reassess this section rather than
treating its detail as a specification.

### Added by Claude: candidate placement criteria

A candidate test for where a rule belongs, from the design round:

- **Kernel** only if all three hold: the rule can apply in a turn with no tool
  call, such as discussion, review, or a report; missing it is costly, such as
  unauthorized action, a false need that leads to machinery, or a misleading
  report; and no check at a fixed moment can enforce it.
- **Machine enforcement** when compliance can be decided from files at a fixed
  moment, such as a commit or a check run, and doing the work right does not
  need the prose beforehand. The check's failure message is then the delivery.
- **Event-delivered module** when the rule's earliest moment is an edit to a
  matching file, a matching command, a commit, a session start, or a
  menu-generated request. A module would stay under a size cap; Codex replaces
  hook context over 2,500 tokens with a partial preview by default.
- **Recognition trigger**, a one-line kernel pointer to an owner, only where no
  event exists and a miss costs moderately. Each would need a stated reason and
  would count against the kernel.
- **Library** holds evidence, never delivery. **Claude memory** holds facts
  about Ariel and preferences that have no other owner.

Moving a rule out of the kernel would need, in one change, an event that fires
before the rule's earliest moment in both agents, the text moved to its module
with its delivery entry, deletion from the kernel, any anchoring check pointed
at the new place, and one smoke delivery per agent. An observed miss where no
event preceded the rule would send it back, or add an event.

### Added by Claude: worked placement examples

- **The discovery rule** would be kernel. The claims it controls happen in
  discussion, reviews, and closeouts, where no tool call precedes them, and a
  miss caused the incidents in `INV-010A`.
- **The intentional-workflow-result rule** could be a module delivered with code
  editing and debugging. Its damage, building recovery or detection machinery,
  needs either a claim or an edit. A claim is already stopped by the kernel's
  discovery gate, which sends the agent to the behavior's design owner, where
  intentional states are recorded, for example the Handoff design's
  `The Native Codex Screen After Intentional Shutdown`. An edit would trigger
  the module.
- **`Correct the owner, not the symptom`** would stay in the kernel
  provisionally, until evidence shows the discovery gate covers its proposal
  moment.

Illustrative classification of the September 2026 rules, not a proposal to
rewrite them: a code-edit module for `Proof and implementation speed`,
`Waits and synchronization`, `Working or removed`, `Trace values`, `Comments`,
and `User-visible identifiers`; a destructive-command module for
`Enumerate before filtering`, delivered by refusing the first `Stop-Process`,
`taskkill`, or deleting command; a standing-file module for
`Durable files contain no one-run state` and `Line endings`, backed by
`.gitattributes` and a check; a commit module for the AutoHotkey `AGENTS.md`
items 23 to 25 and the Codex checkpoint format, backed by `commit-msg`; and a
live-run module for AutoHotkey items 4, 5, and 10, delivered by commands that
start or stop `AutoHotkey64.exe`. Under that classification the Codex
always-loaded total was estimated at roughly 11 to 12 KB instead of the measured
23,114 bytes. That is an estimate, not a measurement.

### Added by Claude: candidate delivery paths in each agent

Documented provider behavior, not tested on the installed versions:

| Moment | Claude Code | Codex |
|---|---|---|
| Kernel | Import from one Studio kernel file plus the project `CLAUDE.md` | Global `AGENTS.md` carrying a checked copy of the kernel only, plus project `AGENTS.md` |
| Before a matching file edit | Pre-tool hook on Edit or Write using `file_path`; native path-scoped rules also cover reads | Pre-tool hook on `apply_patch`; how its file paths are exposed is untested |
| Before a matching command | Pre-tool hook on Bash using the command; a refusal shows its reason | Pre-tool hook on the shell tool; a refusal hides its reason, so the module goes in added context beside it |
| After compaction | Session-start hook with source `compact` clears the record of delivered modules | Same |
| Mode phrases and generated prompts | Prompt-submit hook matches the exact phrase or marker | Same; the script reads the prompt text because matchers are ignored |
| Commit | `.githooks/commit-msg` plus a pre-tool hook on `git commit` | Same |
| Menu operations | Generated requests, already in place | Same |

Codex reads files through shell commands, so read-time delivery for Codex
depends on parsing commands and is the weakest path. The kernel copy would stay
native for Codex rather than moving into a session-start hook, because a failed
hook would silently remove every Studio rule from the session.

Prompt submission is the earliest documented moment in both agents, before the
agent reasons. It is the natural bridge between capability discovery and rule
delivery. Relayed ChatGPT prompts already open with fixed markers such as
"Read-only confirmation", so a fixed task-identity line would be cheap for
those prompts. Messages Ariel types herself carry no identity; for those the
kernel's discovery gate would be the fallback.

### Added by Claude: keeping the router from becoming a catalog

- A delivery map would be read only by the hook script, never loaded into an
  agent's context, so its size would cost no standing bytes.
- Map entries would name areas and kinds of moment, such as file patterns,
  command patterns, generated-request markers, and session sources, never
  individual rules. A new rule would add no map entry unless it created a new
  kind of moment.
- A module that reached its size cap would split into narrower matches, which
  also makes delivery more precise.
- Each module would be delivered once per session and again after compaction,
  so repeated edits do not re-inject the same text.
- The Library README already anticipates a generated or database-backed search
  ("Agents search record front matter now; a generated or database-backed index
  can replace that search later"), which is what `D-012` owns. A generated
  heading index would follow that direction, whereas a hand-maintained catalog
  would not.

### Added by Claude: capability discovery through existing owners

- **Project to journey.** Each journey's `design-scope-and-purpose.md` is, by its
  standard, one paragraph saying what the journey does, so together they are a
  compact journey-level capability list. The AutoHotkey `AGENTS.md` item 3
  already requires reading them, but only "before coding".
- **Journey to behavior.** `design-intended-behavior.md` is organized by visible
  behavior, and UA headings are behavior-level reminders. The headings alone list
  what exists, including agreements and refusals. Both `INV-010A` incidents
  needed exactly that: the working notice and the discard behavior.
- **Behavior to implementation and evidence.** The matching code-map entry and
  the KP, INV, and TECH records it names, searched through front-matter
  `search_terms` and `applies_to`.
- **Across projects.** Library records with `scope: studio`,
  `candidates-for-reuse-across-projects/`, and `project-template`.
- A candidate generated index per journey would list design headings, UA
  identifiers with titles, and code-map function names, rebuilt from the owners
  with nothing hand-maintained, and delivered by the prompt-submit hook for the
  journey a prompt names.

### Added by Claude: promotion triggers that already exist

The Studio already promotes knowledge when something repeats: a KP entry
requires `repeated`; a second journey depending on a code surface triggers a
cross-journey code map; several similar bounded tasks justify a fast-lane file;
project completion moves candidates into
`candidates-for-reuse-across-projects/`. The missing step is graduating a
repeated rule into a helper, generator, template, or check that later projects
inherit, and retiring the prose once they do. The question "what is the
cheapest durable form of this lesson?" could be asked at moments that already
exist: the closeout routing in the AutoHotkey
`MASTER-conversation-handoff-generator.md`, the retrospective efficiency loop,
and the Library's TECH admission.

### Added by Claude: detecting a missed delivery without broad proof machinery

- The existing conventions check could fail when a map entry points to a missing
  module, a module exceeds its size cap, or the kernel exceeds its budget.
- Each delivered module could begin with a line naming itself, so a transcript
  shows whether it arrived, and triage of a rule failure would first ask
  whether the rule was delivered.
- Claude Code's `InstructionsLoaded` hook event logs native rule loads.
- After any hook change, one smoke delivery per agent: one matching edit in a
  scratch file, confirming the named module arrived.
- Known limit: both agents continue when a hook fails, so a failed hook means a
  missing module until the failure is noticed.

### Added by Claude: estimated cost and implementation choices raised

- Rough permanent machinery for the hook route: a shared hook script of about
  120 to 200 lines, handling two event shapes, map matching, delivered-module
  tracking per session, section extraction, and JSON output; hook configuration
  of about 20 lines per agent; delivery maps of about 10 to 30 lines each; about
  30 to 50 lines added to the conventions check. About 200 to 300 lines in
  total, Moderate, paid once for every Studio project. Codex would also need a
  trust review of each hook definition.
- The hook script's language is an open choice: the AutoHotkey project's rule
  that AutoHotkey v2 is primary governs that repository, while a Studio-wide
  hook would serve every project, most of which are expected to be web
  applications.
- Claude memory under the architecture: governing rules would move to the
  kernel or a module with the memory entry deleted in the same change, and
  command lessons would become command-event modules that also reach Codex,
  which memory never does. Examples from the September 2026 memory index: long
  Bash heredocs failing, `/Switch` arguments run from Bash, AutoHotkey
  validation needing `Start-Process`, probes needing DPI awareness, and
  `Get-Process` listing one window per application. `D-050` owns the existing
  memory review.
- Before depending on any hook, verify the documented behavior on the installed
  Codex (`codex-cli 0.154.0-alpha.6.2` in September 2026) and in both agents'
  VS Code integrations.

### Added by Claude: cautions

- The layered model must not become a framework. Each layer already has an
  owner: the kernel in `CLAUDE.md` and the `AGENTS.md` kernel; task identity in
  hook input and a prompt identity line; scoped catalogs in maps that no agent
  loads; full owners in design documents, the debugging protocol, and the
  Library; golden paths in the Handoff generator, `project-template`, and
  existing helpers; enforcement in checks and Git hooks; learning in closeout
  and retrospective routing. Needing anything beyond a hook script, maps, and
  small check additions would be a sign of drift.
- "Load applicable scoped guidance before acting" should not be a kernel
  instruction, because it depends on recognition. Delivery should do the
  loading, and the kernel would only say that delivered modules govern.
- The broader external survey ChatGPT relayed, covering OpenAI's internal Codex
  account, the Agent Skills specification, Cursor, Windsurf and Devin, GitHub
  Copilot, Sourcegraph, Aider, Backstage, Nx, and golden paths, reached the same
  pattern, but it was not independently verified and is not evidence.
