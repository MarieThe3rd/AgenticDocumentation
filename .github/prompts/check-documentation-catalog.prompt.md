---
description: "Audit the existing numbered documentation catalog for completeness, Mermaid usage, metadata coverage, placeholder cleanup, and secret safety."
agent: documentation-catalog-validator
---

## User Input

```text
$ARGUMENTS
```

Validate the existing documentation catalog for this repository.

Interpret `$ARGUMENTS` as:

- `<documentation-folder>`

Defaults:

- documentation folder: `Documentation`

Execution requirements:

1. Inspect the documentation folder and compare it against the expected numbered catalog.
2. Report missing files, stale placeholders, missing metadata, and README mismatches.
3. Report diagram sections that are not Mermaid-based.
4. Report obvious secret leakage risks in markdown without reproducing the values.
5. Do not make code or configuration changes.
6. Do not rewrite documentation unless the user explicitly asks for fixes after the audit.