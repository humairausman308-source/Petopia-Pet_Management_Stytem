# Petopia Pet Shop Management System

## Software Requirements Specification

**Course:** Software Construction and Development (SCD)  
**Group/Section:** BSSE Group B  
**Team members:** Aimen Ishtiaq; Humaira Usman  
**Instructor:** Engr. Umar Haroon  
**GitHub repository:** https://github.com/humairausman308-source/Petopia-Pet_Management_System.git  
**Project status:** Development is in progress.

## 1. Project Information

**Project title:** Petopia Pet Shop Management System

**Course:** Software Construction and Development (SCD)

**Group/Section:** BSSE Group B

**Team members:** Aimen Ishtiaq; Humaira Usman

**Instructor:** Engr. Umar Haroon

**Repository:** https://github.com/humairausman308-source/Petopia-Pet_Management_System.git

**Project status:** Development is in progress.

## 2. Introduction

**2.1 Purpose:** This document defines the functional and non-functional requirements, architecture, security controls, payment scope, constraints, and prioritized backlog for Petopia Pet Shop Management System.

**2.2 System overview:** Petopia is a web-based system for managing pet-shop information and related customer activities. The system uses an existing browser-based frontend, a Python API backend, and a MySQL database. It includes authentication, pet and appointment-related functions, and a payment flow limited to the approved scope.

**2.3 Problem statement:** Pet-shop information and operational activities can become difficult to maintain when records, customer requests, appointments, and payment states are handled inconsistently. Petopia aims to centralize these activities and apply validation, access control, and consistent data handling.

## 3. Objectives

**O-01:** Provide a consistent web interface for customers and administrators.

**O-02:** Store and retrieve pet-shop records through a centralized database.

**O-03:** Support authenticated access and role-appropriate authorization.

**O-04:** Manage appointment records and their approved status transitions.

**O-05:** Provide clearly defined cash-on-delivery and sandbox online-payment paths.

**O-06:** Improve maintainability through separation of frontend, API, service, repository, and database responsibilities.

## 4. Intended Users

**Customer:** Browses available pet information and uses the customer-facing functions currently implemented in the frontend.

**Administrator:** Manages system records and performs authorized administrative tasks, including planned pet-management and appointment-control interface improvements.

**Developer/maintainer:** Configures, tests, maintains, and deploys the application.

## 5. System Architecture and Technology Requirements

**5.1 Frontend:** The frontend uses HTML5, CSS3, and vanilla JavaScript. Existing pages and styling are to be preserved. Changes should be limited to approved functional work and necessary security fixes; a visual redesign is not part of the scope.

**5.2 Backend:** The backend is implemented in Python 3.12 or later using FastAPI and Uvicorn. Pydantic v2 is used for request/response validation and settings-related data structures. The API is organized into routers, services, repositories, and SQLAlchemy models.

**5.3 Database:** MySQL 8 is the database platform. SQLAlchemy provides ORM access, PyMySQL provides the MySQL driver, and Alembic supports schema migrations. Database configuration and credentials must be supplied through environment-based settings rather than hard-coded secrets.

**5.4 Middleware and request handling:** The application includes request-body size limiting, security headers, request-context handling, configured CORS handling, and centralized exception handling. Uvicorn serves the FastAPI application. These controls support consistent request processing but do not replace endpoint-level authorization or validation.

**5.5 Shared security controls:** Authentication uses JWT with HS256. Passwords are hashed using bcrypt. Authorization is enforced through FastAPI dependencies and service-level ownership/permission checks. Login and registration rate limiting is implemented in memory. Input validation uses Pydantic schemas; frontend output should be safely escaped where applicable. Production configuration must use strong secrets, restricted CORS origins, HTTPS, and secure deployment settings.

**5.6 Payments:** Cash on delivery (COD) is supported in the approved scope. Card payment is integrated with Safepay in sandbox/test mode. An Easypaisa route is conditional on verified provider/account support and remains disabled by default unless explicitly configured. An online payment must not be marked paid merely because checkout was initiated; payment status must rely on verified provider confirmation. Real-money processing and refunds are outside the current project scope.

**5.7 Development and test tools:** Git and GitHub are used for version control. Pytest and HTTPX are used for backend testing; pytest-cov can measure coverage. Ruff and Black may be used for linting and formatting. The project requires Python 3.12 or later and MySQL 8.

