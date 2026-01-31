# Day 03 – IDOR & BOLA Analysis

## Definitions

### IDOR (Insecure Direct Object Reference)
Occurs when:
- User-controlled identifiers (IDs) are used
- Without verifying ownership of the referenced object

### BOLA (Broken Object Level Authorization)
API-level version of IDOR where:
- Authenticated users can access objects belonging to other users

---

## Common IDOR Pattern

```http
DELETE /api/resource/:id

If backend logic only checks:

where: { id: req.params.id }

Then:

    Any authenticated user can access any object

    Ownership is not enforced