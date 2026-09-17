# Production Studio Foundations

Project: AI Production Studio
Journey: none, this is a main project file

## Purpose

The studio's behavior is the working method it defines. This file holds the
working principles that hold whatever agent is in use. Each agent's own
interaction system, and where that system is configured, is in
`architecture.md`.

This file also defines the Studio's foundational Elements: what each Element is
for, why it exists, and where its detailed rules live. Detailed formats,
procedures, thresholds, implementation mechanics, and individual records remain
with their detailed owners rather than being duplicated here.

## Principles

Agent-independent working principles. Each one is followed by the reason it
exists, because a principle without its reason is the first thing to be argued
away.

**Discussion and implementation are different states.** Talking about a change
is not a request to make it. Exploring a design needs a state where nothing is
built, or the exploration keeps being cut short by work that was never asked for.

**Implementation requires explicit authorization.** Authorization is never
inferred from conversational momentum, from agreement with the reasoning, or
from how finished the design looks. On 2026-08-19 an agent read impatience in a
relayed critique as release, created a repository, wrote two scripts, and edited
a production file, none of which had been authorized.

**After an extended discussion, omitting the mode phrase does not authorize
implementation.** Only a clear instruction to change something does. A message
that criticizes how the agent is working is about the discussion, however
impatient it sounds.

**Read-only investigation resolves questions without authorizing
state-changing work.** Reading files, searching repositories, and running
reporting commands settle most design questions, and none of them changes
anything. Reaching for a broader grant than the question needs is what turns a
discussion into unrequested work.

**Finish the design decisions before asking for authorization.** Bringing a
half-settled design to the user forces them to manage the design process, which
is the work they delegated. Ask only for decisions that genuinely need their
preference.

**When asking for a real decision, give the practical implications first.** The
user should not have to ask what an option means before they can choose it.

**Never broaden a task beyond the agreed scope.** A newly discovered concern is
named as separate work rather than folded into the task in hand.

**Prefer applying an existing rule to adding a new one.** When a report or a
piece of work disappoints, the first question is which existing rule it broke.
Rules accumulate faster than they are read, and an unread rule prevents nothing.

**Use canonical and parallel terminology for formal Studio concepts.** Once a
formal concept has a canonical human-facing term and capitalization, use them
consistently rather than alternating among synonyms or casing. When sibling
concepts are discussed together, use parallel forms so wording differences do
not create false distinctions.

For Project Proven Solutions Library record types, ordinary prose uses
`KP`/`KP entry`, `INV`/`INV entry`, and `TECH`/`TECH entry`. If full words are
genuinely necessary, use only `Known Problems (KP)`, `Investigations (INV)`, or
`Techniques (TECH)`, with the acronym included every time. For singular grammar,
use the acronym form such as `a KP`, `an INV`, or `a TECH entry` rather than
inventing a singular spelled-out form.

On the first use of the grouping concept within each section, write
`Investigation Family (groups of related INVs)`. Later uses within that same
section may say `Investigation Family`.

`Cause Case`, `Problem Dimension`, and `Proven Solution` are separate formal
sub-concepts and keep those exact names and capitalization.

Literal schema keys, enum values, identifiers, filenames, `record_type` values,
relationship values, and other machine-required text retain their exact spelling
where changing them would alter mechanics. When a machine-required literal
differs from the canonical human-facing term, its authoritative schema or
definition site states the translation.

This exists to reduce human interpretation cost. Different names for the same
formal concept make the reader repeatedly decide whether a wording difference
carries meaning when it does not.

**Start from the closest existing user-visible capability before designing a
parallel one.** When new work substantially overlaps an existing user-visible
capability, whether that capability belongs to Production Studio tooling or to
the project being built, first inspect what already exists: its current design
and, where relevant, its code map, proven-solution records, and working
implementation. Identify what is already solved and what is actually different.
Prefer reuse or refactoring, and begin a parallel mechanism or fresh
provider/mechanism research only when the existing capability is insufficient.
Keep the search targeted rather than searching unrelated history or forcing
greenfield work into an unrelated mechanism.

