# design-scope-and-purpose.md

Project: AI Production Studio
Journey: none, this is a main project file

## Scope and Purpose

The AI Production Studio defines the methodology, tools, workflows, and
standards used to plan, design, build, review, test, and maintain software with
AI coding agents. It is built for roughly 20 to 50 projects, most of them
personal web applications. It owns what every project shares, including how the
agents and Ariel work together. Each project repository owns its own product,
its own rules, and its own design.

Efficient agent communication is part of that infrastructure, not a preference.
A report that buries its result costs reading time. A message that leaves the
decision unclear costs a round of clarification. Both are paid again in every
project, so across 20 to 50 projects a communication defect multiplies instead
of being absorbed. Work on how an agent writes is therefore studio work, and its
results are recorded here rather than in whichever project happened to expose
the problem.

## North Star

One place explains how work is done with AI agents, every project inherits it
without copying it, and a person can act on any agent's message the first time
they read it.

## Anti-Drift

**One agent's interaction rules are never promoted into universal rules.** What
ChatGPT needs is not what Claude Code needs, and what Gemini will need is
unknown. Principles that hold whatever the agent are recorded here. An agent's
own system stays with that agent and is named here, never restated.

**The rationale is written once.** Other repositories carry a short pointer that
names the file. A pointer cannot fall out of date; a summary always does.

**The studio does not accumulate process for its own sake.** Before a rule is
added, check whether an existing rule already covered the failure and simply went
unapplied. Prefer deleting a rule that never fires to adding one that might.
