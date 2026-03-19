---
description: "Scan documentation markdown for secrets, passwords, keys, tokens, and other sensitive values without running the broader catalog audit."
agent: documentation-secret-scanner
---

## User Input

```text
$ARGUMENTS
```

Scan documentation for secrets and sensitive values.

Interpret `$ARGUMENTS` as:

- `<documentation-folder>`

Defaults:

- documentation folder: `Documentation`

Execution requirements:

1. Inspect markdown files in the target documentation folder.
2. Report likely secrets, passwords, keys, tokens, private keys, certificate bodies, and credential-bearing connection strings.
3. Do not reproduce the sensitive values in the response.
4. Do not make code or configuration changes.
5. Do not rewrite documentation unless the user explicitly asks for fixes after the audit.
