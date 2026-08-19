# design-behavior-details.md

Project: AI Production Studio
Journey: none, this is a main project file

## Purpose

The studio's behavior is the working method it defines. This file holds the
working principles that hold whatever agent is in use. Each agent's own
interaction system, and where that system is configured, is in
`architecture.md`.

## Expected Behavior

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

## Current Behavior

Three agents are in use or expected, and their interaction systems are at
different stages.

- **ChatGPT.** Established and working. Discussion mode and engineering mode are
  the settled distinction.
- **Claude Code.** Established and under active refinement. Its authoritative
  files are named in `architecture.md`.
- **Gemini.** Not established. No interaction system has been designed for it,
  and none should be invented in advance. Learn it empirically when it is first
  used seriously.

## Completion Criteria

The current iteration is complete when the cross-agent principles above, each
agent's authoritative configuration location, and the relationships between the
repositories are recorded here and pointed to from the other repositories.

## Next

1. Record Gemini's interaction model once it has been used seriously enough to
   know what it needs.
