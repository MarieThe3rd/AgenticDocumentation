---
name: webforms-refactoring
description: "Use when creating or updating a refactoring plan for a .NET full framework ASP.NET Web Forms application. Provides domain knowledge of Web Forms patterns, migration targets, sequencing risks, and safe-change strategies."
---

# Web Forms Refactoring Skill

Use this skill when the target repository is a .NET full framework ASP.NET Web Forms application and the goal is to produce a modernization or refactoring plan.

## Use Cases

- produce a phased refactoring plan for a Web Forms application
- identify Web Forms-specific technical debt and migration blockers
- map postback lifecycle dependencies before extraction
- sequence a migration toward ASP.NET Core MVC, Minimal API, or Blazor
- document safe incremental steps that keep the application deployable at each phase

## Domain Knowledge — Web Forms Patterns to Recognize

### Page Lifecycle and Postback

- `Page_Init`, `Page_Load`, `Page_PreRender`, `Page_Unload` event sequence
- `IsPostBack` guards that mix initialization and mutation logic
- `__VIEWSTATE`, `__EVENTVALIDATION` hidden fields inflating page size
- `UpdatePanel` + `ScriptManager` for partial-page rendering (AJAX-like postbacks)
- `RegisterClientScriptBlock` / `RegisterStartupScript` for injecting JavaScript

### Code-Behind and Separation of Concerns

- `.aspx` markup tightly coupled to `.aspx.cs` code-behind
- Business logic embedded in code-behind event handlers
- `SqlDataSource`, `ObjectDataSource`, `GridView`, `Repeater`, `DataList`, `FormView` controls with inline SQL or direct data binding
- Master Pages (`.master`) and Content Pages defining layout inheritance

### Configuration

- `Web.config` with `<system.web>`, `<httpRuntime>`, `<compilation>`, `<authentication>`, and `<sessionState>` sections
- `connectionStrings` block (credentials must not be reproduced in documentation)
- Web.config transforms (`Web.Debug.config`, `Web.Release.config`)
- `Global.asax` (`Application_Start`, `Application_Error`, `Session_Start`) for application lifecycle hooks
- HTTP Modules (`IHttpModule`) and HTTP Handlers (`IHttpHandler`, `.ashx`) for cross-cutting concerns

### Security and Identity

- `FormsAuthentication` with `.ASPXAUTH` cookie
- `Membership` and `Roles` providers (SqlMembershipProvider, etc.)
- `<authorization>` rules in `Web.config`
- `Request.Form` / `Request.QueryString` — high XSS and injection risk if not validated
- `Response.Write` and inline expressions (`<%= %>`) — watch for XSS

### State Management

- `Session` (InProc, SqlServer, StateServer) — serialization and sticky-session requirements
- `Application` state (global shared mutable state)
- `Cache` (System.Web.Caching.Cache) — different API from `IMemoryCache`
- `ViewState` per-control enabled/disabled flags

### Bundling and Static Assets

- `ScriptManager` managing script registration order
- `BundleConfig.cs` (if System.Web.Optimization is used)
- Theme folders (`App_Themes/`) and CSS control adapters

## Migration Targets

| From                       | To                                                | Key Concerns                                                          |
| -------------------------- | ------------------------------------------------- | --------------------------------------------------------------------- |
| Web Forms pages            | ASP.NET Core MVC controllers + Razor views        | Eliminate postback lifecycle; map code-behind logic to actions        |
| Web Forms pages            | Blazor Server or Blazor WebAssembly               | Closest event-model analogy; component state replaces ViewState       |
| HTTP Modules               | ASP.NET Core Middleware                           | `IHttpModule` → `IMiddleware`; order matters                          |
| HTTP Handlers (.ashx)      | ASP.NET Core Minimal API endpoints or controllers | Direct HTTP response handling                                         |
| FormsAuthentication        | ASP.NET Core Cookie Authentication + Identity     | Cookie name, sliding expiration, and claim mapping                    |
| Membership / Roles         | ASP.NET Core Identity                             | Schema migration required; password hash algorithm change             |
| SqlDataSource / inline SQL | Repository pattern + Dapper or EF Core            | Extract to data layer before UI migration                             |
| Web.config                 | appsettings.json + environment variables          | Section-by-section mapping; secrets to Secret Manager or Key Vault    |
| Global.asax                | Program.cs / Startup.cs                           | Map Application_Start to `WebApplication.CreateBuilder` configuration |
| ScriptManager bundles      | Webpack / Vite / CDN                              | Decouple from server-side rendering pipeline                          |
| System.Web.Caching.Cache   | IMemoryCache / IDistributedCache                  | API not compatible; requires rewrite                                  |

