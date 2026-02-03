Excellent request.
Below is a **real-world, AppSec-engineer-grade list of business logic flaws** — not textbook, not theoretical — these are **exactly the places teams forget to check**.

I’ll group them by **industry**, explain **what goes wrong**, and **why it’s missed**.

---

# 🔴 REAL-LIFE BUSINESS LOGIC FLAW SCENARIOS

*(Where Auth, Validation & Scanners All Pass)*

---

## 🛒 E-COMMERCE / MARKETPLACES

### 1️⃣ Coupon / Promo Code Reuse

**What goes wrong**

* Coupon meant for one-time use
* Applied multiple times by:

  * Replaying requests
  * Applying after cart update
  * Applying across multiple orders

**Why it’s missed**

* Coupon validation happens client-side
* Backend doesn’t track redemption state properly

**Impact**

* Financial loss
* Unlimited discounts

---

### 2️⃣ Price Manipulation After Checkout

**What goes wrong**

* User adds item
* Price calculated
* User modifies quantity/price via API before payment

**Why it’s missed**

* Backend trusts client-calculated totals
* Re-calculation not enforced server-side

**Impact**

* Free or underpriced orders

---

### 3️⃣ Skipping Payment Step

**What goes wrong**

* Checkout API called directly
* Payment verification not enforced
* Order marked as paid

**Why it’s missed**

* Workflow assumed, not enforced

**Impact**

* Free purchases

---

### 4️⃣ Refund Abuse

**What goes wrong**

* User requests refund multiple times
* Refund issued without checking refund history

**Why it’s missed**

* Missing state validation

**Impact**

* Double refunds

---

## 🏦 FINTECH / BANKING

### 5️⃣ Transfer Limit Bypass

**What goes wrong**

* Daily transfer limit enforced per transaction
* User splits transfers into multiple rapid calls

**Why it’s missed**

* Limit not tracked cumulatively
* Race conditions ignored

**Impact**

* Fraud, money laundering

---

### 6️⃣ Currency Conversion Abuse

**What goes wrong**

* Backend trusts exchange rates from client
* User submits manipulated conversion values

**Why it’s missed**

* Assumption that UI is trusted

**Impact**

* Financial exploitation

---

### 7️⃣ Negative Balance Creation

**What goes wrong**

* Withdraw allowed before balance update
* Multiple concurrent withdrawals

**Why it’s missed**

* No transactional locking
* Race conditions not considered

**Impact**

* Financial loss

---

## 🎟️ BOOKINGS / TICKETING / EVENTS

### 8️⃣ Seat Reservation Abuse

**What goes wrong**

* Seats reserved but not paid
* Reservation never expires
* Inventory locked

**Why it’s missed**

* Timeout logic missing
* Cleanup not enforced

**Impact**

* Denial of service to real users

---

### 9️⃣ Ticket Type Downgrade

**What goes wrong**

* VIP ticket added
* Ticket type changed via API before confirmation

**Why it’s missed**

* Backend trusts client-sent ticket category

**Impact**

* Revenue loss

---

## 📱 SUBSCRIPTIONS / SAAS

### 🔟 Trial Reset Abuse

**What goes wrong**

* User resets trial via:

  * Account deletion
  * Email change
  * Re-registration

**Why it’s missed**

* Trial logic tied to user ID only

**Impact**

* Revenue loss

---

### 1️⃣1️⃣ Plan Upgrade Without Payment

**What goes wrong**

* Subscription tier changed
* Payment verification missing

**Why it’s missed**

* Backend assumes frontend flow

**Impact**

* Free premium access

---

## 🏢 ENTERPRISE / INTERNAL APPS

### 1️⃣2️⃣ Approval Workflow Bypass

**What goes wrong**

* User directly calls “approve” API
* No role/state validation

**Why it’s missed**

* UI hides button, backend trusts UI

**Impact**

* Unauthorized approvals

---

### 1️⃣3️⃣ Status Manipulation

**What goes wrong**

* User changes request status:

  * `pending → approved`

**Why it’s missed**

* Status field not validated server-side

**Impact**

* Process abuse

---

## 🧾 REPORTING / ANALYTICS

### 1️⃣4️⃣ Time-Range Abuse

**What goes wrong**

* User queries data outside allowed date range

**Why it’s missed**

* No server-side date bounds

**Impact**

* Data exposure, DoS

---

### 1️⃣5️⃣ Pagination Abuse

**What goes wrong**

* Extremely high `limit` values accepted

**Why it’s missed**

* No max enforcement

**Impact**

* Performance degradation

---

## 🔐 AUTH / ACCOUNT MANAGEMENT

### 1️⃣6️⃣ Password Reset Abuse

**What goes wrong**

* Reset tokens reused
* Tokens not invalidated

**Why it’s missed**

* Poor state tracking

**Impact**

* Account takeover

---

### 1️⃣7️⃣ Email Change Without Verification

**What goes wrong**

* Email updated
* No re-verification required

**Why it’s missed**

* Assumed safe flow

**Impact**

* Account hijacking

---

## 🧠 WHY THESE ARE MISSED (VERY IMPORTANT)

These flaws are missed because:

* All inputs are valid
* Auth & authz pass
* Requests look normal
* No payload needed
* Scanners don’t understand *intent*

---

## 🔑 UNIVERSAL BUSINESS LOGIC CHECKLIST

For **every workflow**, ask:

1️⃣ Can steps be skipped?
2️⃣ Can steps be repeated?
3️⃣ Can order be changed?
4️⃣ Are client values trusted?
5️⃣ Is state validated server-side?

If yes → **logic flaw exists**

---

## 🟢 ONE-LINE SUMMARY (LOCK THIS)

> Business logic flaws occur when applications enforce syntax and access controls but fail to enforce intent and state.

---

If you want next, I can:

* Map **these scenarios to Juice Shop challenges**
* Teach you **how to test logic flaws using Burp**
* Give you a **business-logic testing checklist**

Just tell me what you want to do next.
we