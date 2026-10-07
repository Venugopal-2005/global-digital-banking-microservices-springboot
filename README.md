# Global Digital Banking System – Microservices Project 
Link: https://gdb-banking-portal.vercel.app/dashboard

https://github.com/Venugopal-2005

# Global Digital Bank (GDB) - Enterprise Distributed Banking Platform

[![Java 17](https://img.shields.io/badge/Java-17-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-Gateway%20%7C%20Eureka-blue.svg)](https://spring.io/projects/spring-cloud)
[![React 18](https://img.shields.io/badge/React-18.2-cyan.svg)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📌 Executive Summary

**Global Digital Bank (GDB)** is an enterprise-grade, distributed microservices-based core banking application designed to handle end-to-end retail and corporate banking workflows. The system features multi-tier architecture, autonomous database-per-service persistence, dynamic service discovery, intelligent API routing, role-based access control (RBAC), simulated external verification registries (UIDAI Aadhar & MCA CIN), a centralized payment gateway simulator, credit card and statement lifecycle management, and Google Gemini AI-driven financial insights.

---

## 🏛️ System Architecture

The platform is designed following the **Database-per-Service** and **API Gateway Pattern** with **Netflix Eureka** for dynamic service discovery and **Spring Security + JWT** for distributed authentication.

```
                                  ┌───────────────────────────────┐
                                  │   React 18 + Vite Frontend   │
                                  │     (Port 3000 / SPA / UI)    │
                                  └──────────────┬────────────────┘
                                                 │ HTTP / REST / JWT
                                                 ▼
                                  ┌───────────────────────────────┐
                                  │   Spring Cloud API Gateway    │
                                  │          (Port 8000)          │
                                  └───────┬──────────────┬────────┘
                                          │              │
                    Service Discovery ┌───▼──────────────▼───┐ Dynamic Lookup
                    & Heartbeats      │    Eureka Server     │
                                      │     (Port 8761)      │
                                      └───▲──────────────▲───┘
                                          │              │
         ┌────────────────────────────────┴──────────────┴────────────────────────────────┐
         │                                                                                │
   ┌─────▼──────────┐ ┌───────────────┐ ┌───────────────┐ ┌─────────────────┐ ┌──────────▼────────┐
   │  auth-service  │ │ users-service │ │account-service│ │transactions-svc │ │ credit-cards-svc  │
   │  (Port 8004)   │ │  (Port 8003)  │ │  (Port 8001)  │ │   (Port 8002)   │ │    (Port 8010)    │
   └───────┬────────┘ └───────┬───────┘ └───────┬───────┘ └────────┬────────┘ └─────────┬─────────┘
           │                  │                 │                  │                    │
      ┌────▼─────┐       ┌────▼─────┐      ┌────▼─────┐       ┌────▼─────┐         ┌────▼─────┐
      │ auth_db  │       │ users_db │      │accounts_db       │transact_db         │creditcard_│
      └──────────┘       └──────────┘      └──────────┘       └──────────┘         └──────────┘
         │                                      │                  │
         │                    Inter-Service     │                  │  Settlement
         │                    KYC Check         ▼                  ▼  Routing
         │               ┌────────────────────────┐      ┌────────────────────────┐
         │               │     aadhar-service     │      │payment-gateway-service │
         │               │  (Port 8005 - UIDAI)   │      │ (Port 8008 - UPI/IMPS) │
         │               └────────────────────────┘      └────────────────────────┘
         │               ┌────────────────────────┐      ┌────────────────────────┐
         │               │    company-service     │      │ bank-statements-service│
         │               │   (Port 8006 - MCA)    │      │  (Port 8011 - Export)  │
         │               └────────────────────────┘      └────────────┬───────────┘
         │               ┌────────────────────────┐                   │
         │               │    settings-service    │              ┌────▼─────┐
         │               │      (Port 8012)       │              │statement_│
         │               └───────────┬────────────┘              └──────────┘
         │                           │
         │                      ┌────▼─────┐             ┌────────────────────────┐
         │                      │settings_db│            │       ai-service       │
         │                      └──────────┘             │  (Port 8016 - Gemini)  │
         └───────────────────────────────────────────────┴────────────────────────┘
```

---

## 🛠️ Complete Tech Stack & Component Matrix

### Backend Core
- **Framework:** Java 17+, Spring Boot 3.x
- **API Routing & Discovery:** Spring Cloud Gateway, Netflix Eureka Server & Client
- **Security:** Spring Security 6, JWT (JSON Web Tokens), BCrypt Password Hashing, Distributed Token Blacklisting
- **Data Access & ORM:** Spring Data JPA, Hibernate, Spring JDBC (`NamedParameterJdbcTemplate`)
- **Resilience & Fault Tolerance:** Resilience4j (`@Retry`, Circuit Breakers), Spring AOP (`@Aspect`, `@Around` execution metrics)
- **Caching:** Spring Cache Abstraction (`@Cacheable`, `@CacheEvict`, `@CachePut`)
- **AI Integration:** Google Gemini REST / SDK for intelligent advisory and spending insights

### Frontend Presentation
- **Framework:** React 18, Vite Bundler
- **State Management:** Zustand (lightweight global store for Auth, Theme, and Notifications)
- **Routing & Navigation:** React Router DOM v6 with dynamic Protected / Public routes and RBAC guards
- **Styling & UI:** Tailwind CSS, Lucide React Icons, React Hot Toast
- **Form Handling & Validation:** React Hook Form, Zod Schema Validation
- **Data Visualization:** Recharts (Interactive account balances, transaction volume graphs)
- **HTTP Client:** Axios with custom request/response interceptors and automated Bearer token injection

### Infrastructure & Persistence
- **Databases:** PostgreSQL 15 (7 independent, isolated databases)
- **Containerization:** Docker, Docker Compose multi-stage builds, Bridge Networks, Healthcheck probes
- **Database Tooling:** pgAdmin 4, automated DDL / DML migration scripts

---

## 🧩 Microservice Catalog & Port Reference

| Service Name | Port | Database | Primary Responsibility | Upstream / Downstream Dependencies |
| :--- | :--- | :--- | :--- | :--- |
| **`gateway-service`** | `8000` | None | Unified entry point, CORS deduplication, SSL/TLS, route dispatching | Eureka Server, All downstream microservices |
| **`eureka-server`** | `8761` | None | Dynamic Service Registry, heartbeat healthcheck directory | All Microservices (Eureka Clients) |
| **`auth-service`** | `8004` | `gdb_auth_db` | User login, JWT token issuance, verification, token revocation | `users-service`, `gateway-service` |
| **`users-service`** | `8003` | `gdb_users_db` | User identity profiles, roles, security credentials, alert logs | `auth-service` |
| **`account-service`** | `8001` | `gdb_accounts_db` | Savings & Current accounts lifecycle, status updates, balance management | `aadhar-service`, `company-service`, `auth-service` |
| **`transactions-service`** | `8002` | `gdb_transactions_db` | Deposits, withdrawals, domestic fund transfers, transaction logging | `account-service`, `payment-gateway-service`, `auth-service` |
| **`aadhar-service`** | `8005` | None (In-Memory) | Mock UIDAI registry for Savings Account KYC identity verification | `account-service` |
| **`company-service`** | `8006` | None (In-Memory) | Mock MCA CIN registry for Current / Corporate Account onboarding | `account-service` |
| **`payment-gateway-service`**| `8008` | None | Settlement simulator supporting UPI, IMPS, RTGS, and NEFT | `transactions-service` |
| **`credit-cards-service`** | `8010` | `gdb_credit_cards_db` | Credit card applications, limits, statement billing, and card payments | `transactions-service`, `account-service` |
| **`bank-statements-service`**| `8011` | `gdb_bank_statements_db` | Financial statement previews, PDF generation, date-filtered transaction export | `transactions-service`, `account-service` |
| **`settings-service`** | `8012` | `gdb_settings_db` | User preferences, theme settings, security configurations, 2FA states | `users-service` |
| **`ai-service`** | `8016` | Read-only access | Gemini AI conversational banking assistant and financial analytics | `account-service`, `transactions-service` |
| **`frontend`** | `3000` | Local Storage | React SPA user interface with responsive dark/light themes | `gateway-service` |

---

## 👥 Role-Based Access Control (RBAC) Matrix

| Feature / Page | Admin (`ADMIN`) | Branch Manager (`MANAGER`) | Bank Teller (`TELLER`) | Customer (`CUSTOMER`) |
| :--- | :---: | :---: | :---: | :---: |
| **Dashboard & Portfolio Overview** | ✅ Full Access | ✅ Full Access | ✅ Full Access | ✅ Full Access |
| **User Onboarding & Management** | ✅ Create / Edit / Deactivate | ❌ View Only | ❌ No Access | ❌ No Access |
| **Account Onboarding (Savings/Current)** | ✅ Full Access | ✅ Approve / Edit | ✅ Create & Verify | ❌ View Own Only |
| **Cash Deposit & Withdrawal Operations** | ❌ Audit Only | ❌ Override Only | ✅ Process / Execute | ❌ Request Only |
| **Domestic Fund Transfer & Limits** | ❌ View Logs | ❌ Adjust Policy | ✅ Execute Transfer | ✅ Self Transfer |
| **Credit Card Application & Management** | ✅ Audit Reports | ✅ Approval Desk | ✅ Submit App | ✅ Apply & Pay |
| **Statement Generation & Export** | ✅ Global Reports | ✅ Branch Statements | ✅ Account History | ✅ Download Own |
| **Security Alerts & Audit Logs** | ✅ Full Audit Log | ✅ Read Alerts | ❌ No Access | ❌ No Access |
| **AI Advisory & Financial Insights** | ✅ Usage Stats | ✅ Risk Summary | ❌ No Access | ✅ Chat & Insights |

---

## 🔄 Core Business Workflows & Data Flows

### 1. Savings & Corporate Account Onboarding Workflow
```
[Client / Teller UI]
        │
        ├─ 1. Submits KYC details (Aadhar 12-digit UID or Company 21-character CIN)
        ▼
[account-service]
        │
        ├─ 2. Calls aadhar-service (/api/v1/verify/{aadharNumber}) or company-service (/api/v1/company/verify/{cin})
        │     ↳ Protected with Resilience4j @Retry and Timeout Policy
        │
        ├─ 3. Upon 200 OK verification, verifies customer record in users-service
        │
        ├─ 4. Generates unique 12-digit Account Number, seeds Initial Balance in gdb_accounts_db
        ▼
[Response to Frontend] ➔ Renders Account Overview Card & sends Welcome notification
```

### 2. Fund Transfer & Settlement Execution
```
[Teller / Customer UI]
        │
        ├─ 1. POST /api/v1/transactions/transfer (Source, Target, Amount, Mode: IMPS/UPI/NEFT)
        ▼
[transactions-service]
        │
        ├─ 2. Validates Request DTO via @Valid and checks daily transaction cap via TransferProperties
        │
        ├─ 3. Inter-service call to account-service to check balance and lock funds
        │
        ├─ 4. Calls payment-gateway-service to simulate central banking network switch
        │
        ├─ 5. Executes double-entry debit/credit ledger updates across accounts
        │
        ├─ 6. Invalidates stale cache via @CacheEvict(value = "accounts", key = "#accountNumber")
        ▼
[Response to Frontend] ➔ Returns Transfer Reference ID & refreshes balance instantaneously
```

---

## ⚠️ Challenges, Real-World Issues & Technical Resolutions

During the architectural build, integration, and bug-fixing phases, several complex distributed systems issues were identified and resolved:

### 1. Spring Cloud Gateway vs Downstream Duplicate CORS Headers
- **Problem:** When sending requests from React (`localhost:3000`) through Gateway (`localhost:8000`) to downstream microservices, the browser rejected responses with `Multiple CORS header 'Access-Control-Allow-Origin' contains conflicting values`.
- **Root Cause:** Both the API Gateway and individual Spring Boot microservices had CORS filters enabled, causing duplicate headers in the response payload.
- **Resolution:** Implemented `DedupeResponseHeader` filter in `gateway-service/application.yml`:
  ```yaml
  default-filters:
    - DedupeResponseHeader=Access-Control-Allow-Origin Access-Control-Allow-Credentials, RETAIN_FIRST
  ```
  Centralized all CORS declarations exclusively in the API Gateway.

### 2. Spring AOP `@Around` Advice Double Execution Bug
- **Problem:** Financial transaction records were intermittently being executed and logged twice; balance deductions were doubling during withdrawals.
- **Root Cause:** In the performance monitoring aspect (`LoggingAspect.java`), `joinPoint.proceed()` was called inside the execution timer calculation *and* again in the method return statement.
- **Resolution:** Refactored the aspect advice to invoke `joinPoint.proceed()` once, store the result in an `Object` reference, compute elapsed time, and return the cached result.

### 3. Cache Desynchronization and Stale Balance Inconsistencies
- **Problem:** After executing a deposit, withdrawal, or transfer, the customer dashboard still rendered the old balance until the user performed a hard page refresh or re-logged in.
- **Root Cause:** The `account-service` used `@Cacheable` to optimize read performance on account summaries, but mutation endpoints lacked eviction triggers.
- **Resolution:** Added `@CacheEvict(value = "accounts", key = "#accountNumber")` on all balance-modifying service operations to guarantee immediate read-after-write consistency.

### 4. JPA Sorting Crash on Snake_case Database Column Names
- **Problem:** Fetching the Security Alerts grid with dynamic sorting crashed with `PropertyReferenceException: No property 'alert_date' found for type SecurityAlert`.
- **Root Cause:** The REST client passed raw SQL column names (`alert_date`) instead of JPA Java entity property names (`alertDate`).
- **Resolution:** Sanitized and mapped incoming sort request parameters to entity field identifiers within the Spring Data JPA specification layer.

### 5. Swallowed Downstream Verification Errors in Resilience4j Fallbacks
- **Problem:** When an invalid Aadhar number was entered, the user interface displayed a generic `500 Service Outage` error banner instead of a descriptive `Aadhar Not Found` validation error.
- **Root Cause:** The Feign / RestTemplate catch block wrapped all HTTP non-2xx status codes (including `404 Not Found` and `400 Bad Request`) into a generic `RuntimeException`.
- **Resolution:** Added specific `HttpClientErrorException` handling in `AadharClient.java` to extract the downstream message and propagate exact HTTP 4xx validation feedback to the frontend.

### 6. Distributed Token Revocation & Session Blacklisting
- **Problem:** Standard stateless JWTs remained valid until their expiration timestamp even after a user clicked "Logout" or an admin deactivated their profile.
- **Root Cause:** Stateless token validation did not check if the token had been explicitly revoked.
- **Resolution:** Built an in-memory / cache-backed token blacklist mechanism in `auth-service`. The gateway/filter inspects the token signature against revoked tokens before delegating requests.

---

## 🎯 Interview Quick Reference & System Design Discussion Points

When explaining this project in software engineering interviews, emphasize these core architecture and system design concepts:

### 1. Why Microservices over a Monolith?
- **Domain Decoupling:** Banking systems have strictly segmented domain boundaries (Core Accounts, High-Volume Payments, Fraud/Audit, Credit Operations).
- **Independent Scaling:** The `transactions-service` experiences 10x higher traffic spikes during peak hours than `account-service` onboarding. Microservices enable independent horizontal scaling.
- **Fault Isolation:** A temporary outage in the external UIDAI KYC integration does not impede internal payment transfers or balance checks.

### 2. Database-per-Service Trade-offs & Consistency
- **Trade-off:** We traded monolithic ACID transactions across all tables for database independence and autonomous deployments.
- **Consistency Model:** Used strong consistency for balance modifications within `account-service` and transactional boundaries with compensating actions across multi-service workflows (Saga pattern readiness).

### 3. Distributed Security Architecture
- **Stateless Authorization:** Cryptographically signed JWTs carrying user role claims (`ADMIN`, `MANAGER`, `TELLER`, `CUSTOMER`).
- **Gateway Security:** Gateway validates token authenticity and strips/forwards claims to downstream services via HTTP headers, eliminating redundant auth lookups.

### 4. Resilience & Graceful Degradation
- **Resilience4j:** Automatic retry policies with exponential backoff for flaky external network registries (Aadhar/CIN).
- **Graceful Fallbacks:** Mock registries ensure local environment testability without requiring external live government API gateways.

---

## 🚀 Setup & Installation Guide

### Prerequisites
- **Java:** JDK 17 or higher
- **Build Tool:** Apache Maven 3.8+
- **Node.js:** v18.0+ & npm 9+
- **Database:** PostgreSQL 15+ running on port `5432`
- **Optional:** Docker & Docker Compose

---

### Step 1: Database Setup (PostgreSQL)
Ensure your PostgreSQL instance is running with user `postgres` and password `postgres` (or update your `application.yml` files accordingly). Create the 7 isolated databases:

```sql
CREATE DATABASE gdb_auth_db;
CREATE DATABASE gdb_users_db;
CREATE DATABASE gdb_accounts_db;
CREATE DATABASE gdb_transactions_db;
CREATE DATABASE gdb_credit_cards_db;
CREATE DATABASE gdb_settings_db;
CREATE DATABASE gdb_bank_statements_db;
```

Execute the initial seed script in `gdb_users_db` (or allow Spring Boot JPA DDL auto-generation to populate schemas).

---

### Step 2: Running via Docker Compose (Recommended)
You can launch the entire ecosystem (Databases, Eureka, Gateway, Microservices, and React Frontend) with a single command:

```bash
# Build and start all 15 containers
docker-compose up --build
```

---

### Step 3: Running Locally via PowerShell Script (Windows)
We provide an automated runner script [autorun.ps1](file:///d:/PROJECTS/gdb/autorun.ps1) that launches all microservices and the frontend in separate terminal windows:

```powershell
.\autorun.ps1
```

---

### Step 4: Manual Startup Order (Terminal by Terminal)

1. **Service Registry:**
   ```bash
   cd eureka-server && mvn spring-boot:run
   ```
   *(Verify Eureka Dashboard at `http://localhost:8761`)*

2. **Core Services:**
   ```bash
   cd auth-service && mvn spring-boot:run
   cd users-service && mvn spring-boot:run
   cd account-service && mvn spring-boot:run
   cd transactions-service && mvn spring-boot:run
   cd aadhar-service && mvn spring-boot:run
   cd company-service && mvn spring-boot:run
   cd payment-gateway-service && mvn spring-boot:run
   cd credit-cards-service && mvn spring-boot:run
   cd bank-statements-service && mvn spring-boot:run
   cd settings-service && mvn spring-boot:run
   cd ai-service && mvn spring-boot:run
   ```

3. **API Gateway:**
   ```bash
   cd gateway-service && mvn spring-boot:run
   ```

4. **Frontend:**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

---

## 🔑 Default Test Credentials

The system comes pre-configured with default credentials for role testing:

| Role | Username | Password | Permitted Capabilities |
| :--- | :--- | :--- | :--- |
| **System Administrator** | `admin` | `password` | User CRUD, Security Alerts, System Configuration |
| **Branch Manager** | `manager` | `password` | Account Approval, Audit Reports, Risk Analytics |
| **Bank Teller** | `teller` | `password` | Savings/Current Onboarding, Deposits, Withdrawals, Transfers |

---

## 🧪 Testing & Verification

Run automated JUnit 5 & Mockito test suites across any microservice:

```bash
# Run tests for account service
cd account-service
mvn test

# Run build across all services skipping tests for speed
mvn clean install -DskipTests
```

---

## 📄 License & Contribution
This project is developed as an enterprise banking demonstration. Built with best practices in distributed systems, security, and modern web design.
