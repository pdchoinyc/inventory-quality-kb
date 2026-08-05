# Inventory and WMS Synchronization

## Purpose

This diagram shows how physical warehouse stock updates reach customer-facing inventory systems.

```mermaid
flowchart TD
    WMS[Warehouse Management System]
    Event[Stock Update Event]
    Sync[Inventory Synchronization]
    Inventory[Inventory Service]
    DB[(Inventory Database)]
    Cache[(Inventory Cache)]
    CustomerUI[Customer-Facing Services]
    Alert[Monitoring and Alerting]

    WMS -->|Publish stock update| Event
    Event --> Sync
    Sync --> Inventory
    Inventory --> DB
    Inventory --> Cache
    Inventory --> CustomerUI

    Event -->|Delay or failure| Alert
    Sync -->|Retry failure| Alert
    Inventory -->|Mismatch detected| Alert
```

## QA Focus

- Measure synchronization latency.
- Verify duplicate events do not update stock multiple times.
- Validate retry and recovery behavior.
- Confirm database, cache, and UI converge to the same state.
- Ensure delays and mismatches trigger monitoring alerts.