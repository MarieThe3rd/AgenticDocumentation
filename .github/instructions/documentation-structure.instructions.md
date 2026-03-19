---
description: Use when creating or maintaining a numbered application documentation catalog in Documentation, docs, or a similarly named folder.
applyTo: "**/{Documentation,docs}/**/*.md"
---

# Documentation Catalog Structure

Follow these rules when working on a numbered application documentation set:

1. Preserve file numbering once the catalog exists.
2. Keep one primary subject per file.
3. Update the catalog README whenever the set changes.
4. Use cross-links between related documents when they improve navigation.
5. Prefer stable headings and repeated section patterns so catalogs are comparable across repositories.
6. Distinguish among facts, assumptions, known issues, and recommendations.
7. If a document is not applicable, say why at the top instead of leaving a blank file.
8. Documentation tasks must not change application code or runtime configuration.
9. Documentation may update only documentation assets unless the user explicitly expands scope.
10. Sensitive values must be redacted or omitted from all documentation outputs.

Recommended file order:

- `README.md`
- `00-Architecture-Overview.md`
- `01-19` domain-specific documents
- `20-Session-Log.md`
