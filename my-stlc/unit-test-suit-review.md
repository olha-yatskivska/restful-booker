# API Documentation and Baseline Test Review


### API Documentation & Baseline Test Review
In this project, I reverse-engineered the repository author's existing automated API test scripts to extract a formalized Smoke Test Suite. By analyzing the underlying codebase, I verified that these tests successfully exercise the application's core critical paths (CRUD operations and basic authentication). I executed this baseline suite via the terminal (npm test) to validate the initial system health. However, upon reviewing the results, I identified several architectural defects. 
To document this, I created a baseline matrix comparing the code's current behavior against industry security standards. This shift-left approach allowed me to identify requirement-level bugs before expanding the automated test suite.

Reference: The test oracle used for HTTP status code validation is based on standard REST conventions: [The five classes of HTTP status codes](https://blog.postman.com/what-are-http-status-codes/)

Link Bug reports 

### Expanding Coverage & Shift-Left Analysis

While the developer's initial tests provided a solid foundation, my independent test analysis revealed critical coverage gaps. I applied formal test design techniques to identify overlooked edge cases, negative scenarios, and authorization vulnerabilities.

Link to Full Test Analysis Documentation
Link to Postman Collection

### A matrix comparing the code's current behavior against industry security standards

| Endpoint / Suite  | Scenario                                   | Expected Result according to the code|  Expected result according to the best practices standard                           | 
|-------------------|--------------------------------------------|--------------------------------------|------------------------------------------------------------------------------------ |
| System (Root)     | Ping the server (/ping)                    | 201 Created                          | 200 OK/204 No content                                                               |
| System (Root)     | Request an invalid path (/foo/bar)         | 404 Not Found                        | 404 Not Found                                                                       |
| GET /booking      | Request all bookings                       | 200 OK, returns list of booking IDs  | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by firstname                        | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by lastname                         | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by checkin date                     | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by checkout date                    | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by checkin & checkout dates         | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by name AND dates combined          | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter with invalid date format            | 500 Internal Server Error            | 400 Bad Request (client error responses) Bug report RE-002                          |
| GET /booking/{id} | Request specific booking ID (JSON Accept)  | 200 OK, returns JSON booking data    | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking/{id} | Request specific booking ID (XML Accept)   | 200 OK, returns XML booking data     | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| POST /booking     | Submit valid JSON payload                  | 200 OK, assigns new ID               | 201 Created/200 OK, assigns new ID                                                  | 
| POST /booking     | Submit valid XML payload                   | 200 OK, assigns new ID               | 201 Created/200 OK, assigns new ID                                                  |  
| POST /booking     | Submit incomplete payload                  | 500 Internal Server Error            | 400 Bad Request (client error responses) Bug report RE-003                          |     
| POST /booking     | Submit multiple requests sequentially      | 200 OK, increments IDs correctly     | 200 OK, increments IDs correctly                                                    |
| POST /booking     | Submit valid payload, request XML response | 200 OK, returns XML payload          | 200 OK, returns XML payload                                                         |
| POST /booking     | Submit payload with extra/unmapped fields  | 200 OK, ignores extra fields         | 200 OK, ignores extra fields                                                        |
| POST /booking     | Request with invalid Accept header (/ogg)  | 418 I'm a Teapot                     | 400 Bad Request/406 Not Acceptable                                                  |    
| POST /auth        | Submit valid credentials                   | 200 OK, returns auth token           | 200 OK, returns auth token                                                          |
| POST /auth        | Submit invalid credentials                 | 200 OK, returns "Bad credentials"    | 401 Unauthorized                                                                    |
| PUT /booking      | Update booking without token               | 403 Forbidden                        | 401 Unauthorized                                                                    |
| PUT /booking      | Update booking with invalid token          | 403 Forbidden                        | 401 Unauthorized                                                                    |
| PUT /booking      | Update booking with valid token            | 200 OK, returns updated JSON         | 200 OK, returns updated JSON                                                        |    
| PUT /booking      | Update booking with Basic Auth header      | 200 OK, returns updated JSON         | 200 OK, returns updated JSON                                                        |
| PUT /booking      | Update non-existent booking ID             | 405 Method Not Allowed               | 404 Not Found (if authorized) or 401/403 (if unauthorized/invalid token)            |
| PUT /booking      | Update using XML payload                   | 200 OK, returns updated JSON         | 200 OK, returns updated JSON                                                        | 
| PUT /booking      | Update valid booking, request XML response | 200 OK, returns updated XML          | 200 OK, returns updated XML                                                         |
| DELETE /booking   | Delete booking without token               | 403 Forbidden                        | 401 Unauthorized                                                                    |
| DELETE /booking   | Delete booking with invalid token          | 403 Forbidden                        | 401 Unauthorized                                                                    |
| DELETE /booking   | Delete valid booking with token            | 201 Created                          | 204 No Content/200 OK                                                               |
| DELETE /booking   | Delete valid booking with Basic Auth       | 201 Created                          | 204 No Content/200 OK                                                               |
| DELETE /booking   | Delete non-existent booking ID             | 405 Method Not Allowed               | 404 Not Found (if authorized) or 401/403 (if unauthorized/invalid token)            |    
