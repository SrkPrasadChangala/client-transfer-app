# client-transfer-app

A full-stack Java Spring Boot and Angular application for managing ACH (Automated Clearing House) transactions. This module supports secure user authentication, ACH transfer submission, transaction processing, and viewing historical transfers. Built to real-world enterprise standards — modular, testable, secure, and CI/CD ready.

---

## Tech Stack

| Layer    | Stack                                                   |
| -------- | ------------------------------------------------------- |
| Frontend | Angular 16+, TypeScript, RxJS, Angular Material         |
| Backend  | Java 17, Spring Boot 3, Spring Security, JPA, Hibernate |
| Database | PostgreSQL, Liquibase                                   |
| DevOps   | Docker, GitHub Actions (CI/CD), Swagger, Postman        |

---

## Features (Issue-Based)

### \[#1] Implement User Authentication

* JWT-based stateless authentication
* Role-based access control for User/Admin
* Angular AuthGuard, interceptors, and token storage

### \[#2] Set Up Core App Structure

* Backend MVC setup with controllers, services, and repositories
* API versioning with `/api/v1/` endpoints
* Angular routing with lazy loading and modular architecture

### \[#3] Create Database Schema for Users and Transactions

* Tables: `users`, `ach_transactions`, `audit_logs`
* Liquibase changelogs for reproducible schema management

### \[#4] Develop ACH Transaction Data Model

* Entity: `AchTransaction`
* Fields: `senderAccount`, `receiverAccount`, `amount`, `status`, `createdAt`
* Enum for `status`: `PENDING`, `PROCESSED`, `FAILED`

### \[#5] Create UI/Form for ACH Transfer Submission

* Angular reactive form with validation (amount, account numbers)
* Integration with backend via Angular service
* Success and error notifications with Angular Material snackbar

### \[#6] Implement Backend Logic for ACH Processing

* Validations (formatting, account limits, duplicate prevention)
* Save to DB with `PENDING` status and timestamp
* Logging transaction metadata with SLF4J

### \[#7] Display ACH Transaction History for Users

* API filtered by logged-in user’s ID
* Angular material data table with pagination and filtering

### \[#8] Basic Error Handling and Logging

* `@ControllerAdvice` for exception mapping
* Centralized logging with SLF4J and Logback
* Angular global error interceptor with UI fallback

---

## Folder Structure

### Spring Boot (Backend)

```bash
server/
├── src/main/java/com/srk/achtransfer/
│   ├── controller/
│   ├── dto/
│   ├── entity/
│   ├── repository/
│   ├── service/
│   ├── security/
│   └── exception/
└── resources/
    ├── application.yml
    └── db/changelog/liquibase-changelog.xml
```

### Angular (Frontend)

```bash
client/
├── src/app/
│   ├── auth/
│   ├── transfer/
│   ├── shared/
│   └── core/
└── environments/
```

---

## Running Locally

### Backend

```bash
cd server
./mvnw spring-boot:run
```

### Frontend

```bash
cd client
npm install
ng serve
```

> PostgreSQL must be running with the expected schema and credentials. Use Docker Compose for local database provisioning.

---

## Postman Collection

Import the collection from [`./docs/client-transfer.postman_collection.json`](./docs/client-transfer.postman_collection.json) to test:

* Auth: `/auth/register`, `/auth/login`
* ACH: `/api/v1/ach/submit`, `/api/v1/ach/history`

---

## ⚙️ CI/CD Pipeline

* GitHub Actions workflows:

  * Linting
  * Unit testing (backend & frontend)
  * Docker image build & push
  * Staging deployment via Docker Compose or Kubernetes
* Includes `Dockerfile` and `docker-compose.yml`

---

## Security Overview

* BCrypt-hashed passwords
* JWT auth with short-lived access + refresh tokens
* CORS enabled with proper origins
* CSRF protections in forms and API endpoints

---

## Future Enhancements

* Admin portal for approval and review of transactions
* Export ACH history as PDF or Excel
* Email and SMS notifications
* Retry strategy for failed ACH submissions

---

## Contributors

* [SrkPrasadChangala](https://github.com/SrkPrasadChangala)
* [Achyuthgopi156](https://github.com/Achyuthgopi156)

---

## License

[MIT License](./LICENSE) — Fork, use, and contribute as needed.
