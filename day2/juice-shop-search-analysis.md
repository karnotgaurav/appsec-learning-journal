
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