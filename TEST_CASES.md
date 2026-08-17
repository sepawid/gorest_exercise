# GoREST Users API — Test Cases

| Flow | Request | Method | Expected | Purpose |
|---|---|---|---|---|
| Positive | Create a user | POST | 201 | Create user and store its ID |
| Positive | Reject duplicate user email | POST | 422 | Validate unique email |
| Positive | Get the created user | GET | 200 | Retrieve created user |
| Positive | Update the created user | PATCH | 200 | Partially update user |
| Positive | Verify the updated user | GET | 200 | Confirm PATCH persisted |
| Positive | Replace the created user | PUT | 200 | Fully replace user |
| Positive | Verify the replaced user | GET | 200 | Confirm PUT persisted |
| Positive | Delete the created user | DELETE | 204 | Delete user |
| Positive | Verify deleted user is unavailable | GET | 404 | Confirm deletion |
| Validation | Reject user without email | POST | 422 | Validate required email |
| Validation | Reject invalid email format | POST | 422 | Validate email format |
| Validation | Reject missing required fields | POST | 422 | Validate name, gender, and status |
| Validation | Reject invalid gender and status values | POST | 422 | Validate enum values |
| Validation | Reject malformed JSON body | POST | 400 / 422 | Reject invalid JSON |
| Validation | Reject unsupported content type | POST | 400 / 415 / 422 | Reject non-JSON body |
| Authentication | Reject request without authentication | POST | 401 | Require bearer token |
| Authentication | Create user for authorization checks | POST | 201 | Create isolated test user |
| Authentication | Hide user from unauthenticated update | PATCH | 404 | Do not expose token-owned user |
| Authentication | Hide user from unauthenticated delete | DELETE | 404 | Do not expose token-owned user |
| Authentication | Delete authorization-check user | DELETE | 204 | Clean up test user |
| Authentication | Reject invalid bearer token | POST | 401 | Reject invalid credentials |
| Method | Reject unsupported method on collection | PUT | 404 / 405 | Reject invalid collection operation |
| Public | List users with pagination | GET | 200 | Validate response shape and pagination headers |
| Public | Filter users by gender and status | GET | 200 | Validate server-side filtering |
| Public | Unknown user returns 404 | GET | 404 | Handle absent numeric ID |
| Public | Non-numeric user ID returns 404 | GET | 404 | Handle malformed identifier |

The suite contains 26 requests and 40 assertions. It generates unique data and deletes test users after execution.
