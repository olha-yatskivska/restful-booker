# Smoke Test Suite

### Project Overview & Baseline Analysis

In this project, I reverse-engineered the existing automated API test scripts provided by the repository's author to extract a formalized Smoke Test Suite. By analyzing the underlying codebase, I verified that these tests successfully exercise the application's core critical paths (CRUD operations and basic authentication). I executed this baseline suite via the terminal (npm test) to validate the initial system health.

### Expanding Coverage with Postman

While the developer's initial tests provide a solid foundation, my independent test analysis revealed several critical coverage gaps. I applied formal test design techniques to identify overlooked edge cases, negative scenarios, and authorization vulnerabilities. To ensure comprehensive quality, I am developing a supplementary suite of automated API tests using Postman to cover these complex scenarios and bridge the testing gaps.



| Endpoint / Suite  | Scenario                                   | Expected Result (Status & Payload)   |
|-------------------|--------------------------------------------|--------------------------------------|
| System (Root)     | Ping the server (/ping)                    | 201 Created                          |
| System (Root)     | Request an invalid path (/foo/bar)         | 404 Not Found                        |
| GET /booking      | Request all bookings                       | 200 OK, returns list of booking IDs  |
| GET /booking      | Filter by firstname                        | 200 OK, returns matching IDs         |
| GET /booking      | Filter by lastname                         | 200 OK, returns matching IDs         |
| GET /booking      | Filter by checkin date                     | 200 OK, returns matching IDs         |
| GET /booking      | Filter by checkout date                    | 200 OK, returns matching IDs         |
| GET /booking      | Filter by checkin & checkout dates         | 200 OK, returns matching IDs         |
| GET /booking      | Filter by name AND dates combined          | 200 OK, returns matching IDs         |
| GET /booking      | Filter with invalid date format            | 500 Internal Server Error            |
| GET /booking/{id} | Request specific booking ID (JSON Accept)  | 200 OK, returns JSON booking data    |
| GET /booking/{id} | Request specific booking ID (XML Accept)   | 200 OK, returns XML booking data     |
| POST /booking     | Submit valid JSON payload                  | 200 OK, assigns new ID               |
| POST /booking     | Submit valid XML payload                   | 200 OK, assigns new ID               |
| POST /booking     | Submit incomplete payload                  | 500 Internal Server Error            |
| POST /booking     | Submit multiple requests sequentially      | 200 OK, increments IDs correctly     |
| POST /booking     | Submit valid payload, request XML response | 200 OK, returns XML payload          |
| POST /booking     | Submit payload with extra/unmapped fields  | 200 OK, ignores extra fields         |
| POST /booking     | Request with invalid Accept header (/ogg)  | 418 I'm a Teapot                     |
| POST /auth        | Submit valid credentials                   | 200 OK, returns auth token           |
| POST /auth        | Submit invalid credentials                 | 200 OK, returns "Bad credentials"    |
| PUT /booking      | Update booking without token               | 403 Forbidden                        |
| PUT /booking      | Update booking with invalid token          | 403 Forbidden                        |
| PUT /booking      | Update booking with valid token            | 200 OK, returns updated JSON         |
| PUT /booking      | Update booking with Basic Auth header      | 200 OK, returns updated JSON         |
| PUT /booking      | Update non-existent booking ID             | 405 Method Not Allowed               |
| PUT /booking      | Update using XML payload                   | 200 OK, returns updated JSON         |
| PUT /booking      | Update valid booking, request XML response | 200 OK, returns updated XML          |
| DELETE /booking   | Delete booking without token               | 403 Forbidden                        |
| DELETE /booking   | Delete booking with invalid token          | 403 Forbidden                        |
| DELETE /booking   | Delete valid booking with token            | 201 Created                          |
| DELETE /booking   | Delete valid booking with Basic Auth       | 201 Created                          |
| DELETE /booking   | Delete non-existent booking ID             | 405 Method Not Allowed               |
