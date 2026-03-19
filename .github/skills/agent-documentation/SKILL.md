---
name: agent-documentation
description: "Use when creating, updating, reviewing, or standardizing a numbered application documentation catalog with role-based agents, reusable markdown templates, and cross-document consistency checks."
---

# Agent Documentation Skill

Use this skill for documentation portfolios that need a stable, repeatable structure across multiple repositories.

## Use Cases

- create a new application documentation catalog
- standardize an existing documentation folder to the 00-19 structure
- fill gaps in architecture, QA, risk, configuration, report, or onboarding documentation
- review an existing catalog for staleness, unsupported claims, and missing coverage
- run a one-command autopilot generation of the full catalog via `/generate-documentation-catalog`
- run an incremental documentation refresh via `/refresh-documentation-catalog`
- audit a catalog with `/check-documentation-catalog`
- run a focused secret scan with `/check-documentation-secrets`

## Inputs To Gather

- target documentation folder
- primary source locations such as `src/`, `tests/`, `builds/`, `docs/`, database scripts, and pipeline files
- whether the user wants a full catalog or only selected documents

## Workflow

1. Inspect the existing documentation folder and README if present.
2. Preserve numbering and filenames when a catalog already exists.
3. Use the bundled templates in `.github/skills/agent-documentation/templates/agent-documentation/` for missing files.
4. Match work to the appropriate role agent:
   - Documentation Lead for architecture, onboarding, deployment, screen flow, and catalog consistency
   - Business Analyst for business rules, permissions, workflows, glossary, reports, and survey behavior
   - QA Engineer for manual test plans and validation matrices
   - Legacy Code Analyst for debt, risks, troubleshooting, integrations, configuration, security, and stored procedure references
   - Refactoring Planner for phased remediation or modernization plans
   - Session Logger for `20-Session-Log.md`
   - Work Monitor for task breakdown or backlog tracking
5. Update the README to reflect the actual document set.
6. Record assumptions and known gaps instead of inventing unsupported detail.
7. Use Mermaid for every diagram included in the catalog.

## Safety Rules

- Documentation mode is read-only for application behavior: inspect and describe, but do not change source code, tests, pipelines, database scripts, or runtime configuration.
- Restrict edits to documentation assets unless the user explicitly changes the task to implementation work.
- Never reproduce secrets in documentation output. Redact or omit passwords, API keys, tokens, certificates, private keys, secrets in connection strings, and similar sensitive values.
- If a secret exposure is discovered, document the existence of the exposure and its risk without copying the underlying value.

## Quality Bar

- Every major document should declare author role, date, and status.
- Inventories should use tables.
- Recommendations should be separated from current-state documentation.
- Cross-links should be added where they reduce navigation cost.
- Statements derived from inference should be labeled as inferred.
- Diagrams should be written in Mermaid and kept close to the document section they explain.

## Output Expectations

- a coherent numbered catalog
- consistent headings and metadata
- explicit known issues and evidence gaps
- minimal duplication across documents

## Validation Expectations

The audit workflow should check at least:

- required numbered files exist
- README matches the actual catalog
- Mermaid is used for diagrams where diagrams exist
- documentation does not reproduce obvious secrets or credentials
- non-applicable documents are explicitly marked
- major documents include role, date, and status metadata

## Autopilot Entry Point

Use the prompt `/generate-documentation-catalog [documentation-folder]` when the user wants the full documentation set generated with minimal interaction.
Use the prompt `/refresh-documentation-catalog [documentation-folder]` when the user wants an incremental refresh of an existing catalog.
Use the prompt `/check-documentation-catalog [documentation-folder]` when the user wants an audit of catalog completeness and safety.
Use the prompt `/check-documentation-secrets [documentation-folder]` when the user only wants a focused secret, password, key, and token audit.

## Bundled Assets

- Skill README: `.github/skills/agent-documentation/README.md`
- Templates: `.github/skills/agent-documentation/templates/agent-documentation/`
- Examples: `.github/skills/agent-documentation/examples/`
