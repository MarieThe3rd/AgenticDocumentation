# {{APPLICATION_NAME}} - External Integrations

> **Owner Role:** Legacy Code Analyst
> **Date:** {{DATE}}
> **Status:** {{STATUS}}

## Integration Diagram

```mermaid
flowchart LR
	App[Application] --> Ext1[Integration 1]
	App --> Ext2[Integration 2]
	Ext1 --> Downstream1[Downstream Service]
```

## Integration Inventory

| Integration | Direction | Purpose | Authentication | Failure Mode | Owner |
|-------------|-----------|---------|----------------|--------------|-------|
| {{INTEGRATION}} | {{DIRECTION}} | {{PURPOSE}} | {{AUTH}} | {{FAILURE_MODE}} | {{OWNER}} |

## Operational Notes

- {{INTEGRATION_NOTE_1}}
