---
description: "Generate or refresh the refactoring plan for a .NET full framework ASP.NET Web Forms application. Produces a phased migration roadmap with risk inventory, sequencing diagram, and cross-links to supporting catalog documents."
agent: webforms-refactoring-planner
---

## User Input

```text
$ARGUMENTS
```

Generate or refresh the Web Forms refactoring plan for this repository.

Interpret `$ARGUMENTS` as:

- `<documentation-folder>` — the catalog folder (default: `Documentation`)
- `<migration-target>` — the target framework if known (e.g., `ASP.NET Core MVC`, `Blazor Server`, `Minimal API`)

Defaults:

- documentation folder: `Documentation`
- migration target: ask the user if not provided and not determinable from the repository

Execution requirements:

1. Load `.github/skills/webforms-refactoring/SKILL.md` before producing any output.
2. Inspect the repository for `.aspx`, `.aspx.cs`, `.master`, `.ashx`, `Global.asax`, `Web.config`, and `IHttpModule` / `IHttpHandler` implementations.
3. Inventory ViewState usage, ScriptManager patterns, FormsAuthentication configuration, Membership/Roles providers, and Session state mode.
4. Identify inline SQL, `Response.Write` / `<%= %>` XSS risks, and `System.Web` references in shared libraries.
5. Produce or update `04-Refactoring-Plan.md` with phases, prerequisites, work items, exit criteria, and a Mermaid sequencing diagram.
6. Populate a risk table with findings ranked by impact and likelihood.
7. Record security findings in `15-Security-Remediation-Checklist.md` without reproducing secret values.
8. Update cross-links in `03-Technical-Debt-and-Risks.md`, `09-External-Integrations.md`, and `13-Configuration-Reference.md` where supporting evidence exists.
9. Do not modify source code, tests, Web.config, or any application file.
10. Do not write secrets, connection strings with credentials, passwords, or tokens into any documentation file.
