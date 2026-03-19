# Agent Documentation Skill Assets

This folder contains the installed documentation skill assets for this repository.

It provides four things:

- Generic role-based agents for producing and reviewing application documentation
- Instructions that keep the document set consistent and evidence-driven
- A reusable skill for generating or updating a numbered documentation catalog
- Markdown templates that mirror the 00-19 document structure used in this repository

## Design Goals

- Agent-specific, not squad-specific
- Portable across multiple applications and repositories
- Neutral naming so teams can use their own personas or no personas at all
- Consistent document numbering and section structure
- Easy to copy into another repository with minimal changes

## Installed Layout

```text
.github/
  copilot-instructions.md
  agents/
  instructions/
  prompts/
  skills/
    agent-documentation/
      SKILL.md
      README.md
      templates/
        agent-documentation/
      examples/
```

## Bundled Assets

- Skill definition: `.github/skills/agent-documentation/SKILL.md`
- Templates: `.github/skills/agent-documentation/templates/agent-documentation/`
- Examples: `.github/skills/agent-documentation/examples/`

## Recommended Usage

1. Use the repository root `Documentation` folder as the home for generated documentation.
2. Ask Copilot to generate or update the documentation catalog for the application.
3. The documentation agents and prompts will use the bundled templates from this skill folder.
4. Use the role agents when you want a specific perspective such as architecture, business rules, QA, risk, or refactoring.

## Autopilot Trigger

After copying the package into another repository, use the prompt below to generate the full catalog in one run:

- `/generate-documentation-catalog [documentation-folder]`
- `/refresh-documentation-catalog [documentation-folder]`
- `/check-documentation-catalog [documentation-folder]`
- `/check-documentation-secrets [documentation-folder]`

Example:

- `/generate-documentation-catalog Documentation`
- `/refresh-documentation-catalog Documentation`
- `/check-documentation-catalog Documentation`
- `/check-documentation-secrets Documentation`

What it does:

- scans the repository for source, tests, configuration, build, pipeline, and database artifacts
- creates any missing numbered documentation files from the template set
- updates the documentation README to match the generated catalog
- stays in documentation-only mode with no code changes and no secret reproduction

Use `generate` for the first full pass and `refresh` for later incremental updates when the repository has changed.
Use `check` to audit whether the catalog is complete, Mermaid-compliant, and free of secret leakage.
Use `check-documentation-secrets` for a narrower pass that only looks for passwords, keys, tokens, and similar sensitive values.

If you omit the argument, the prompt will default to `Documentation`.

## Diagram Standard

All diagrams in the generated documentation should be written in Mermaid.

- Use Mermaid for architecture diagrams, workflows, ERDs, dependency maps, and navigation flows.
- Do not embed screenshots, Visio exports, draw.io images, or external diagram formats as the primary source of truth.
- If a visual cannot be represented perfectly in Mermaid, provide the closest Mermaid version and note any simplifications.

## Validation Workflow

Recommended sequence in a new repository:

1. `/generate-documentation-catalog`
2. `/check-documentation-catalog`
3. `/refresh-documentation-catalog` after meaningful repository changes
4. `/check-documentation-catalog` again after refreshes

## Generic Role Set

- Documentation Lead
- Business Analyst
- QA Engineer
- Legacy Code Analyst
- Refactoring Planner
- Session Logger
- Work Monitor

These roles are intentionally generic. Teams can rename them locally without changing the document structure.

## Template Catalog

The template set includes:

- `README.md`
- `00-Architecture-Overview.md`
- `01-Business-Rules.md`
- `02-QA-Test-Plan.md`
- `03-Technical-Debt-and-Risks.md`
- `04-Refactoring-Plan.md`
- `05-Troubleshooting-Playbook.md`
- `06-Data-Dictionary.md`
- `07-Permissions-and-Roles.md`
- `08-Primary-Workflow.md`
- `09-External-Integrations.md`
- `10-Stored-Procedure-Reference.md`
- `11-Onboarding-Guide.md`
- `12-Screen-Flow-and-Navigation.md`
- `13-Configuration-Reference.md`
- `14-Glossary-and-Domain-Model.md`
- `15-Security-Remediation-Checklist.md`
- `16-Entity-Relationship-Diagram.md`
- `17-Deployment-and-Release-Runbook.md`
- `18-Feature-Configuration-Guide.md`
- `19-Report-Catalog.md`
- `20-Session-Log.md`

If a target application does not use one of those domains, keep the file and mark it not applicable, or remove it if the team prefers a smaller catalog.

## Notes

- The filenames preserve the existing numbering so downstream teams can compare catalogs across applications.
- The template names are application-neutral and can be adopted as-is across repositories.
