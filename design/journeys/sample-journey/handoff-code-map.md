# handoff-code-map.md

Project: [Project Name]
Journey: [Journey Name]

## Context Loading Order

1. This Handoff Code Map
2. Project Design Scope & Purpose — `../../design-scope-and-purpose.md`
3. Project Design Behavior Details — `../../design-behavior-details.md`
4. Journey Design Scope & Purpose — `design-scope-and-purpose.md`
5. Journey Design Behavior Details — `design-behavior-details.md`
6. Handoff Brief, if present — `handoff-brief.md`
7. Implementation files listed below

## Purpose

Serve as the context entry point for this journey and help a coding agent quickly understand and navigate the implementation files while minimizing unnecessary exploration.

Provides:

- Context loading order
- Implementation files
- Navigation to the correct functions, handlers, or components
- Important shared state
- Fragile implementation facts
- Key design decisions

## Implementation Files

Primary implementations:

- [Primary implementation file]

Related implementations:

- [Related implementation file, or None yet]

Language and stack:

- [Language, framework, or platform]

## Journey Structure

Describe where this journey appears within the product or menu hierarchy.

## Navigation Index

| Function, handler, or component | Purpose | Important dependencies |
|---|---|---|
| [Name] | [Purpose] | [Dependencies] |

## Shared State

**[Variable, store, service, or shared component]**

Describe its purpose and why it matters.

## Fragile Implementation Facts

- [Non-obvious implementation fact that a coding agent must not overlook]

## Journey Boundary

Avoid changes outside this journey unless they are required to support it.

## Design Decisions

- [Important intentional decision that should not be casually changed]