This exists because the multi-slot Handoff work began considering new notices
and new closeout behavior before the existing Agent Conversation Continuation
and Agent Handoff capabilities were examined, even though those capabilities had
already proved much of the required lifecycle. Starting from the closest
working capability reduces duplicate research, parallel mechanisms, and
avoidable redesign.

**Agent memory is never the only owner of knowledge a future agent needs.** For
anything an agent's memory holds, ask: if that memory were unavailable, could a
future agent make a wrong decision, repeat a corrected mistake, redo meaningful
work, or lose settled work? If so, the knowledge belongs in its existing
authoritative stable owner, such as the design that governs the behavior, the
instructions that govern the work, a Project Proven Solutions Library record
that meets its evidence gate, or the architecture or environment description.
Memory may keep a pointer to that owner or a convenience copy.

When the user has deliberately postponed related work, its Deferred Work entry
may temporarily hold the information needed to resume and complete that work.
Deferred Work is not the permanent owner: when the deferred work is completed,
harvest information with continuing value into its authoritative stable owner
and delete the completed Deferred Work entry.

This exists because an agent's memory serves that agent's own working context,
while the knowledge the Production Studio depends on must reach every agent,
project, and later session that needs it.

## Elements

Elements are recurring concepts the Production Studio uses to keep human
decisions, proven knowledge, and temporary work in the right kinds of owners.
Foundations defines their purpose and relationship. Their detailed owners define
their formats, mechanics, thresholds, validation, identifiers, and individual
records.

The initial Elements are deliberately limited to the concepts below. Do not
expand this catalog merely because the Studio uses another identifier, document,
or artifact. An Element may also be optional in a particular project or
workflow.

### UA — User Agreement

A User Agreement records something Ariel deliberately agrees to do, avoid,
accept, prefer, tolerate, or handle herself when that agreement materially
changes intended behavior, what we intend to code, what software needs to
automate, protect, detect, recover from, or support, or what machinery can be
omitted or removed.

A UA commonly arises during design, but it may also become important during
implementation, debugging, refactoring, cleanup, or simplification. The actual
UA lives with the current authoritative behavior it governs so the human
agreement and its design consequence cannot silently drift apart.

Do not create a UA for ordinary product behavior, a machine-owned invariant, an
implementation limitation, a historical workaround Ariel has not accepted, or
a hypothetical agreement introduced merely to make implementation easier.

A UA identifier is a current locator, not a permanent historical identity. If a
UA moves to another authoritative owner, its identifier moves with that current
ownership. Do not build aliases, tombstones, used-number histories, redirects,
or other machinery whose purpose is reconstructing old UA identifiers.

For agents: do not invent a UA, broaden one Ariel made, or turn a preference,
fallback, or accepted manual boundary into a stronger obligation.

In the current AutoHotkey pilot, detailed UA writing, placement, identifier, and
movement rules belong in `design/README.md` under `## User Agreements`; actual
UAs belong in the authoritative current behavior owners they govern. Commit-time
UA reconciliation belongs in the project's existing Design reconciliation path.

### Project Proven Solutions Library

The Project Proven Solutions Library preserves **proven knowledge** so future
work can discover and reuse what has already been learned instead of paying to
rediscover it.

It is selective permanent knowledge, not a diary or an archive of every idea.
Hypotheses, proposed causes, candidate solutions, and other unproved material
stay outside permanent Library records until the applicable evidence gate is
met.

The Library is the parent Element for three kinds of permanent record:

- **KP** — one recurring problem, its proven causes, and its Proven Solutions.
- **INV** — one time-intensive investigation, with what it established and what
  it ruled out.
- **TECH** — one proven, reusable method.

The current detailed owner is
`1AutoHotkey/project-proven-solutions-library/README.md` and the records governed
by it. That owner defines record formats, admission thresholds, evidence rules,
scope, routing, identifiers, and individual records. Foundations does not
duplicate those mechanics.

### KP

A KP preserves one observed or evidence-established problem so future work can
recognize it and route back to proven knowledge. A new KP requires `repeated`:
the problem has recurred, and a reliably reproduced recurrence of the same
problem counts as recurrence.

Prefer the human experience of the problem as the recognition key when
practical. A recurring technical or internal problem is also valid. Name the
problem from what was observed or established, not from a suspected cause.

