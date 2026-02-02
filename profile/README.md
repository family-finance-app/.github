# Family Finance

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16-black?logo=next.js" alt="Next.js 16">
  <img src="https://img.shields.io/badge/React-19-61DAFB?logo=react" alt="React 19">
  <img src="https://img.shields.io/badge/NestJS-11-E0234E?logo=nestjs" alt="NestJS 11">
  <img src="https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript" alt="TypeScript 5">
  <img src="https://img.shields.io/badge/PostgreSQL-17-336791?logo=postgresql" alt="PostgreSQL 17">
  <img src="https://img.shields.io/badge/Redis-7.2-DC382D?logo=redis" alt="Redis 7.2">
  <img src="https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker" alt="Docker">
  <img src="https://img.shields.io/badge/Tailwind-4-06B6D4?logo=tailwindcss" alt="Tailwind CSS 4">
</p>

A comprehensive family financial management platform that enables users to track personal and shared finances, manage multi-currency accounts, monitor transactions, and gain insights through visual analytics.

## Live Environments

| Environment | Frontend                       | Backend API                        |
| ----------- | ------------------------------ | ---------------------------------- |
| Production  | https://familyfinance.site     | https://api.familyfinance.site     |
| Development | https://dev.familyfinance.site | https://api-dev.familyfinance.site |

