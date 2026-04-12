interview defination of when does idor happens?
idor happens when a user can access or moddify an object they do not own because the application does not enforce object level authorization 

two types of access cotrol faliures are 
1.horizontal same level 
2.vertical normal to admin

what does idor mean it does not mean just to change id it can be 
Body parameter (userId)
JSON field
Header value
Nested object ID
Query parameter
Hidden form field
State machine manipulation


how to know if there is idor in code 
we should look for things such as 
req.params.id
req.query.userId
req.body.accountId
req.body.orderId

we need to ask question such as 
is identity extracted from jwt
ownership enforced in db
role check is needed or not 
is object fi;tred by both id and owner
is there fallbacl logic 

## Advanced IDOR Patterns

1. Indirect Object References (tokens, filenames)
2. Nested Object IDOR
3. IDOR via Request Body
4. State-Based IDOR
5. File Path Enumeration
6. Soft-Delete Bypass

### Core Principle
Any client-controlled object reference must be validated against authenticated identity.
