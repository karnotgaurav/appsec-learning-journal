day8/systemic-admin-authorization-failure.md

## Systemic Authorization Failure on Admin Endpoints (Cache-Aware)

### Affected Endpoints
- GET /rest/admin/application-version
- GET /rest/admin/application-configuration

---

### Issue
Admin endpoints do not enforce role-based authorization. Any authenticated user can access sensitive administrative configuration.

---

### Cache Behavior Observed (Important)

Initial requests returned `304 Not Modified` due to ETag-based caching.

The requests included headers such as:
- `If-None-Match`

This caused the server to return cached responses, **masking the actual authorization behavior**.

After removing:
- `If-None-Match`
- `If-Modified-Since`

(or by forcing `Cache-Control: no-cache`)

the server returned fresh responses.

---

### Authorization Result (Without Cache Headers)

- **Status:** `200 OK`
- **User role:** Normal authenticated user (non-admin)
- **Response:** Full admin configuration and internal data

This confirms that **authorization checks are missing**, and cached responses were only hiding the issue.

---

### Impact
- Exposure of internal application configuration
- Disclosure of feature flags, OAuth client configuration, hidden routes, internal metadata, and application behavior
- Increased attack surface and reconnaissance capability
- Vulnerability affects multiple admin endpoints, indicating a **systemic access control failure**

---

### Severity
**High**

---

### OWASP Classification
- **OWASP Top 10:** A01 – Broken Access Control  
- **OWASP API Top 10:** API5 – Broken Function Level Authorization  

---

### Recommendation
- Enforce strict role-based authorization on all `/rest/admin/*` endpoints
- Do not rely on authentication alone
- Ensure authorization checks are evaluated **before** cache decisions
- Avoid serving cached admin responses to unauthorized users

---

### Key Lesson
ETag-based caching can mask authorization vulnerabilities. Authorization testing must always be performed on **non-cached responses** to avoid false negatives.