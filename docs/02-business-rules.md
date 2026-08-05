# **BR-01. Only Available Products Can Be Purchased**

Customers should only be able to purchase products that have available inventory.

### Business Impact

- Prevents overselling
- Reduces order cancellations
- Protects customer trust

---

# **BR-02. Inventory Must Be Consistent Across All Services**

Inventory information should remain consistent across:

- Search
- Product Detail Page (PDP)
- Cart
- Checkout
- Order

Customers should never observe conflicting inventory information during their purchase journey.

### Quality Risk

Example

PDP
In Stock

↓

Checkout
Out of Stock

---

# **BR-03. Inventory Must Be Reserved During Purchase**

When a customer starts the purchase process, inventory should be reserved according to the business policy.

Reservation prevents multiple customers from purchasing the same item simultaneously.

### Quality Risk

Multiple successful purchases for the last available product.

---

# **BR-04. Inventory Must Be Updated Immediately After Order Completion**

Once an order is successfully created, inventory should be updated without unnecessary delay.

### Expected Result

Inventory

10

↓

Customer purchases 1

↓

Inventory

9

---

# **BR-05. Failed Orders Must Restore Inventory**

If payment fails or the order is cancelled before completion, inventory should be restored.

### Business Impact

Failure to restore inventory may lead to false out-of-stock situations.

---

# **BR-06. Inventory Should Never Become Negative**

Inventory quantity must never become negative.

### Example

Inventory

0

↓

Purchase

×

Reject Order

---

# **BR-07. Concurrent Purchases Must Be Handled Safely**

When multiple customers purchase the last remaining product simultaneously,

only one order should succeed.

### Expected Result

Customer A

Success

Customer B

Out of Stock
