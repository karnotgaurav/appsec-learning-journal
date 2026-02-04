📝 GitHub-Ready Writeup (Day 8A)

Save as:

day8/excessive-data-exposure-user-creation.md

## Excessive Data Exposure in User Creation API

**Endpoint**
POST /api/Users

**Issue**
The user creation endpoint returns internal and unnecessary fields in the response, including role assignment, account status flags, internal timestamps, last login metadata, and exact profile image storage paths.

**Exposed Fields**
- role
- profileImage (internal storage path)
- lastLoginIp
- isActive
- deletedAt

**Impact**
Although not directly exploitable, this information disclosure aids attacker reconnaissance, reveals internal authorization models and storage structures, and increases the attack surface for chained vulnerabilities.

**Severity**
Low to Medium

**Recommendation**
Limit API responses to only fields required by the client. Internal fields and metadata should not be exposed.