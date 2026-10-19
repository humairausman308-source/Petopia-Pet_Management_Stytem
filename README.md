# Petopia Pet Shop Management System

Petopia is a web-based pet-shop management system developed for the Software Construction and Development (SCD) course.

## Project information

- **Group/Section:** BSSE Group B
- **Team members:** Aimen Ishtiaq and Humaira Usman
- **Instructor:** Engr. Umar Haroon
- **Repository:** https://github.com/humairausman308-source/Petopia-Pet_Management_System.git
- **Status:** Development is in progress.

## Technology stack

### Frontend
- HTML5
- CSS3
- Vanilla JavaScript

The existing frontend is to be preserved. Changes should be limited to approved functionality and necessary security fixes.

### Backend
- Python 3.12 or later
- FastAPI
- Uvicorn
- Pydantic v2
- SQLAlchemy
- PyMySQL
- Alembic
- JWT (HS256)
- bcrypt

### Database
- MySQL 8

### Middleware and shared controls
The application includes request-body size limiting, security headers, request-context handling, configured CORS handling, and centralized exception handling. Login and registration rate limiting is implemented in memory. Authentication and authorization are enforced through dependencies and service-level checks.

## Architecture

The backend separates API routers, business services, repositories, SQLAlchemy models, Pydantic schemas, and shared configuration/security/database components. The frontend communicates with the backend through the documented API contract. MySQL stores persistent application data.

## Main functionality

- Account registration and login
- Authentication and role-appropriate authorization
- Pet information and availability
- Appointment-related records and approved status values
- Cash-on-delivery payment path
- Safepay sandbox card checkout
- Structured validation and error responses

## Payment scope

Card checkout uses Safepay sandbox/test configuration. A payment must not be marked successful until provider confirmation has been verified. COD must not be represented as paid before delivery/settlement under the configured business process. Easypaisa is conditional on verified provider/account support and remains disabled by default unless explicitly configured. Real-money processing and refunds are outside the current scope.

## Requirements

- Python 3.12 or later
- MySQL 8
- Environment configuration for database connectivity and application secrets
- Sandbox payment credentials for testing the online payment path

## Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/humairausman308-source/Petopia-Pet_Management_System.git
   cd Petopia-Pet_Management_System
   ```

2. Review the backend setup instructions in `backend/README.md` and the environment example/configuration files included in the repository.
3. Configure the required database connection and application secrets through environment variables. Do not commit real credentials or secrets.
4. Create or configure the MySQL 8 database required by the application.
5. Install backend dependencies using the project's documented setup instructions.
6. Apply the documented database migrations/setup steps.
7. Start the FastAPI application using the command documented in `backend/README.md`.
8. Run the backend tests before considering the application ready for use.

Use the repository's actual backend instructions and environment template as the source of truth for required variable names and exact commands.

## Testing and code quality

The project uses pytest and HTTPX for backend testing. pytest-cov can be used for coverage reporting. Ruff and Black may be used for linting and formatting. Tests should cover authentication, authorization, input validation, error handling, database behavior, and payment status transitions.

## Current scope and limitations

- The pet “Buy” action remains a placeholder; a complete purchase/order workflow is not included.
- A customer-facing feedback submission form is not part of the approved UI scope.
- Administrator pet-management and appointment-control UI improvements remain planned until implemented and tested.
- Rate limiting is currently in memory and is process-local; a shared store is required for consistent limits across multiple instances.
- Safepay is configured for sandbox/test use. Real-money processing and refunds are out of scope.
- Easypaisa must remain disabled unless support and configuration are confirmed.

## Documentation

The detailed requirements specification is provided in `docs/requirements.md` in the project repository once this file is placed there.
