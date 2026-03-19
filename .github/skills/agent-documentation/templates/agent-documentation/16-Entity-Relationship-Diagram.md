# {{APPLICATION_NAME}} - Entity Relationship Diagram

> **Owner Role:** Business Analyst
> **Date:** {{DATE}}
> **Status:** {{STATUS}}

## Diagram Scope

Describe which schemas, entities, or bounded contexts are represented.

## Relationship Notes

| Entity | Related Entity | Relationship | Notes |
|--------|----------------|--------------|-------|
| {{ENTITY}} | {{RELATED_ENTITY}} | {{RELATIONSHIP}} | {{NOTES}} |

## Diagram Placeholder

Add a Mermaid ER diagram here.

```mermaid
erDiagram
	ENTITY_ONE ||--o{ ENTITY_TWO : relates_to
	ENTITY_ONE {
		string id
	}
	ENTITY_TWO {
		string entityOneId
	}
```
