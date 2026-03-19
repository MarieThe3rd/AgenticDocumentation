---
description: "Refresh an existing numbered documentation catalog for this repository in one run. Use for incremental updates after repository changes or when the catalog exists but is stale."
agent: documentation-catalog-refresher
---

## User Input

```text
$ARGUMENTS
```

Refresh the existing documentation catalog for this repository.

Interpret `$ARGUMENTS` as:

- `<documentation-folder>`

Defaults:

- documentation folder: `Documentation`

Execution requirements:

1. Inspect the repository and the current documentation set before writing.
2. Update stale or incomplete documents using repository evidence.
3. Create any missing numbered files from the template set.
4. Update the catalog README.
5. Use Mermaid for all new or updated diagrams.
6. Do not make code or configuration changes.
7. Do not write secrets into documentation.
8. Continue until the refresh is complete unless blocked by missing evidence.