## Recommended Refactoring Phases

Use these as a starting point; adjust based on observed evidence in the target repository.

| Phase                       | Goal                                     | Typical Work Items                                                                                                      | Gating Criteria                                        |
| --------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| 0 — Baseline                | Establish safety net and inventory       | Add integration/smoke tests; document page inventory; capture ViewState sizes; audit `Request.Form` usage               | Test suite exists and passes on current codebase       |
| 1 — Extract Logic           | Separate business logic from UI          | Move code-behind business logic to service classes; replace SqlDataSource with repository classes; eliminate inline SQL | Services testable independently of Web Forms runtime   |
| 2 — Decouple Infrastructure | Replace Web.config providers             | Migrate connection strings to environment config; replace FormsAuthentication; replace Membership/Roles                 | Application still builds and runs under .NET Framework |
| 3 — Isolate State           | Reduce ViewState and Session coupling    | Disable ViewState on non-essential controls; externalize Session to Redis/SQL; eliminate Application state              | No behavioral regression on stateful pages             |
| 4 — Side-by-Side Migration  | Introduce new framework alongside legacy | Add ASP.NET Core project; route new features to new stack; proxy or share session; run both stacks in same IIS site     | New framework handles at least one end-to-end flow     |
| 5 — Page-by-Page Migration  | Migrate pages incrementally              | Prioritize low-coupling pages first; migrate Master Pages last; maintain URL parity                                     | Each migrated page covered by acceptance test          |
| 6 — Decommission            | Remove Web Forms surface                 | Delete .aspx files, code-behind, Global.asax, HTTP modules; remove System.Web references                                | All traffic handled by new framework                   |

## Risk Inventory — Common Web Forms Blockers

| Risk                                     | Likelihood | Impact   | Mitigation                                                                     |
| ---------------------------------------- | ---------- | -------- | ------------------------------------------------------------------------------ |
| ViewState-dependent business logic       | High       | High     | Audit `ViewState` reads in Page_Load; extract state to service layer           |
| Session serialization incompatibility    | Medium     | High     | Audit session object types before switching providers                          |
| ScriptManager script ordering dependency | Medium     | Medium   | Inventory `RegisterClientScriptBlock` calls; replace with module bundler       |
| FormsAuthentication ticket format change | High       | High     | Plan a coordinated cutover; do not mix auth stacks per-request                 |
| `System.Web` types in shared libraries   | High       | High     | Identify shared assemblies referencing `System.Web`; decouple before migration |
| InProc session on web farm               | Medium     | High     | Move to distributed session before horizontal scaling                          |
| Inline SQL in code-behind or markup      | High       | Critical | Extract and parameterize before migration; audit for injection risk            |
| `Response.Write` / `<%= %>` XSS          | Medium     | High     | Encode all output; replace with Razor or component rendering                   |

## Safety Rules

- This skill is used during documentation-phase work. Do not modify source code, tests, `Web.config`, database scripts, or application configuration.
- Never reproduce connection strings, passwords, API keys, or secrets found in `Web.config` or code files. Describe the type of credential, its location, and its owner only.
- If a security finding (e.g., unparameterized SQL, `Response.Write` XSS) is discovered, record it as a finding in `03-Technical-Debt-and-Risks.md` or `15-Security-Remediation-Checklist.md`. Do not patch it during a documentation task.

## Output Expectations

- A phased refactoring plan in `04-Refactoring-Plan.md` with phases, prerequisites, work items, and exit criteria per phase.
- A risk table populated from evidence observed in the repository.
- Cross-links to `03-Technical-Debt-and-Risks.md`, `09-External-Integrations.md`, and `13-Configuration-Reference.md` where those documents contain supporting evidence.
- All migration sequencing diagrams written in Mermaid.
