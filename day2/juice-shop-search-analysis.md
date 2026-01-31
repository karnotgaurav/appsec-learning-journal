
You can paste this as-is (it reflects exactly what you learned with me).

# Day 02 – Juice Shop Code Research Methodology

## Objective
To learn how to read a real-world Express + TypeScript codebase from an AppSec perspective and identify:
- User input sources
- Authorization gates
- Output sinks
- Security-relevant logic

This document focuses on **how to analyze**, not on a single vulnerability.

---

## Step 1: Identify Routing File

Juice Shop uses `server.ts` as the main routing and middleware wiring file.

Important observation:
- `server.ts` rarely contains final response logic
- It maps endpoints to handler functions defined elsewhere

Example:
```ts
app.get('/rest/products/search', searchProducts())


This means:
➡ The actual logic is in routes/search.ts

Step 2: Follow the Import

To find where responses are generated:

Identify the handler function name

Follow the import statement

Open the corresponding file inside routes/

Example:

import { searchProducts } from './routes/search'


➡ Open routes/search.ts

Step 3: Identify User Input Sources

In route handler files, search for:

req.body
req.query
req.params
req.headers


Rule:

Every accessed property of these objects is attacker-controlled input.

Example:

req.query.q
req.body.email
req.params.id

Step 4: Identify Middleware vs Business Logic

Important distinction:

Code that modifies req and calls next() is middleware

Code that sends res.send / res.json / res.render is output logic

Middleware example:

app.post('/api/Users', (req, res, next) => {
  req.body.email = req.body.email.trim()
  next()
})


This does NOT produce a response.

Step 5: Locate Output Sinks

Search for:

res.send
res.json
res.render
res.redirect


These are security-critical sinks.

If not found immediately:

Scroll to the end of async functions

Look after Promise chains

Step 6: Determine Output Context

Ask:

Is output JSON?

Is output HTML?

Is output rendered in frontend JS?

Key insight:

JSON responses are not executable by themselves

XSS risk depends on frontend rendering (e.g. innerHTML)

Step 7: Separate Primary vs Secondary Vulnerabilities

Example from search endpoint:

Primary: SQL Injection (backend)

Secondary: Stored XSS (frontend-dependent)

Lesson:

Not every vulnerability is visible in one file.

Step 8: Security Controls to Watch For

While reading Juice Shop code, always look for:

security.isAuthorized() → authentication & authorization

security.appendUserId() → identity attachment (not auth)

Input normalization (trim, length checks)

Missing ownership checks (IDOR/BOLA risk)