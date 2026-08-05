# Business Rules

Business rules define the expected behavior of the Inventory domain.  
All quality activities—including functional testing, API validation, automation, and release readiness—should be designed around these rules rather than implementation details.

---

## **BR-01** Only Available Products Can Be Purchased

Customers should only be able to purchase products that have available inventory. Products that are out of stock must not proceed to order placement.

**Why it matters**

Allowing customers to purchase unavailable products results in overselling, order cancellations, delayed refunds, and loss of customer trust.

**QA Focus**

- Verify stock availability across the entire purchase journey.
- Validate Out-of-Stock handling.
- Ensure unavailable products cannot be ordered.

---

## **BR-02** Inventory Must Be Consistent Across All Customer Touchpoints

Inventory information should remain consistent across all customer-facing services, including Search, Product Detail Page (PDP), Cart, Checkout, and Order.

**Why it matters**

Customers should never experience conflicting inventory information during a single purchase journey.

Example:

```
PDP
In Stock

↓

Checkout
Out of Stock
```

**QA Focus**

- Validate consistency across multiple services.
- Perform end-to-end verification.
- Verify cache synchronization after inventory updates.

---

## **BR-03** Inventory Must Be Reserved During Checkout

Inventory should be reserved according to the business policy once a customer begins the purchase process.

**Why it matters**

Reservation prevents multiple customers from purchasing the same inventory simultaneously.

**QA Focus**

- Verify reservation timing.
- Validate reservation expiration.
- Test concurrent purchase scenarios.

---

## **BR-04** Inventory Must Be Updated Immediately After Successful Order Creation

Inventory should be deducted immediately after an order is successfully created.

**Why it matters**

Delayed inventory updates may expose inaccurate stock information to other customers, increasing the risk of overselling.

Example:

```
Inventory = 10

↓

Customer purchases 1

↓

Inventory = 9
```

**QA Focus**

- Validate inventory deduction.
- Verify API response consistency.
- Measure inventory synchronization latency.

---

## **BR-05** Failed Orders Must Restore Inventory

If an order fails due to payment failure or cancellation before completion, the reserved inventory should be released.

**Why it matters**

Failure to restore inventory reduces available stock unnecessarily and may create false Out-of-Stock conditions.

**QA Focus**

- Verify inventory restoration after payment failure.
- Validate cancellation scenarios.
- Confirm inventory consistency after rollback.

---

## **BR-06** Inventory Quantity Must Never Become Negative

Inventory should never become less than zero under any circumstances.

**Why it matters**

Negative inventory indicates a critical system integrity issue and usually represents concurrency or synchronization failures.

**QA Focus**

- Validate boundary conditions.
- Perform high-concurrency testing.
- Verify data integrity after repeated transactions.

---

## **BR-07** Concurrent Purchases Must Be Handled Safely

When multiple customers attempt to purchase the last available item simultaneously, only one order should succeed.

Expected Result

```
Customer A

Order Success

↓

Inventory = 0

Customer B

Out of Stock
```

**Why it matters**

Concurrency handling is one of the highest-risk scenarios in inventory management. Failure may lead to overselling, customer complaints, and operational issues.

**QA Focus**

- Perform concurrent transaction testing.
- Verify order uniqueness.
- Validate inventory synchronization across services.

---

# Summary

These business rules establish the quality baseline for the Inventory domain.

Every test strategy, automation scenario, production monitoring activity, and release readiness checklist should trace back to one or more of these business rules.
