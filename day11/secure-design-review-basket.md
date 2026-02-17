## Feature: Add Product to Basket

### Trust Boundaries
- Client → API
- JWT → User identity
- Basket ownership
- Quantity validation

### Predicted Risks
- Negative quantity manipulation
- Out-of-stock bypass
- DB constraint information leak
- IDOR via BasketId manipulation

### Secure Design Requirements
- Server-side numeric validation
- Ownership enforcement
- Transactional DB updates
- Generic error handling


things to understand what type of question should we ask during kt session ?

1.ask design question like what is the flow 
user ->api->middleware-->db-->response 

who can acess this endpoint
what type of data does it expose
is it read-only
any secret it has
should it ever be public 
is role enforecement requireed
what happens if chahing bupasses role checks 
it measn that once a admin logged in so the cahce was not cleared it got stored that is why this happend and a simple user can see the data that should only be visible to the admin 
🚨 Where It Becomes Dangerous

Imagine this scenario:

1️⃣ Admin logs in
2️⃣ Admin requests /rest/admin/application-configuration
3️⃣ Server returns full config + ETag
4️⃣ Browser caches it

Now:

5️⃣ Admin logs out
6️⃣ Normal user logs in
7️⃣ Browser sends If-None-Match
8️⃣ Server replies 304 Not Modified

Now the browser may display the previously cached admin data.

⚠️ Role check was never re-evaluated properly.

That’s what:

“Caching bypasses role checks”

means.

we should keep cache-control as private or no store 
