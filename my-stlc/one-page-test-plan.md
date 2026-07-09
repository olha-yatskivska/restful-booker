# Test Plan: Epic: Restful-Booker API Functional and Security Validation 
> **Identifier:** #TP001
> **Reference Template:** One-page Test Plan

---

## Project Overview
| Attribute | Details |
| :--- | :--- |
| **Project** | Restful-Booker |
| **Site/App** | [API restful-booker](https://restful-booker.herokuapp.com/apidoc/index.html) |
| **Feature Under Test** | PI-01 Restful-Booker API Endpoints (CRUD & Auth)|
| **Owner / QA Lead** | Tester |
| **Release / Sprint** | R01 / S01 |

---

## Introduction
Restful-booker is a Create Read Update Delete Web API that comes with authentication features. 

## Goals
1. Functional validation of the module
2. Verification of data integrity
3. Deriving non-functional quality characteristics need to be tested
5. Creation Postman collection
6. Creation test documantation 
7. Using LLMs for Risk-based analysis

## Scope
* **In Scope:** Parsing, Schema validation, CRUD operations, business rules, parsing, API security (BOLA/auth)
* **Out Of Scope:** performance at scale, deep dive into security, interaction capability (usability/accessability), database layer validation
  
## Risks
* Environment availability: Local Docker API test enviroment is running correctly
* No requirements, based on Assamption
* No knowledge of internal structure and integrations

## Environments & Tools
* **OS/Browsers:** API
* **Testing Tools:** Postman
* **Source Control:** GitHub

## Criteria
### Entry Criteria
* [ ] Condition 1: Requirements are ready
* [ ] Condition 2: Test data is prepared
* [ ] Condition 3: Local Docker API environment is running successfully

### Exit Criteria
* [ ] Condition 1: 100% of critical tests passed
* [ ] Condition 2: All defects are logged

## Schedule & Estimations
| Task | Estimation |
| :--- | :--- |
| Test Analysis & Design | [3/15 |
| Test Implementation |  [5/25 |
| Test Execution | 2/10] |
| Reporting | 3/15] |
