# Order Cancellation and Inventory Restoration

## Purpose

This sequence shows inventory restoration when an eligible order is cancelled before shipment.

```mermaid
sequenceDiagram
    participant Customer
    participant App
    participant Order
    participant WMS
    participant Payment
    participant Inventory

    Customer->>App: Request cancellation
    App->>Order: Cancel order
    Order->>WMS: Check fulfillment state
    WMS-->>Order: Not shipped
    Order->>Payment: Request refund
    Payment-->>Order: Refund confirmed
    Order->>Inventory: Restore inventory
    Inventory-->>Order: Inventory updated
    Order-->>App: Cancellation completed
```

## QA Focus

- Verify cancellation eligibility by order state.
- Confirm inventory is restored only after the required business conditions are met.
- Prevent duplicate inventory restoration.
- Validate consistency among cancellation, refund, and inventory states.