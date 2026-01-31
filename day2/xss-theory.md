# Day 02 – XSS Theory (Context-Based Understanding)

## What is XSS?
Cross-Site Scripting (XSS) occurs when untrusted data is rendered in an executable context in the browser without proper encoding.

XSS is not only an input validation issue, but primarily an output context issue.

---

## Types of XSS

### Reflected XSS
- Input is sent in the request
- Reflected immediately in the response
- Example: search queries reflected in HTML

### Stored XSS
- Malicious input is stored in the database
- Rendered later to other users
- Example: product reviews, descriptions

---

## Why JSON Responses Are Not Immediate XSS
- JSON is a data format, not executable HTML
- Browser does not execute JSON by itself
- XSS depends on how frontend renders the data

---

## innerHTML vs textContent

- `innerHTML` parses and executes HTML
- `textContent` treats input as plain text

Using `innerHTML` with untrusted data leads to XSS.

---

## Key Takeaway
XSS prevention requires:
- Safe output rendering
- Context-aware encoding
- Avoiding dangerous DOM sinks