## 6. Functional Requirements

**FR-01 — Account registration:** The system shall allow a user to register using the fields supported by the implemented registration interface and API.

**FR-02 — Login:** The system shall authenticate users with valid credentials and reject invalid credentials.

**FR-03 — Password storage:** The system shall store password hashes rather than plaintext passwords.

**FR-04 — Authentication state:** Protected API operations shall require valid authentication where specified by the API contract.

**FR-05 — Authorization:** The system shall restrict administrative actions to authorized roles and enforce ownership checks for user-specific resources.

**FR-06 — Pet information:** The system shall retrieve and display pet information available through the current frontend and API.

**FR-07 — Availability information:** The system shall represent pet availability/status consistently in stored records and API responses.

**FR-08 — Administrative pet management:** The planned administrator interface shall support authorized viewing, adding, editing, updating availability/status, and safely retiring pet records.

**FR-09 — Appointment records:** The system shall support the appointment-related operations currently defined by the API contract.

**FR-10 — Appointment status:** Authorized administrative appointment controls shall support the approved statuses Scheduled, Completed, and Cancelled.

**FR-11 — Data validation:** The system shall validate incoming data and return consistent validation errors for invalid requests.

**FR-12 — Error responses:** The API shall return structured error responses without exposing stack traces or sensitive internal details to clients.

**FR-13 — Database persistence:** The system shall persist supported application records in MySQL.

**FR-14 — Schema migration:** Database schema changes shall be managed through versioned migrations where applicable.

**FR-15 — Request protection:** The system shall apply configured request-size limits, CORS policy, security headers, and authentication/rate-limit controls.

**FR-16 — Payment choice:** The checkout flow shall distinguish the supported COD path from the Safepay sandbox card-payment path.

**FR-17 — Payment status:** The system shall not mark an online payment as successful until provider confirmation has been verified.

**FR-18 — COD status:** COD shall not be represented as paid before delivery/settlement according to the configured business process.

**FR-19 — Payment configuration:** Provider keys, webhook secrets, and payment settings shall be supplied through environment configuration, not committed as source code.

**FR-20 — Payment failure handling:** The system shall handle cancelled, failed, or unconfirmed online payment attempts without falsely recording a successful payment.

**FR-21 — Frontend compatibility:** The backend shall provide the documented API behavior required by the existing frontend, except for explicitly approved changes.

**FR-22 — Safe output handling:** Frontend code shall safely escape untrusted text before inserting it into HTML contexts where applicable.

**FR-23 — Logging and request context:** The backend shall attach request context and log operational errors in a way that supports debugging without unnecessarily exposing secrets or credentials.

**FR-24 — Customer feedback:** A customer-facing feedback submission form is not included in the currently approved UI scope.

**FR-25 — Pet purchase action:** The current pet “Buy” action remains a placeholder and is not a complete purchase/order workflow.

## 7. Non-Functional Requirements

**NFR-01 — Security:** Credentials and secrets shall not be hard-coded or committed to the repository. Production traffic shall use HTTPS and production-safe secret values.

**NFR-02 — Access control:** Protected resources and administrative operations shall enforce authentication, authorization, and ownership rules on the server.

**NFR-03 — Data integrity:** The system shall validate inputs and use database constraints/transactions where required to prevent inconsistent records.

**NFR-04 — Reliability:** Unexpected errors shall be handled centrally and should not expose internal stack traces to clients.

**NFR-05 — Maintainability:** The backend shall keep routing, business logic, data access, schemas, and shared configuration in separate responsibilities.

**NFR-06 — Compatibility:** The existing HTML/CSS/JavaScript frontend shall remain compatible with the API and retain its established visual design.

**NFR-07 — Performance:** Common API requests should avoid unnecessary database queries and return within a reasonable response time under normal project-scale use.

**NFR-08 — Scalability constraint:** The current in-memory rate limiter is process-local. A shared rate-limit store is needed before relying on consistent limits across multiple backend instances.

**NFR-09 — Usability:** User-facing validation and error messages should be understandable and should not expose technical internals.

**NFR-10 — Testability:** API routes, validation, authentication, authorization, and payment-state behavior should be covered by automated tests where practical.

**NFR-11 — Configuration:** Environment-specific values such as database credentials, signing secrets, CORS origins, and payment provider settings shall be configurable without source-code changes.

