# Family Finance

A comprehensive family financial management application built with modern web technologies. This platform enables families to collaboratively manage their finances, track expenses, set budgets, and achieve financial goals together.

## Features

### Core Functionality

- **Multi-user Family Groups** - Create and manage family financial groups with multiple members (WIP)
- **Account Management** - Track multiple bank accounts, credit cards, and financial accounts
- **Transaction Tracking** - Record and categorize income and expenses across all family members
- **Budget Planning** - Set and monitor budgets for different categories and family members (WIP)
- **Financial Goals** - Create shared financial goals and track progress towards achieving them (WIP)
- **Expense Categories** - Organize transactions with customizable categories

## Architecture

Family Finance follows a modern microservices-inspired architecture with a monolithic backend for simplicity and performance.

```
family-finance/
├── frontend/             # Next.js React application
├── backend/              # NestJS monolithic API server
├── api-gateway/          # Nginx reverse proxy
├── postgres-db/          # PostgreSQL database
└── global-compose/       # Global Docker orchestration
```

### Technology Stack

#### Frontend

- **Next.js 14** - React framework with App Router
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first CSS framework
- **React Hooks** - Modern React patterns
- **Sentry** - Error monitoring and performance tracking

#### Backend

- **NestJS** - Scalable Node.js framework
- **Prisma** - Modern database ORM
- **PostgreSQL** - Reliable relational database
- **JWT** - Secure authentication
- **Argon2** - Password hashing
- **TypeScript** - End-to-end type safety

#### Infrastructure

- **Docker** - Containerization
- **Nginx** - Reverse proxy and load balancing
- **Docker Compose** - Multi-container orchestration

## Getting Started

### Prerequisites

- Node.js 18+
- Docker and Docker Compose
- Git

### Quick Start

1. **Clone the repositories**

   ```bash
   git clone https://github.com/family-finance-app/backend.git
   git clone https://github.com/family-finance-app/frontend.git
   # Clone other service repositories as needed
   ```

2. **Start the database**

   ```bash
   cd postgres-db
   docker-compose up -d
   ```

3. **Start the backend services**

   ```bash
   cd backend-compose
   docker-compose up -d
   ```

4. **Start the frontend**

   ```bash
   cd frontend
   npm install
   npm run dev
   ```

5. **Access the application**
   - Frontend: http://localhost:3000
   - API: http://localhost/api
   - Database: localhost:5432

### Development Setup

#### Backend Development

```bash
cd backend
npm install
npm run prisma:generate
npm run prisma:migrate
npm run dev
```

#### Frontend Development

```bash
cd frontend
npm install
npm run dev
```

## API Documentation

The Family Finance API provides comprehensive endpoints for all financial operations:

### Authentication

- `POST /api/auth/signup` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/refresh` - Token refresh
- `POST /api/auth/logout` - User logout

### Accounts Management

- `GET /api/accounts` - List user accounts
- `POST /api/accounts` - Create new account
- `PUT /api/accounts/:id` - Update account
- `DELETE /api/accounts/:id` - Delete account

### Transactions

- `GET /api/transactions` - List transactions
- `POST /api/transactions` - Create transaction
- `PUT /api/transactions/:id` - Update transaction
- `DELETE /api/transactions/:id` - Delete transaction

### Family Groups

- `GET /api/groups` - List family groups
- `POST /api/groups` - Create family group
- `POST /api/groups/:id/members` - Add family member

## Database Schema

The application uses PostgreSQL with a comprehensive schema supporting:

- **Users** - User accounts and authentication
- **Groups** - Family financial groups
- **Accounts** - Bank accounts and financial accounts
- **Transactions** - Financial transactions and transfers
- **Categories** - Expense and income categories
- **Goals** - Financial goals and targets
- **Notifications** - System and user notifications

## Security

- **Authentication** - JWT-based with refresh tokens
- **Authorization** - Role-based access control
- **Data Protection** - Encrypted sensitive data
- **HTTPS** - SSL/TLS encryption
- **Input Validation** - Comprehensive request validation
- **CORS** - Properly configured cross-origin requests

````

### Environment Variables

```env
# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/family_finance

# Authentication
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=1h
JWT_REFRESH_EXPIRES_IN=7d

# Application
NODE_ENV=production
PORT=3000
````

## Architecture Migration

This project recently migrated from a microservices architecture to a monolithic backend for improved development velocity and simplified deployment. The migration consolidated:

- **auth-service** → `backend/src/modules/auth/`
- **account-service** → `backend/src/modules/accounts/`
- **transaction-service** → `backend/src/modules/transactions/`

All services now share a unified database connection and benefit from simplified inter-service communication.
