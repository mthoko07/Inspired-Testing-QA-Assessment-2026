# Part A — Automation Readiness & Judgement

Let’s start with **Step 1: Test Cases**

---
 TC001 — Successful purchase (happy path)

**Title:** User completes a successful product purchase
**Preconditions:**

* User has a valid account
* User is logged out at start
* Product is in stock
* Cart is empty before execution

**Steps:**

1. Navigate to login page
2. Enter valid username and password
3. Click “Login”
4. Search/select a product
5. Click “Add to Cart”
6. Open cart
7. Click “Checkout”
8. Enter valid delivery and payment details
9. Confirm order

**Expected Result:**

* Order is successfully placed
* Confirmation message is displayed
* Order number is generated and visible
* Cart is cleared after purchase

**Priority:** High

---

TC002 — Checkout with invalid payment details (negative case)

**Title:** User cannot complete purchase with invalid payment info
**Preconditions:**

* User is logged in
* Product is already in cart

**Steps:**

1. Go to checkout
2. Enter invalid card number / expired date
3. Attempt to place order

**Expected Result:**

* Payment is rejected
* Clear error message is displayed
* Order is not created
* User remains on checkout page

**Priority:** High

---

TC003 — Add to cart updates cart count correctly

**Title:** Cart badge updates after adding product
**Preconditions:**

* User is logged in

**Steps:**

1. Open product page
2. Click “Add to Cart”

**Expected Result:**

* Cart icon shows correct item count (e.g. +1)
* Item appears in cart

**Priority:** Medium


---


**1. "What questions would you ask before starting automation?"**
- *Journey clarity:* "Is the purchase journey identical for every product, or do some items (e.g. out-of-stock) branch differently?"
- *Test data/accounts:* "Can we get dedicated test accounts instead of the shared logins that keep getting locked?"
- *Environment stability:* "Since other teams test on the same environment, is there a way to isolate or reset state before each run?"
- *Acceptance criteria:* "What does 'pass' look like — order confirmation text? A specific order number format?"
- *Release visibility:* "Can the schedule/automation get notified on deploy, even without a formal release note?"

**2. "Is this journey ready for reliable scheduled automation?"**
- Verdict: "Not yet, but close."
- Evidence: shared logins get locked, shared environment causes unpredictable state (pre-filled carts, duplicate orders), UI elements shift.
- Flip condition: "Ready once we have dedicated accounts and a way to isolate/reset test data."

3. Top risks and minimum controls

Risk | Minimum control 

| Shared logins get locked | Dedicated test accounts |
| Shared env causes flaky state | Data reset/isolation before each run |
| UI shifts break locators | Stable selectors (e.g. data-testid, not CSS position) |
| Inconsistent release notes | Smoke-test gate after each deploy + alert on failure |

**4. "Week one: automate first vs. deliberately not yet"**
## Part B2 — Design & Readiness

1. **Test cases** — ID, title, preconditions, steps, expected result, priority. Include the happy path + at least one negative case 
2. **Pseudocode/flow** —  Login → AssertLoggedIn → AddToCart → AssertCartCount → Checkout → EnterDetails → AssertOrderSummary → Finish → AssertConfirmation.
3. **Test data requirements** — dedicated non-shared accounts, known stable product set, one valid + one invalid checkout dataset.
4. **Preconditions/cleanup** — cart must be empty before each run; account not locked; reset/clear state after.
5. **Assertions** — make them specific and observable (cart badge count, confirmation message text, order number present) — not just "page loads."
6. **Now vs later** — now: happy path + one negative case; later: edge cases, cosmetic UI variance, less critical alternate flows.
7. **Review checklist** — independent test data, re-runnable without manual reset, no hard-coded waits, resilient selectors, clear run instructions.

Want to try drafting your actual test cases for step 1, and I'll give feedback on them?
