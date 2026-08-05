# Test Scenarios

## Purpose

This document outlines representative test scenarios for validating the Inventory domain.

The scenarios are prioritized based on customer impact and business criticality rather than implementation complexity.

---

# Test Scenario Categories

| Category | Objective |
|----------|-----------|
| Inventory Availability | Validate inventory visibility |
| Inventory Reservation | Validate stock reservation |
| Inventory Update | Validate inventory deduction |
| Inventory Restoration | Validate rollback scenarios |
| Synchronization | Validate consistency across services |
| Concurrency | Prevent overselling |
| Exception Handling | Validate recovery from failures |

---

# TS-01 Product Availability

## Scenario

Customer views a product with available inventory.

### Expected Result

- Product is purchasable
- Inventory status is displayed correctly
- Quantity selection is available

### Priority

🔴 Critical

---

# TS-02 Out-of-Stock Product

## Scenario

Customer opens a product with zero inventory.

### Expected Result

- Purchase is blocked
- Out-of-Stock message is displayed
- Inventory status is consistent across Search, PDP, and Checkout

### Priority

🔴 Critical

---

# TS-03 Successful Purchase

## Scenario

Customer completes checkout successfully.

### Expected Result

- Order is created
- Inventory is deducted
- Updated inventory is reflected across all services

### Priority

🔴 Critical

---

# TS-04 Payment Failure

## Scenario

Payment fails after inventory reservation.

### Expected Result

- Order is not created
- Reserved inventory is released
- Inventory quantity is restored

### Priority

🔴 Critical

---

# TS-05 Order Cancellation

## Scenario

Customer cancels an order before shipment.

### Expected Result

- Order status is updated
- Inventory is restored
- Inventory is available for future purchases

### Priority

🟠 High

---

# TS-06 Concurrent Purchase

## Scenario

Two customers purchase the last available item simultaneously.

### Expected Result

- Only one purchase succeeds
- Inventory becomes zero
- The second customer receives an Out-of-Stock message

### Priority

🔴 Critical

---

# TS-07 Inventory Synchronization

## Scenario

Inventory changes after an order is completed.

### Expected Result

Inventory remains consistent across:

- Search
- PDP
- Cart
- Checkout
- Order
- WMS

### Priority

🔴 Critical

---

# TS-08 Cache Synchronization

## Scenario

Inventory is updated while cached inventory still exists.

### Expected Result

- Updated inventory becomes visible within the expected time
- No stale inventory is displayed during purchase

### Priority

🟠 High

---

# TS-09 WMS Synchronization

## Scenario

Warehouse inventory changes after fulfillment.

### Expected Result

- Inventory Service receives updates
- Customer-facing inventory remains accurate
- Synchronization delay stays within the acceptable threshold

### Priority

🟠 High

---

# TS-10 Boundary Validation

## Scenario

Inventory values reach boundary conditions.

### Test Data

- Inventory = 0
- Inventory = 1
- Inventory = Maximum
- Negative inventory
- Large purchase quantity

### Expected Result

Business rules are enforced correctly.

### Priority

🟡 Medium

---

# TS-11 Inventory API Failure

## Scenario

Inventory Service returns an error or times out.

### Expected Result

- Customer receives an appropriate error message
- Unsafe purchases are prevented
- Errors are logged and monitored

### Priority

🟠 High

---

# TS-12 Regression Scenario

## Scenario

A new inventory feature is deployed.

### Regression Scope

- Search
- PDP
- Cart
- Checkout
- Payment
- Order
- Inventory APIs
- WMS Integration

### Expected Result

Existing inventory functionality continues to operate correctly.

---

# Automation Candidates

The following scenarios should be included in the automated regression suite.

| Scenario | Automation |
|----------|------------|
| Product Availability | ✅ |
| Successful Purchase | ✅ |
| Inventory Deduction | ✅ |
| Payment Failure | ✅ |
| Inventory Restoration | ✅ |
| Inventory API Validation | ✅ |
| End-to-End Purchase | ✅ |

---

# Staff QA Perspective

Test scenarios should reflect real customer journeys rather than isolated system functions.

Priority should be given to scenarios that directly affect customer trust, purchasing success, and business continuity.

Inventory testing is most effective when business rules, API validation, integration testing, and end-to-end customer journeys are validated together.