An agent may independently propose a KP after observing recurrence or reliable
reproduction. It does not wait for Ariel to notice the pattern first.

When an evidence-established technical state is merely the proven cause of a
problem an existing KP already represents, keep it there as a Cause Case. Give
that state its own KP only when the state itself is the recurring problem future
work will recognize and search for.

One problem may have more than one proven cause, and one cause may have more
than one Proven Solution. A KP can also preserve approaches the evidence
actually ruled out and Proven Solutions later superseded, because that evidence
can prevent expensive repetition. An approach that was merely considered,
dropped, or never proved does not become a failed approach in the permanent
record.

`time_intensive` may additionally be recorded when it is true, but it never
substitutes for `repeated`.

For agents: begin from the observed problem and its evidence fingerprint, then
reuse the matching proven knowledge rather than assuming that similar symptoms
must have the same cause.

### INV

An INV preserves a materially time-intensive investigation so future work does
not pay the same discovery cost again: what the evidence established, what it
ruled out, relevant alternatives, provider or tool behavior, successful
approaches, approaches the evidence disproved, and the limits of what was
actually proved.

A new INV requires `time_intensive`. Ariel explicitly asking for an INV is
itself sufficient to establish that gate, and no agent re-measures or
re-qualifies it. An agent may also establish the gate independently; reaching at
least twice the applicable Fast Track target, or one hour where no target
exists, is one sufficient trigger rather than the exclusive definition.

`repeated` may additionally be recorded when it is true, but it never
substitutes for `time_intensive`.

An INV does not have to end with one winning solution. Its value may be the
durable understanding of several conditions or workable choices and the
boundaries between them.

For agents: preserve established findings and their limits. Do not turn an
investigated possibility into a proven fact.

### TECH

A TECH entry preserves a proven, materially valuable way of working so that
useful knowledge is discoverable and reusable instead of having to be
rediscovered. One TECH entry represents one independently reusable method, which
may contain several rules or steps when they work together as that method. One
research question or INV may establish several TECH entries, and separate
methods are not combined merely because they were discovered together.

A TECH entry may originate in and currently apply to only one project. It is
admitted when the method is proven, materially valuable, has credible potential
for future reuse or adaptation, and is worth preserving because rediscovering it
would be expensive. All four must hold. One successful outcome is not enough.

The TECH entry itself stays concise: state the Rule, When it applies, Evidence,
and Where the proof stops. When the durable reusable knowledge is larger than
those four parts, Evidence points to the KP, INV, or other durable owner that
preserves the fuller evidence, conditions, approaches the evidence ruled out,
provider or tool findings, boundaries, and other established information needed
for future reuse.

Harvest and organize the proven knowledge so future work can discover it,
understand it, and evaluate whether and how it can be reused or adapted. Do not
limit the durable harvest to only what the current project can use within its
current scope. The current project may expand, and future projects may benefit
from proven knowledge that is not useful today.

A project-specific instruction is not automatically a TECH entry. It must clear
the TECH admission bar and contain durable knowledge worth preserving for future
discovery and possible reuse rather than merely describing how the current
project happens to operate.

Hypotheses, proposed explanations, and other unproved material do not belong in
a TECH entry or its permanent supporting records.

For agents: make the TECH entry easy to discover and reuse without duplicating
the full evidence story. Preserve the complete durable proven knowledge in the
appropriate permanent owner and make the TECH entry lead future agents to it.

### TMP — Temporary Working Document

A TMP is an optional generated, noncanonical working artifact used while work is
being prepared, reviewed, transferred, compared, or developed. It is temporary
working material, not authoritative current truth and not a permanent knowledge
record.

In workflows that use numbered TMP history, the current unnumbered TMP may be
the operationally active artifact. Numbered older TMPs are development history,
not current truth and not routine required reading.

Temporary debugging probes, logs, hypotheses, and unverified candidates are not
TMP merely because they are temporary; the current AutoHotkey process uses
`DBG-` for that debugging role.

In the current AutoHotkey pilot, the detailed `TMP-` prefix rules belong in
`design/project/reuse-considerations.md`, while each workflow's own TMP lifecycle
belongs in its authoritative behavior owner. Foundations does not define a
universal retention or deletion policy for TMP files.
