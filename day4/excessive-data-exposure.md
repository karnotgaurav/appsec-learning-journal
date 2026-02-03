---

## 📄 `Day-04/excessive-data-exposure.md`

```md
# Day 04 – Excessive Data Exposure

## What is Excessive Data Exposure?

Excessive data exposure happens when APIs return more data than the client
actually needs, including internal or sensitive fields.

This can occur even when:
- The user is authenticated
- The user is authorized
- The data belongs to the user

---

## Vulnerable Pattern

```ts
res.json(user)

Returning full database objects directly to the client.
Example Vulnerable Response

{
  "id": 12,
  "email": "user@test.com",
  "password": "$2b$10$hash...",
  "role": "user",
  "isAdmin": false,
  "failedLoginAttempts": 2
}

Why This Is Dangerous

    Password hashes aid offline attacks

    Role fields help privilege escalation

    Internal fields expose security logic

    Enables chaining with mass assignment

Even if impact is low, it is still information disclosure.
Secure Pattern

Return only required fields:

{
  "email": "user@test.com",
  "createdAt": "2023-01-01"
}

AppSec Takeaway

APIs must follow data minimization.
Return only what the client strictly needs.