# Purchase and Inventory Workflow

## Purpose

This sequence shows how inventory is validated, reserved, deducted, or restored during checkout.

```mermaid
sequenceDiagram
    participant Customer
    participant App
    participant Checkout
    participant Inventory
    participant Reservation
    participant Payment
    participant Order

    Customer->>App: Start checkout
    App->>Checkout: Submit product and quantity
    Checkout->>Inventory: Validate stock
    Inventory-->>Checkout: Stock available
    Checkout->>Reservation: Reserve inventory

    alt Reservation succeeds
        Reservation-->>Checkout: Reservation ID
        Checkout->>Payment: Process payment

        alt Payment succeeds
            Payment-->>Checkout: Payment success
            Checkout->>Order: Create order
            Order->>Inventory: Confirm deduction
            Inventory-->>Order: Inventory updated
            Order-->>App: Order confirmed
        else Payment fails
            Payment-->>Checkout: Payment failure
            Checkout->>Reservation: Release reservation
            Reservation-->>Checkout: Inventory restored
            Checkout-->>App: Payment failed
        end
    else Reservation fails
        Reservation-->>Checkout: Out of stock
        Checkout-->>App: Purchase unavailable
    end
```

## QA Focus

- Revalidate inventory before payment.
- Confirm that reservation happens only once.
- Verify inventory restoration after payment failure.
- Ensure successful orders deduct inventory exactly once.
- Validate safe behavior for duplicate requests.