**NFR-12 — Portability:** The application should be runnable in a documented Python environment with the required MySQL service and configured environment variables.

## 8. Main System Modules

**Authentication and account module:** Registration, login, password hashing, token validation, and protected access.

**Pet information module:** Retrieval and display of pet records and availability information.

**Administration module:** Authorized management of pet records and planned appointment controls.

**Appointment module:** Appointment-related records and approved status handling.

**Payment module:** COD and Safepay sandbox card checkout, with verified status transitions and conditional Easypaisa configuration.

**API and validation module:** FastAPI routes, Pydantic schemas, structured responses, and centralized error handling.

**Data-access module:** SQLAlchemy models, repositories, MySQL persistence, and Alembic migrations.

**Security and request middleware module:** Request-size limit, security headers, request context, configured CORS, rate limiting, and authentication/authorization dependencies.

## 9. Prioritized Product Backlog

**Priority 1 — Critical:** Confirm environment configuration and database connectivity; verify registration/login; test JWT validation and bcrypt hashing; verify authorization and ownership checks; validate central error responses; ensure payment success cannot be recorded without verified provider confirmation.

**Priority 2 — High:** Complete automated tests for core API routes, validation, authentication, authorization, and payment status transitions; verify database migrations and data integrity; confirm the existing frontend works with the documented API contract.

**Priority 3 — Medium:** Complete the planned administrator pet-management interface; complete administrator appointment controls using Scheduled, Completed, and Cancelled; improve user-facing failure and validation feedback where already supported by the UI.

**Priority 4 — Medium/Low:** Improve automated test coverage and code-quality checks; review operational logs and deployment configuration; document backup and recovery procedures.

**Out of scope for current delivery:** A complete pet purchasing/order workflow, customer-facing feedback submission form, real-money payment processing, and refunds. Easypaisa is only included if provider/account support is confirmed and explicitly enabled.

## 10. Assumptions and Dependencies

**A-01:** The deployment environment provides Python 3.12 or later and MySQL 8.

**A-02:** Required environment variables and secrets will be supplied securely by the operator.

**A-03:** The existing frontend is the baseline and should not be visually redesigned.

**A-04:** Safepay sandbox credentials and configuration are available for test checkout.

**A-05:** Easypaisa support depends on provider and account availability and is not assumed to be active.

**A-06:** External provider behavior, network availability, and database availability are dependencies outside the application’s direct control.

## 11. Constraints and Known Limitations

**C-01:** The current rate limiter is in memory and does not coordinate limits across multiple worker processes or separate instances.

**C-02:** The pet “Buy” action is a placeholder; the complete purchase/order workflow is not part of the current scope.

**C-03:** Customer-facing feedback submission is not in the approved UI scope.

**C-04:** Safepay card processing is configured for sandbox/test use; real-money processing and refunds are out of scope.

**C-05:** Easypaisa must remain disabled unless its support and configuration are confirmed.

**C-06:** Administrative pet-management and appointment-control UI improvements are planned and should not be described as complete until implemented and tested.

**C-07:** The legacy Node.js backend may be retained temporarily as a reference during migration; it should not be treated as the production backend for the final Python deployment.

## 12. Team Responsibilities

**Aimen Ishtiaq:** Project planning, requirements analysis, implementation, testing, documentation, and coordination as agreed by the team.

**Humaira Usman:** Project planning, implementation, testing, documentation, and coordination as agreed by the team.

**Team responsibility:** Both team members are responsible for reviewing changes, validating requirements, maintaining repository quality, and ensuring that the submitted project accurately reflects the implemented system.

## 13. Repository and Collaboration

**Repository URL:** https://github.com/humairausman308-source/Petopia-Pet_Management_System.git

**Version control:** Git is used to track changes, while GitHub hosts the project repository. Changes should be reviewed and tested before they are merged into the main project branch.

**Documentation alignment:** Requirements and README instructions should be updated when implementation, environment variables, API behavior, or supported payment flows change.

## 14. Conclusion

**Summary:** Petopia is a web-based pet-shop management system with an HTML/CSS/JavaScript frontend, a Python FastAPI backend, and MySQL persistence. The requirements emphasize preserving the existing frontend, validating and securing API operations, maintaining clear architecture, and implementing payment flows without falsely reporting unverified payments. Development is in progress.
