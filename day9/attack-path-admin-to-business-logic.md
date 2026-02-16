## Chained Attack Path: Authorization Bypass to Business Logic Abuse

### Step 1: Authorization Bypass
A normal authenticated user can access admin-only endpoints such as `/rest/admin/application-configuration` and `/rest/admin/application-version` by removing cache headers. This exposes internal configuration and hidden functionality.

### Step 2: Reconnaissance via Excessive Data Exposure
The exposed admin endpoints reveal internal feature flags, OAuth configuration, hidden routes, and application behavior, significantly reducing attack complexity.

### Step 3: Business Logic Abuse
Using the gained understanding of application workflows, the attacker exploits insufficient server-side validation on basket item quantities, allowing negative values and price manipulation.

### Impact
- Unauthorized access to administrative configuration
- Expanded attack surface through internal knowledge
- Financial impact via logic abuse
- Increased risk of further chained exploitation

### Severity
High (due to combined impact)

### Key Lesson
Seemingly low or medium issues can escalate into high-impact vulnerabilities when chained together.
