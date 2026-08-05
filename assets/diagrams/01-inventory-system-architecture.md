# Inventory System Architecture

## Purpose

This diagram shows the major systems that read, reserve, update, and synchronize inventory across the customer purchase journey.

```mermaid
flowchart LR
    Customer[Customer]
    App[Mobile App]

    Search[Search Service]
    PDP[Product Detail Service]
    Cart[Cart Service]
    Checkout[Checkout Service]
    Payment[Payment Service]
    Order[Order Service]

    Inventory[Inventory Service]
    Reservation[Inventory Reservation]
    Cache[(Inventory Cache)]
    DB[(Inventory Database)]

    WMS[Warehouse Management System]
    Fulfillment[Fulfillment Service]
    Delivery[Delivery Service]
    Monitoring[Monitoring and Alerting]

    Customer --> App

    App --> Search
    App --> PDP
    App --> Cart
    App --> Checkout

    Search -->|Availability| Inventory
    PDP -->|Stock status| Inventory
    Cart -->|Quantity validation| Inventory
    Checkout -->|Reservation request| Reservation

    Reservation --> Inventory
    Checkout --> Payment
    Payment --> Order
    Order -->|Confirm deduction| Inventory

    Inventory --> Cache
    Inventory --> DB
    Inventory <--> WMS

    Order --> WMS
    WMS --> Fulfillment
    Fulfillment --> Delivery

    Inventory --> Monitoring
    Reservation --> Monitoring
    Order --> Monitoring
    WMS --> Monitoring
```

## QA Focus

- Validate inventory consistency across Search, PDP, Cart, Checkout, and Order.
- Verify cache and database synchronization.
- Confirm that WMS updates propagate to customer-facing systems.
- Monitor failures, latency, and inventory mismatches.