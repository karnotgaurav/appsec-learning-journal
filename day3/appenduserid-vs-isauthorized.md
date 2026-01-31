# Day 03 – appendUserId vs isAuthorized

## Purpose
To understand the difference between identity attachment and authorization enforcement in backend code.

---

## appendUserId()

### What it does
- Extracts JWT from the request
- Maps the token to a user in server-side memory
- Attaches the user ID to `req.body.UserId`
- Calls `next()` if token exists

### What it does NOT do
- Does not check permissions
- Does not verify object ownership
- Does not block authenticated users

### Security role
- Identity
