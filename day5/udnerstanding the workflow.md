📘 Day 5 — API Security Fundamentals (Burp + Authorization)

Path

day5/api-security-fundamentals.md

🎯 Objective

Learn how to correctly test APIs for:

IDOR / BOLA

Mass Assignment

Excessive Data Exposure

While avoiding false positives and understanding when an endpoint is secure by design.

🧰 Environment & Tools

OWASP Juice Shop (Docker)

Burp Suite (Proxy, Repeater)

Authenticated user session (JWT)

🔹 Methodology Followed

For every endpoint tested, the following process was used:

Establish a baseline request

Modify one variable at a time

Observe behavioral changes, not just status codes

Validate findings with ownership and authorization logic

Classify as:

Safe

Informational

Vulnerable

🔍 IDOR / BOLA Testing
Endpoint Tested
GET /api/Addresss/:id

Test Performed

Accessed owned address ID

Modified :id to other values

Used same JWT token

Observed Behavior

Owned ID → 200 OK

Non-owned / invalid IDs → 400 Bad Request

Conclusion

✅ Object-level authorization enforced
❌ No IDOR / BOLA vulnerability

🔍 Mass Assignment Testing
Endpoint Tested
POST /api/BasketItems

Test Performed

Added extra JSON fields to request body

Observed backend handling

Observed Behavior

Requests with unexpected fields failed

No silent acceptance or storage of extra fields

Conclusion

✅ No mass assignment vulnerability
ℹ️ 200 OK alone is not an indicator of mass assignment

🔍 Excessive Data Exposure Testing
Endpoint Tested
GET /rest/user/whoami

Observed Behavior
{"user":{}}


No sensitive fields exposed

No internal metadata leaked

Conclusion

✅ Secure endpoint
❌ No excessive data exposure

Minor Observation

Some endpoints returned internal identifiers (e.g., UserId) where not strictly required.

Severity: Informational
Impact: Low (useful only for attacker recon)

🧠 Key Learnings (Day 5)

200 OK ≠ vulnerability

Authenticated ≠ authorized

IDOR requires cross-user access, not just ID manipulation

Secure endpoints exist and must be identified correctly

Avoiding false positives is a core AppSec skill

✅ Day 5 Status

Completed successfully.
All tested endpoints behaved securely.