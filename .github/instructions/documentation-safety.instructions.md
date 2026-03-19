---
description: "Use when generating, updating, reviewing, or standardizing documentation so the work remains read-only for the application and excludes secrets from all documentation output."
applyTo: "**/{Documentation,docs}/**/*.md"
---

# Documentation Safety Rules

These rules are mandatory for documentation work.

## Read-Only Scope

1. Documentation tasks are analysis-and-writing tasks, not implementation tasks.
2. Do not modify application source code, tests, database scripts, pipelines, infrastructure files, deployment files, or runtime configuration while working on documentation.
3. Limit edits to documentation artifacts only.
4. If a documentation request also asks for code fixes, stop and ask the user to split the work or explicitly change scope to implementation.
5. If you discover a bug, risky code path, or missing safeguard during documentation, document it as a finding. Do not fix it during the documentation task.

## Sensitive Data Rules

1. Never copy secrets or credentials into documentation.
2. This includes passwords, API keys, tokens, certificates, private keys, shared access signatures, client secrets, bearer tokens, cookie values, webhook secrets, and connection strings that contain credentials.
3. Redact sensitive values if they appear in source artifacts.
4. When the presence of a secret matters, document only:
   - what kind of secret it is
   - where it is sourced from
   - which component depends on it
   - who is expected to manage it
5. If sensitive information is already exposed in the repository, document the risk without reproducing the value.

## Conflict Resolution

1. When documentation and implementation are both requested, default to documentation-only behavior unless the user clearly changes scope.
2. When uncertain, prefer asking for scope clarification over making code changes.
3. If the documentation would be unsafe without quoting a secret value, do not include the value. Describe the dependency in redacted terms instead.

## Examples

- Allowed: document that an SMTP password exists in environment-specific configuration and should be rotated.
- Not allowed: paste the SMTP password or the full credential-bearing connection string into markdown.
- Allowed: note that a controller permits unauthorized access in one path.
- Not allowed: patch the controller during a documentation-only task.