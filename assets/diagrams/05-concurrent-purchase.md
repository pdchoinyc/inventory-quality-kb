# Concurrent Purchase of the Last Item

## Purpose

This sequence represents two customers attempting to purchase the final available unit.

```mermaid
sequenceDiagram
    participant UserA as Customer A
    participant UserB as Customer B
    participant Inventory
    participant OrderA as Order Service A
    participant OrderB as Order Service B

    UserA->>Inventory: Reserve last item
    UserB->>Inventory: Reserve last item

    Inventory-->>UserA: Reservation successful
    Inventory-->>UserB: Out of stock

    UserA->>OrderA: Create order
    OrderA->>Inventory: Confirm deduction
    Inventory-->>OrderA: Inventory = 0

    UserB->>OrderB: Attempt order
    OrderB-->>UserB: Order rejected
```

## Expected Result

- Only one reservation succeeds.
- Only one order is created.
- Final inventory is zero.
- No duplicate payment or deduction occurs.
- The unsuccessful customer receives a clear out-of-stock response.

## QA Focus

- Execute concurrent requests against the same stock item.
- Validate order, payment, reservation, and inventory records together.
- Confirm inventory never becomes negative.
- Repeat the test under higher load to identify race conditions.