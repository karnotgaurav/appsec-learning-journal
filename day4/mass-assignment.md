📄 Day-04/mass-assignment.md
# Day 04 – Mass Assignment

## What is Mass Assignment?

Mass assignment occurs when a backend API blindly trusts client-supplied JSON
and writes it directly to the database without filtering or whitelisting fields.

This allows attackers to modify sensitive fields that should be controlled
only by the server.

---

## Why Authentication Does Not Prevent It

- Authentication proves identity
- Authorization controls endpoint access
- Mass assignment abuses backend trust in request data

Even authenticated and authorized users can exploit this flaw.

---

## Vulnerable Pattern

```ts
Model.create(req.body)
Model.update(req.body)


The backend accepts all fields sent by the client.

Example Attack

Expected input:

{
  "email": "user@test.com",
  "password": "password123"
}


Attacker sends:

{
  "email": "user@test.com",
  "password": "password123",
  "role": "admin",
  "isAdmin": true
}


If not filtered, privilege escalation occurs.

Secure Pattern

Explicit field selection:

Model.create({
  email: req.body.email,
  password: hash(req.body.password)
})


Or whitelisting allowed fields.

AppSec Takeaway

Clients must never control sensitive backend fields.
All writable fields must be explicitly defined by the server.