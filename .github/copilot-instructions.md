# Application Documentation Guidance

Use this repository's role-based documentation agents, instructions, and skills when the user asks to generate, extend, review, or standardize an application documentation catalog.

## Goals

- Produce a numbered documentation set with stable filenames and predictable scope.
- Keep documentation grounded in code, configuration, database artifacts, pipeline files, and observed behavior.
- Prefer factual statements over assumptions. Label assumptions explicitly.
- Update the catalog README when adding, removing, or renaming documents.
- Maintain a session log when documentation work spans multiple interactions.

## Phase Awareness

This repository operates in one of two phases. Read the phase indicator below before acting.

> **CURRENT PHASE: `documentation`**
> To switch phases, change the value above to `implementation`.

### Documentation Phase — Hard Guardrails

Active when `CURRENT PHASE` is `documentation`.

- These constraints are reinforced by the dedicated `documentation-safety.instructions.md` file for documentation assets.
- Documentation work is read-only with respect to application code and runtime configuration.
- Do not modify source code, tests, database scripts, pipelines, infrastructure definitions, or application configuration files while performing documentation work.
- Only documentation artifacts may be created or edited during a documentation task.
- Do not copy secrets into documentation. Never record passwords, API keys, tokens, connection strings with credentials, certificates, private keys, client secrets, or other sensitive values.
- If sensitive values are required for explanation, redact them and describe their purpose, location, and ownership instead.
- If a documentation request reveals an exposed secret, document the risk in generalized terms without reproducing the secret value.

### Implementation Phase — Allowed Behaviors

Active when `CURRENT PHASE` is `implementation`.

- Source code, tests, database scripts, pipelines, infrastructure definitions, and configuration files may be created or modified.
- Normal coding, refactoring, bug fixing, and feature work are permitted.
- Documentation artifacts may still be created or updated alongside code changes.
- Secret-handling rules remain in effect in all phases: never copy credentials into any file.

## Role Selection

Use the best-matched role agent for the requested output:

- Architecture or system map: `documentation-lead`
- Business logic or inferred rules: `business-analyst`
- Manual validation or acceptance coverage: `qa-engineer`
- Risks, debt, legacy patterns, operational hazards: `legacy-code-analyst`
- Modernization sequencing and safe change plans: `refactoring-planner`
- Decision chronology and progress notes: `session-logger`
- Work breakdown, backlog, progress tracking: `work-monitor`

## Documentation Standards

- Keep numbering stable once a catalog exists.
- Use explicit evidence sources where possible: page names, class names, SQL objects, config keys, pipelines, logs.
- Prefer tables for inventories, catalogs, access matrices, and data dictionaries.
- Separate facts, known gaps, and recommendations.
- When behavior is inferred rather than observed directly, say so.
- Redact or generalize sensitive operational details before writing them into documentation.

## Template Usage

When creating a new catalog, start from `templates/agent-documentation/` and tailor content to the target application.

## Review Expectations

When reviewing an existing catalog:

- identify stale content
- flag unsupported claims
- note missing source coverage
- preserve existing numbering and links where feasible