---

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Running the Full Stack](#option-1-full-stack-with-docker-compose-recommended)
  - [Running Services Separately](#running-services-separately)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Contributing](#contributing)

---

## Features

### Core Functionality

- **Multi-Currency Accounts** - Support for UAH, USD, and EUR with automatic exchange rate conversion via Monobank API
- **Transaction Management** - Track income, expenses, and transfers between accounts
- **Real-Time Dashboard** - Financial overview with income/expense statistics and recent activity
- **Visual Analytics** - Charts for spending patterns, category breakdown, and savings trends
- **Account Types** - Bank accounts, cash, credit cards, debit cards, deposits, digital wallets, savings, and investments
- **Customizable Categories** - Organize transactions with icons and colors
- **Responsive Design** - Works seamlessly on desktop, tablet, and mobile
- **Dark/Light Theme** - Full theme support for user preference

### Security

- **JWT Authentication** - Access tokens in JSON responses, refresh tokens in httpOnly cookies
- **Argon2 Password Hashing** - Industry-standard password security
- **Role-Based Access Control** - Secure resource authorization
- **Input Validation** - Comprehensive request validation and sanitization
- **Rate Limiting** - API and authentication endpoint protection

### Coming Soon

- **Family Groups** - Share accounts and track family finances together
- **Budget Planning** - Set and monitor spending limits by category
- **Financial Goals** - Create and track progress toward savings targets
- **Notifications** - Alerts for budget limits, goals, and important events

---

## Architecture

Family Finance uses a monolithic backend architecture for simplicity and performance, with an NGINX reverse proxy for production deployments.

```
                          ┌─────────────────────────────────────────────────────────────┐
                          │                    Family Finance Platform                   │
                          └─────────────────────────────────────────────────────────────┘

┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│                 │       │                 │       │                 │       │                 │
│    Clients      │──────►│   API Gateway   │──────►│    Backend      │──────►│   PostgreSQL    │
│  (Web/Mobile)   │       │    (NGINX)      │       │    (NestJS)     │       │   (Database)    │
│                 │       │                 │       │                 │       │                 │
└─────────────────┘       └─────────────────┘       └────────┬────────┘       └─────────────────┘
                                                             │
                          ┌─────────────────┐                │
                          │    Frontend     │                │
                          │   (Next.js)     │                ▼
                          │                 │       ┌─────────────────┐
                          └─────────────────┘       │      Redis      │
                                                    │    (Cache)      │
                                                    └─────────────────┘
```

### Data Flow

1. **Clients** access the frontend application or call the API directly
2. **API Gateway** handles routing, rate limiting, CORS, and TLS termination
3. **Backend** processes business logic, authentication, and data operations
4. **PostgreSQL** stores all persistent data (users, accounts, transactions)
5. **Redis** provides caching and health check capabilities

---

## Technology Stack

### Frontend

| Technology           | Version | Purpose                         |
| -------------------- | ------- | ------------------------------- |
| **Next.js**          | 16      | React framework with App Router |
| **React**            | 19      | UI library                      |
| **TypeScript**       | 5       | Type-safe development           |
| **Tailwind CSS**     | 4       | Utility-first CSS framework     |
| **TanStack Query**   | 5       | Data fetching and caching       |
| **Recharts**         | 3       | Data visualization              |
| **Cloudflare Pages** | -       | Deployment platform             |

### Backend

| Technology      | Version | Purpose               |
| --------------- | ------- | --------------------- |
| **NestJS**      | 11      | Node.js framework     |
| **TypeScript**  | 5       | Type-safe development |
| **Prisma**      | Latest  | Database ORM          |
| **PostgreSQL**  | 17      | Relational database   |
| **Redis**       | 7.2     | Caching layer         |
| **Argon2**      | -       | Password hashing      |
| **prom-client** | -       | Prometheus metrics    |
| **Swagger**     | -       | API documentation     |

### Infrastructure

| Technology         | Purpose                            |
| ------------------ | ---------------------------------- |
| **Docker**         | Containerization                   |
| **Docker Compose** | Multi-container orchestration      |
| **NGINX**          | Reverse proxy, load balancing, TLS |
| **GitHub Actions** | CI/CD pipelines                    |

---

## Repository Structure

```
family-finance/
├── frontend/           # Next.js web application
│   ├── app/            # App Router pages and components
│   ├── docs/           # Frontend documentation
│   └── public/         # Static assets
│
├── backend/            # NestJS API server
│   ├── src/            # Application source code
│   │   ├── modules/    # Feature modules (auth, accounts, transactions, etc.)
│   │   ├── common/     # Shared utilities, filters, pipes
│   │   └── database/   # Database service and configuration
│   ├── prisma/         # Database schema and migrations
│   └── docs/           # Backend documentation
│
├── api-gateway/        # NGINX reverse proxy
│   ├── conf.d/         # Server configuration
│   └── ssl/            # SSL certificates
│
├── global-compose/     # Full-stack Docker orchestration
│   └── docker-compose.yml
│
└── .github/            # Organization profile
    └── profile/README.md
```

---

## Getting Started

### Prerequisites

- **Node.js** 18.17 or later
- **Docker** v20.10 or later (for containerized deployments)
- **Docker Compose** v2.0 or later
- **Git**

---

## Running the Application

### Option 1: Full Stack with Docker Compose (Recommended)

The easiest way to run the entire application with all dependencies.

#### Steps

```bash
# 1. Clone all repositories
mkdir family-finance && cd family-finance
git clone https://github.com/family-finance-app/backend.git
git clone https://github.com/family-finance-app/frontend.git
git clone https://github.com/family-finance-app/api-gateway.git
git clone https://github.com/family-finance-app/global-compose.git

# 2. Configure environment
cd global-compose
cp .env.example .env
# Edit .env with your settings (especially JWT_SECRET)

# 3. Start all services
docker compose up -d --build

# 4. Apply database migrations
docker exec family-finance-backend npm run migrate:prod

# 5. Access the application
# Frontend:  http://localhost:3500
# Backend:   http://localhost:3000
# API Docs:  http://localhost:3000/api
# Gateway:   http://localhost
```

#### Useful Commands

```bash
# View logs
docker compose logs -f

# Stop services
docker compose down

# Restart a service
docker compose restart backend

# Reset database (CAUTION: deletes data)
docker compose down -v && docker compose up -d
```

📖 **Full documentation:** [global-compose/README.md](https://github.com/family-finance-app/global-compose)

---

### Option 2: Backend with Docker (Backend + Database + Redis)

Run the backend API with its dependencies in containers.

#### Steps

```bash
# 1. Clone and enter backend
git clone https://github.com/family-finance-app/backend.git
cd backend

# 2. Configure environment
cp .env.example .env
# Edit .env with your database credentials

# 3. Start backend stack
docker compose up -d --build

# 4. Apply migrations
docker exec backend npm run migrate:prod

# 5. Verify
curl http://localhost:3000/health
```

#### Access Points

- **API:** http://localhost:3000
- **Swagger Docs:** http://localhost:3000/api
- **Health Check:** http://localhost:3000/health
- **Metrics:** http://localhost:3000/metrics

📖 **Full documentation:** [backend/README.md](https://github.com/family-finance-app/backend)

---

### Option 3: Backend Local Development (Hot Reload)

Run the backend with live-reload for development. Requires external PostgreSQL.

#### With Docker Redis Only

```bash
cd backend
docker compose -f docker-compose.local.yml up -d

# Run backend with hot reload
npm install
npm run dev
```

#### Fully Local (No Docker)

```bash
cd backend
npm install
cp .env.example .env
# Configure DATABASE_URL, REDIS_HOST, etc.

npm run build
npm start
```

📖 **Full documentation:** [backend/README.md](https://github.com/family-finance-app/backend)

---

### Option 4: Frontend Only

Run just the frontend application. Requires a running backend.

#### Development Mode

```bash
git clone https://github.com/family-finance-app/frontend.git
cd frontend

npm install
cp .env.example .env
# Set NEXT_PUBLIC_BACKEND_URL to your backend URL

npm run dev
```

**Access:** http://localhost:3500

#### Production Build

```bash
npm run build
npm run start
```

#### Deploy to Cloudflare

```bash
npm run deploy:cloudflare
```

📖 **Full documentation:** [frontend/README.md](https://github.com/family-finance-app/frontend)

---

### Option 5: Full Stack with API Gateway

Production-like setup with NGINX reverse proxy for TLS termination and routing.

#### Steps

```bash
# 1. Create shared network
docker network create family-finance-network

# 2. Start backend (from backend directory)
cd backend
docker compose up -d

# 3. Start API Gateway (from api-gateway directory)
cd ../api-gateway
docker compose up -d

# 4. Start frontend (from frontend directory)
cd ../frontend
npm install && npm run dev
```

#### Access Points

- **Gateway:** http://localhost (routes to backend)
- **Backend Direct:** http://localhost:3000
- **Frontend:** http://localhost:3500

📖 **Full documentation:** [api-gateway/README.md](https://github.com/family-finance-app/api-gateway)

---

## Quick Reference: All Startup Options

| Option                  | What's Running                                    | Best For                         |
| ----------------------- | ------------------------------------------------- | -------------------------------- |
| **Full Stack (Docker)** | Frontend + Backend + Gateway + PostgreSQL + Redis | Production-like testing, demos   |
| **Backend Docker**      | Backend + PostgreSQL + Redis                      | Backend development, API testing |
| **Backend Local**       | Backend only (external DB)                        | Backend hot-reload development   |
| **Frontend Only**       | Next.js app                                       | Frontend development             |
| **With Gateway**        | Backend + Gateway + PostgreSQL + Redis            | Testing proxy configuration      |

---

## API Documentation

Interactive API documentation is available via Swagger at `/api` when the backend is running.

### Core Endpoints

| Domain           | Endpoint                   | Method | Description                   |
| ---------------- | -------------------------- | ------ | ----------------------------- |
| **Health**       | `/health`                  | GET    | Health check (DB + Redis)     |
| **Metrics**      | `/metrics`                 | GET    | Prometheus metrics            |
| **Auth**         | `/auth/signup`             | POST   | Register new user             |
|                  | `/auth/login`              | POST   | Login, returns tokens         |
|                  | `/auth/refresh`            | POST   | Refresh access token          |
|                  | `/auth/logout`             | POST   | Logout, revokes refresh token |
|                  | `/auth/me`                 | GET    | Get current user profile      |
| **Accounts**     | `/accounts/my`             | GET    | List user's accounts          |
|                  | `/accounts/create`         | POST   | Create new account            |
|                  | `/accounts/:id`            | PUT    | Update account                |
|                  | `/accounts/:id`            | DELETE | Delete account (cascades)     |
| **Transactions** | `/transactions/all`        | GET    | List user's transactions      |
|                  | `/transactions/create`     | POST   | Create income/expense         |
|                  | `/transactions/transfer`   | POST   | Transfer between accounts     |
|                  | `/transactions/update`     | PUT    | Update transaction            |
|                  | `/transactions/delete/:id` | DELETE | Delete transaction            |
| **Categories**   | `/categories`              | GET    | List all categories           |
| **User**         | `/user/profile`            | PUT    | Update profile                |
|                  | `/user/password`           | PUT    | Change password               |
|                  | `/user/email`              | PUT    | Change email                  |

---

## Database Schema

### Key Entities

| Entity          | Description                                      |
| --------------- | ------------------------------------------------ |
| **User**        | User accounts with credentials and profile       |
| **Account**     | Financial accounts (bank, cash, credit, etc.)    |
| **Transaction** | Income, expense, and transfer records            |
| **Category**    | Transaction classification with icons and colors |
| **Group**       | Family/team grouping (WIP)                       |
| **Goal**        | Savings targets and progress tracking (WIP)      |

### Supported Enums

| Enum                | Values                                                           |
| ------------------- | ---------------------------------------------------------------- |
| **AccountType**     | DEBIT, CREDIT, CASH, BANK, INVESTMENT, DEPOSIT, DIGITAL, SAVINGS |
| **CurrencyType**    | UAH, USD, EUR                                                    |
| **TransactionType** | EXPENSE, INCOME, TRANSFER                                        |

---

## Environment Variables

### Backend

| Variable                 | Required | Default     | Description                  |
| ------------------------ | -------- | ----------- | ---------------------------- |
| `NODE_ENV`               | No       | development | Environment mode             |
| `PORT`                   | No       | 3000        | API server port              |
| `DATABASE_URL`           | Yes      | -           | PostgreSQL connection string |
| `JWT_SECRET`             | Yes      | -           | Secret for signing tokens    |
| `JWT_EXPIRES_IN`         | No       | 1h          | Access token TTL             |
| `JWT_REFRESH_EXPIRES_IN` | No       | 7d          | Refresh token TTL            |
| `REDIS_HOST`             | Yes      | -           | Redis hostname               |
| `REDIS_PORT`             | No       | 6379        | Redis port                   |
| `REDIS_PASSWORD`         | No       | -           | Redis password               |
| `POSTGRES_DB`            | Yes      | -           | Database name                |
| `POSTGRES_USER`          | Yes      | -           | Database username            |
| `POSTGRES_PASSWORD`      | Yes      | -           | Database password            |

### Frontend

| Variable                  | Required | Description     |
| ------------------------- | -------- | --------------- |
| `NEXT_PUBLIC_BACKEND_URL` | Yes      | Backend API URL |

---

## Contributing

1. Fork the relevant repository
2. Create a feature branch from `develop`
3. Make your changes following the existing code style
4. Run tests and linting
5. Submit a pull request

### Code Style

- **TypeScript** for all source code
- **ESLint** for code linting
- **Prettier** for formatting
- Controllers remain thin; business logic in services

---

## License

Private project. Redistribution is not permitted without prior approval.
