---
description: "Generate the full numbered documentation catalog for this repository in one run. Use for autopilot documentation creation, initial documentation scaffolding, or full catalog refresh."
agent: documentation-catalog-generator
---

## User Input

```text
$ARGUMENTS
```

Generate or refresh the full documentation catalog for this repository.

Interpret `$ARGUMENTS` as:

- `<documentation-folder>`

Defaults:

- documentation folder: `Documentation`

Execution requirements:

1. Inspect the repository before writing documentation.
2. Create all missing numbered files from the template set.
3. Populate the documents using repository evidence.
4. Update the catalog README.
5. Do not make code or configuration changes.
6. Do not write secrets into documentation.
7. Continue until the full catalog is generated unless blocked by missing evidence.
