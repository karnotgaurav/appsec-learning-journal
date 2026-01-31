Day-02/request-to-code-trace.md
# Day 02 – Request → Code → Response Trace

## Objective
To trace user input from HTTP request through backend code to the response.

---

## Endpoint Traced



GET /rest/products/search?q=<input>


Defined in `server.ts` and implemented in:



routes/search.ts


---

## Input Source

```ts
req.query.q


Fully attacker-controlled

Length limited to 200 characters

Not sanitized or encoded

Backend Processing

Input is assigned to variable criteria

Used directly inside a SQL query

No parameterized queries used

Output Sink
res.json(products)


Response is JSON

No HTML rendering in backend

Security Insight

Backend does not introduce XSS directly

Output context is decided by frontend

Vulnerabilities must be analyzed across layers

Key Learning

Tracing input across layers is essential to identify real vulnerabilities.


---

# 📄 3️⃣ `Day-02/juice-shop-search-analysis.md`

```md
# Day 02 – Juice Shop Search Endpoint Analysis

## File Analyzed


routes/search.ts


---

## Code Snippet (Relevant)

```ts
models.sequelize.query(
  `SELECT * FROM Products 
   WHERE ((name LIKE '%${criteria}%' 
   OR description LIKE '%${criteria}%') 
   AND deletedAt IS NULL)`
)

Primary Vulnerability
SQL Injection

User input is concatenated into SQL query

No prepared statements or parameterization

Attacker can manipulate query logic

Secondary Risk
Stored / Reflected XSS (Frontend Dependent)

Product name and description originate from user input

If frontend renders using innerHTML, XSS can occur

Backend JSON response alone is not dangerous

Responsibility Split
Backend

Input validation

Authentication & authorization

Safe database queries

Frontend

Context-aware output encoding

Avoiding unsafe DOM APIs