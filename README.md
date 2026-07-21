# Global Digital Banking System – Microservices Architecture

A full-stack digital banking application built using **Spring Boot Microservices** and **React**, designed to simulate the core functionalities of a modern banking platform. The project follows a distributed microservices architecture where each service is responsible for a specific business capability and communicates securely through REST APIs.

This project was developed to gain hands-on experience with enterprise application development, distributed systems, authentication, API Gateway, database management, Docker, and modern frontend technologies.

---

## Features

- User Registration and Authentication
- Secure JWT-based Login
- Savings and Current Account Management
- Deposit, Withdraw and Fund Transfer
- Daily Transaction Limit Management
- User Profile Management
- Aadhaar Verification Service
- Company Verification Service
- Payment Gateway Simulation
- RESTful APIs with Swagger Documentation
- Dockerized Services
- PostgreSQL Database Integration

---

## Project Architecture

```
                React Frontend
                       │
               API Gateway Service
                       │
 ┌──────────────┬──────────────┬──────────────┐
 │              │              │              │
Auth        Users        Account      Transactions
Service     Service      Service         Service
 │              │              │              │
 ├──────────────┼──────────────┼──────────────┤
 │              │              │
Aadhaar    Company      Payment Gateway
Service     Service          Service
```

Each microservice is developed independently with its own business logic, APIs, and database interactions.

---

## Tech Stack

### Backend

- Java 17+
- Spring Boot
- Spring Security
- Spring Web
- Spring JDBC
- Maven
- JWT Authentication
- REST APIs
- Flyway Migration

### Frontend

- React
- Vite
- JavaScript
- Tailwind CSS

### Database

- PostgreSQL

### DevOps

- Docker
- Docker Compose
- Git
- GitHub

---

## Project Modules

| Service | Description |
|----------|-------------|
| Auth Service | Authentication and JWT token management |
| Users Service | User registration and profile management |
| Account Service | Savings and Current Account operations |
| Transactions Service | Deposit, Withdraw and Fund Transfer |
| Aadhaar Service | Aadhaar verification |
| Company Service | Company verification |
| Payment Gateway Service | Payment processing simulation |
| Gateway Service | API Gateway for routing requests |
| Frontend | React-based user interface |

---

## Folder Structure

```
frontend/
gateway-service/
auth-service/
users-service/
account-service/
transactions-service/
aadhar-service/
company-service/
payment-gateway-service/
database_installation_guide.md
codebase_setup_guide.md
training_backlog.md
README.md
```

---

## Getting Started

### Clone the repository

```bash
git clone https://github.com/Venugopal-2005/global-digital-banking-microservices-springboot.git
```

### Navigate into the project

```bash
cd global-digital-banking-microservices-springboot
```

### Start PostgreSQL

Run PostgreSQL locally or using Docker.

### Start Backend Services

Each service can be started individually.

```bash
cd auth-service
mvn spring-boot:run
```

Repeat the same for the remaining services.

### Start Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## API Documentation

Swagger UI is available after running the services.

Example:

```
http://localhost:8001/swagger-ui/index.html
```

---

## Docker

Build and start the services:

```bash
docker compose up --build
```

---

## Learning Outcomes

Working on this project helped me understand:

- Microservices Architecture
- Spring Boot Development
- REST API Design
- Authentication & Authorization
- JWT Security
- Docker Containers
- PostgreSQL Integration
- Frontend and Backend Communication
- API Gateway Pattern
- Real-world Banking Workflows

---

## Future Improvements

- Service Discovery with Eureka
- Centralized Configuration Server
- Kafka/RabbitMQ Integration
- Redis Caching
- CI/CD Pipeline
- Kubernetes Deployment
- Monitoring with Prometheus and Grafana

---

## Author

**Venugopal K**

B.Tech Computer Science (Core)

SRM Institute of Science and Technology

GitHub:
https://github.com/Venugopal-2005

---

## License

This project is developed for educational and learning purposes.
