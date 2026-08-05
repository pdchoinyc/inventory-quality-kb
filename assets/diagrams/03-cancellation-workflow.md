# Order Cancellation and Inventory Restoration

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