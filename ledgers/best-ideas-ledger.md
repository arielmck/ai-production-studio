# Best Ideas Ledger

## Document Anti-Drift

This ledger preserves accepted Best Ideas, their enduring value and supporting evidence; it does not own operative engineering rules, detailed implementation requirements, reusable code, technical knowledge records or unreviewed project-level candidates.

Preserve established ideas and their identifiers. Add, revise, combine or remove entries only with Ariel's explicit authorization, following the governing rules below.

## Purpose

The Best Ideas Ledger preserves the most valuable ideas that emerge through the development of Production Studio projects. These are ideas that materially improve what we create, how we design software or how we work.

The ledger develops across successive projects, allowing our best ideas to be refined, strengthened, reconsidered and enriched through experience.

## What Belongs Here

Record significant ideas that Ariel has deliberately accepted as Best Ideas with lasting value across Production Studio projects, rather than individual implementation solutions, ordinary engineering instructions, unfinished work or every useful discovery.

An accepted Best Idea may be supported by experience in one project or established through use across several projects. Describe its maturity accurately without requiring a formal classification system. Unreviewed candidates remain with their originating projects until deliberately accepted.

The ledger explains the ideas and why they matter. Detailed rules, implementation requirements, reusable code and technical knowledge remain in their appropriate authoritative owners. A Best Idea entry does not itself establish an operative requirement or authorize implementation.

## Entry Format

Use `BI-NNN` identifiers with three-digit zero-padded numbers and short descriptive titles. Identifiers must be unique within this ledger and remain stable once assigned. Numbers identify ideas, not their ranking or chronological order. Gaps are acceptable.

When promoting a candidate, identify its originating project and CBI identifier in the Best Idea's source/evidence. When another project contributes to an existing Best Idea, refine that entry rather than creating a duplicate.

For the AutoHotkey pilot, retain the originating CBI number when assigning the corresponding BI identifier, provided that number is available. Numbering conventions for candidates from subsequent projects will be established when needed; do not establish them prematurely.

Each entry contains:

**Idea:** Describe the idea clearly, emphasizing what makes it particularly valuable.

**Value:** Explain how the idea improves our software or how we develop software.

**Source/evidence:** Identify the experience, observations or authoritative records supporting the idea.

Include additional information, such as a possible destination, only when it adds meaningful value.

## Evolution and Review

Retain valuable ideas after their adoption into Production Studio practices. Refine existing entries as subsequent projects provide meaningful new insights or evidence.

Review ideas when Ariel deliberately chooses to do so, rather than requiring review only at project completion. Combine overlapping ideas when appropriate, and remove ideas that no longer deserve inclusion. Preserve useful knowledge and reconcile current references before removing an entry.

Do not turn the ledger into a historical archive, implementation rulebook, reuse catalog or collection of project-specific lessons.

## Authorization

Create, revise, combine or remove entries only when Ariel explicitly requests or authorizes the ledger change. Authorization to change the ledger does not authorize changes to its referenced documents, projects or governing rules.

## Best Ideas

### BI-014 — User Agreements (UAs)

**Idea:** User Agreements are one of our best ideas because explicitly agreeing on what the human will do, will not do, or is willing to accept can significantly improve the design of the software. Instead of building complex automation, safeguards and recovery mechanisms to handle every possible situation, we can identify situations where a simple human commitment, an occasional manual action or an accepted limitation allows for a simpler, more reliable and more maintainable design without compromising the intended result.

**Value:** User Agreements expand the design possibilities available to us. Recording these agreements independently of their technical implementation preserves their value as technologies, architectures and implementations evolve. This makes User Agreements a fundamental design concept of the Production Studio.

**Source/evidence:** Originated as AutoHotkey CBI-014. AutoHotkey's extensive development, practical use and refinement of User Agreements established the detailed conventions in `1AutoHotkey/design/README.md` under `User Agreements`. Those conventions govern deliberate human approval, qualification, wording, scope and preservation of actual agreements. Production Studio Foundations, `design/design-behavior-details.md` → `UA — User Agreement`, defines the foundational concept.
