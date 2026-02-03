📘 Day 6 — Business Logic & Workflow Abuse

Path

day6/business-logic-negative-quantity.md

🎯 Objective

Move from endpoint testing to workflow and logic testing, focusing on:

Trust assumptions

State handling

Input boundaries

Financial impact

🧰 Environment & Tools

OWASP Juice Shop

Burp Suite (Proxy, Repeater)

Authenticated user session

🔴 Vulnerability Identified: Business Logic Flaw
Endpoint
POST /api/BasketItems

🧪 Tests Performed
Test 1 — Normal Quantity
{"quantity": 1}


Result:
Rejected due to out-of-stock condition

Test 2 — Negative Quantity
{"quantity": -1}


Result:

Item added successfully

Basket total became negative

Test 3 — Larger Negative Quantity
{"quantity": -5}


Result:

Basket total decreased further

No server-side validation triggered

Test 4 — Zero Quantity
{"quantity": 0}


Result:

500 Internal Server Error

Full stack trace exposed

🚨 Issue 1 — Business Logic Flaw (HIGH)
Root Cause

Backend validates stock availability

Does not validate quantity boundaries

Negative values bypass logic checks

Impact

Price manipulation

Potential free purchases / credit abuse

Inventory corruption

Severity

High

🚨 Issue 2 — Internal Error Information Disclosure
Observed Leakage

ORM name (Sequelize)

Database type (SQLite)

Table names

SQL INSERT statements

Stack traces and file paths

Constraint logic

Impact

Reveals internal application structure

Reduces attacker effort

Increases exploitability of other flaws

Severity

Medium (High when chained with logic flaws)

🧠 OWASP Mapping

OWASP Top 10

A04: Insecure Design

A05: Security Misconfiguration

OWASP API Top 10

API4: Unrestricted Resource Consumption

API8: Security Misconfiguration

✅ Final Assessment

This is a real, exploitable business logic vulnerability with financial impact, combined with improper error handling that leaks sensitive internal details.

🔧 Recommendations

Enforce quantity >= 1 at the application layer

Implement centralized error handling

Return generic error messages (no stack traces)

Validate all numeric boundaries before DB operations

🏁 Day 6 Status

Completed successfully.
Identified and documented a high-severity business logic vulnerability.