---
description: "Use when creating or updating repository documentation, technical design notes, architecture docs, API notes, or task markdown. Covers concise structure, diagrams-first communication, and low-noise documentation style."
applyTo: "docs/**/*.md,tasks/**/*.md"
---

# Documentation Guidelines

Use this instruction for documentation changes in this repository.

## Primary Style

- Follow the documentation method already demonstrated in `tasks/002- tech_design.md`.
- Prefer diagrams, tables, short sections, and compact bullet lists over long prose.
- Keep explanations direct and decision-oriented.
- Write documentation so that a reader can recover the system shape quickly without reading large text blocks.

## Preferred Structure

Use only the sections that add value for the specific document:

- short title and scope
- concise rationale or decision summary
- tables for contracts, responsibilities, fields, or tradeoffs
- Mermaid diagrams where a visual model is clearer than prose
- short implementation notes or constraints
- explicit assumptions, open questions, or follow-up items when needed

## Diagrams First

- Add a Mermaid diagram when architecture, flow, ownership, or state transitions are central to the topic.
- Prefer simple diagrams that match the document purpose:
  - flowchart for process and request flow
  - sequence diagram for interactions
  - graph-style component or dependency diagram for structure
- Keep diagrams readable and small enough to scan quickly.
- Avoid decorative diagrams that repeat the surrounding text.

## Keep Text Tight

- Prefer short paragraphs.
- Prefer tables when comparing options, endpoints, fields, responsibilities, or constraints.
- Prefer bullets for rules and operational notes.
- Avoid repeating the same point across sections.

## Code Snippet Policy

- Do not paste large code blocks into documentation.
- Include code only when a short example is necessary to explain a contract, interface, payload shape, or configuration detail.
- When possible, summarize code behavior in tables or diagrams instead of embedding implementation.
- If a longer example is unavoidable, keep it narrowly scoped and only include the essential lines.

## Repository-Specific Placement

- Put backend documentation in `docs/backend/`.
- Put frontend documentation in `docs/frontend/`.
- Put requirement changes in `docs/requirements/` only when the expected product behavior changes.
- Keep `tasks/` focused on implementation design, planning, and working technical artifacts.

## Consistency Rules

- Keep terminology aligned with the repo's current design and requirements documents.
- Reflect the current implementation and test expectations rather than aspirational architecture.
- When a feature changes behavior, update both the relevant technical doc and any requirement or design document that would otherwise drift.
- If the change affects frontend-backend interaction, document the contract from both sides clearly.

## What To Avoid

- long narrative sections that hide the key decision
- large copied code listings
- vague diagrams with unlabeled nodes or missing relationships
- documentation that describes planned behavior as if it already exists
- duplicating language-specific coding instructions that already live in the Angular and .NET instruction files