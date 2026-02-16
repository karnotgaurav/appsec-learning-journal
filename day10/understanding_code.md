javascript basic knowledge
    a.Values
    b.variables
    c.Objects things with properties 
    d.Functions

eg of objects can be
            const user = {
            name: "Ali",
            age: 25
            }

the above object have a property called name and age


5.Accessing a property 
dot syntax we use this when the name is static  
user.name  here means give me the name that is insider user
Bracket syntax we use this when the name is dynamic
user["name]

a.b.c means go inside a then isnide b then get c


export const appendUserId = () => {
  return (req, res, next) => {
    try {
      req.body.UserId =
        authenticatedUsers.tokenMap[utils.jwtFrom(req)].data.id

      next()
    } catch (error) {
      res.status(401).json({ status: 'error' })
    }
  }
}

in this code what i understood is a 
a const is made nameed appenduserid which could be exported means could be called by other functions

and then there is a arrow functions and a middleware 
with return req response and next function 

it tries to set req.body.userId the  current user who are authenticated get into those tokenMap use the function jwtfrom from the req and then go into data and then go into id and get that id 

then we go to next()

catch is like throw an error if something is wrong 


export const isAuthorized = () => expressJwt(({ secret: publicKey }) as any)
this is same it export the isAuthorized const and that include the secret public key 


appendUserId

Trusted input: JWT extracted from request

Why trusted: Cryptographically verified JWT signature

Assumption: Token mapping is correct and immutable; downstream logic relies on server-set UserId

Failure impact: Ownership and authorization checks can be bypassed

isAuthorized

What it does: Verifies JWT authenticity

What it does NOT do: Enforce role or permission checks

Security risk: Endpoints relying only on isAuthorized may expose privileged functionality