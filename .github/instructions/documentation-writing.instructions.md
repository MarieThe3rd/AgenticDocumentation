---
description: Use when writing technical application documentation that should be evidence-driven, concise, and reusable across teams.
applyTo: "**/{Documentation,docs}/**/*.md"
---

# Documentation Writing Rules

- Write for engineers, analysts, QA, and maintainers.
- Prefer direct statements and concrete terminology.
- Use tables for inventories, mappings, permissions, configuration, reports, and test cases.
- Cite source artifacts in prose using repository-relative paths when known.
- Separate present-state documentation from future-state recommendations.
- Mark inferred logic clearly.
- Do not hide gaps. Call out unknowns, risks, and implementation inconsistencies.
- Keep headings short and scannable.
- Use status, date, and source sections near the top of major documents.
- Treat documentation work as read-only analysis of the system. Do not make code, schema, pipeline, or app-setting changes while documenting.
- Never write secrets into documentation. Redact passwords, tokens, keys, private URLs with credentials, connection strings containing credentials, and similar sensitive material.
- When sensitive configuration matters to understanding, document the type of secret, where it is sourced from, and which component depends on it, but not the value itself.
- All diagrams must be authored in Mermaid.
- Prefer Mermaid flowcharts, sequence diagrams, ER diagrams, state diagrams, and class diagrams where appropriate.
- Do not use screenshots or external diagram binaries as the primary documentation artifact.
