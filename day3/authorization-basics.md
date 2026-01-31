# Day 03 – Authorization Basics

## Authentication vs Authorization

Authentication answers the question:
- Who is the user?

Authorization answers the question:
- What is the user allowed to do?

A user can be authenticated but still unauthorized to access a specific resource.

---

## What is IDOR?

IDOR (Insecure Direct Object Reference) occurs when:
- An application uses user-controlled identifiers (like IDs)
- Without verifying ownership of the referenced object

Example:
- Authenticated user accesses or modifies another user’s data by changing an ID.

---

## What is BOLA?

BOLA (Broken Object Level Authorization) is the API equivalent of IDOR.

It happens when:
- An API endpoint is accessible to authenticated users
- But does not verify whether the user is authorized to access the specific object

---

## Why Authentication Is Not Enough

Having a valid JWT or session only proves identity.

Authorization requires:
- Ownership checks
- Permission checks
- Role-based or object-based validation

Without these checks, IDOR/BOLA vulnerabilities occur.

---

## Key AppSec Takeaway

Attaching a user ID to a request does not enforce authorization.

Authorization must explicitly verify:
- The requested object belongs to the authenticated user
- Or the user has permission to access it


for example :

export const appendUserId = () => {
  return (req: Request, res: Response, next: NextFunction) => {
    try {
      req.body.UserId = authenticatedUsers.tokenMap[utils.jwtFrom(req)].data.id
      next()
    } catch (error: any) {
      res.status(401).json({ status: 'error', message: error })
    }
  }
}


in this the uderid is looked into the tokenmap that is from jwt token and no backend verfication is done for what level of authorization that id has so yeaa its 


