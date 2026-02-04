Endpoint: POST /rest/user/login

Observation:
The endpoint accepts additional fields in the request body; however, these fields are not bound to any model, persisted, or used in authentication or authorization logic.

Verification:
JWT claims and post-login behavior remain unchanged regardless of injected fields.

Conclusion:
No mass assignment vulnerability. Extra fields are safely ignored by the backend.
