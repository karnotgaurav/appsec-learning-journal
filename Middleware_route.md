route is something that tell the url where to go 
A route matches a URL pattern to a specific function.

    GET /users → triggers the function getAllUsers()

middleware is code that runs in the middle -between the time the server receives the request and the time it reaches the final route 

it logs when the request was made the time and ip 
it also do authentication checks and sends 403 response
it also can add mode 
It can modify the request: It can add information (like attaching the user's ID to the request object) before passing it along.