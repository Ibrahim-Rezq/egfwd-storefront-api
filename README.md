# Storefront Backend API

## 📋 Project Overview

A RESTful API for an online storefront application built with **Node.js**, **Express**, and **PostgreSQL**. The application was provided as a starter by **Udacity** as part of the Full Stack JavaScript Nanodegree Program. This project demonstrates backend development skills including database design, API endpoint creation, authentication with JWT, password hashing with bcrypt, and comprehensive testing with Jasmine.

---

## 🛠️ Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **TypeScript** - Type-safe JavaScript

### Database
- **PostgreSQL** - Relational database
- **db-migrate** - Database migrations

### Security & Authentication
- **JWT (jsonwebtoken)** - Token-based authentication
- **bcrypt** - Password hashing

### Testing
- **Jasmine** - Testing framework
- **Supertest** - HTTP assertions

### Development Tools
- **nodemon** - Auto-restart server
- **tsc-watch** - TypeScript watch mode
- **dotenv** - Environment variables

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- PostgreSQL (v12 or higher)
- npm or yarn

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Ibrahim-Rezq/egfwd-storefront-api.git
cd egfwd-storefront-api
```

2. **Install dependencies**
```bash
npm install
```

3. **Database Setup**

Create the development and test databases:
```sql
CREATE DATABASE storefront;
CREATE DATABASE storefront_test;
```

4. **Environment Configuration**

Create a `.env` file in the root directory:
```env
POSTGRES_HOST=127.0.0.1
POSTGRES_DB=storefront
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
POSTGRES_TEST_DB=storefront_test

ENV=dev
TOKEN_SECRET=secretjwt
BCRYPT_PASSWORD=your-secret-password
SALT_ROUNDS=10

TEST_TOKEN=your-test-token-here
```

5. **Run Migrations**
```bash
npm run up
```

---

## 📜 Available Scripts

| Script | Command | Description |
|--------|---------|-------------|
| Install | `npm install` | Install all dependencies |
| Migrate Up | `npm run up` | Run database migrations |
| Migrate Down | `npm run down` | Rollback database migrations |
| Development | `npm run start-dev` | Start server with nodemon |
| Watch | `npm run watch` | TypeScript watch mode |
| Build | `npm run build` | Compile TypeScript to JavaScript |
| Start | `npm run start` | Build and start production server |
| Test | `npm run test` | Run Jasmine tests (Windows) |
| Test (Fix) | `npm run test-fix` | Run tests (Cross-platform) |

### 💡 Testing Note
If `npm run test` fails on your OS, use `npm run test-fix` instead and manually set `ENV=dev` in your `.env` file before running tests.

---

## 🔌 API Endpoints

### Products

| Endpoint | Method | Parameters | Auth Required | Description |
|----------|--------|------------|---------------|-------------|
| `/products` | GET | N/A | No | Get all products |
| `/products/:id` | GET | id | No | Get product by ID |
| `/products` | POST | name, price | Yes | Create new product |

### Users

| Endpoint | Method | Parameters | Auth Required | Description |
|----------|--------|------------|---------------|-------------|
| `/users` | GET | N/A | No | Get all users |
| `/users/:id` | GET | id | No | Get user by ID |
| `/users` | POST | firstname, lastname, username, password | No | Register new user |
| `/users/login` | POST | username, password | No | Login user (returns JWT) |

### Orders

| Endpoint | Method | Parameters | Auth Required | Description |
|----------|--------|------------|---------------|-------------|
| `/orders` | GET | N/A | No | Get all orders |
| `/orders/:id` | GET | id | No | Get order by ID |
| `/orders` | POST | amount, state, user_id | Yes | Create new order |

---

## 🗄️ Database Schema

### Products Table
```sql
Column | Type                   | Constraints
-------|------------------------|---------------------------
id     | INTEGER                | PRIMARY KEY, AUTO INCREMENT
name   | VARCHAR(100)           | 
price  | INTEGER                |
```

### Users Table
```sql
Column    | Type                   | Constraints
----------|------------------------|---------------------------
id        | INTEGER                | PRIMARY KEY, AUTO INCREMENT
firstname | VARCHAR(100)           |
lastname  | VARCHAR(100)           |
username  | VARCHAR(100)           |
password  | VARCHAR                | (hashed with bcrypt)
```

### Orders Table
```sql
Column | Type    | Constraints
-------|---------|---------------------------
id     | INTEGER | PRIMARY KEY, AUTO INCREMENT
state  | BOOLEAN |
user_id| INTEGER | FOREIGN KEY → users(id)
```

### Order_Products Table (Junction)
```sql
Column     | Type    | Constraints
-----------|---------|---------------------------
id         | INTEGER | PRIMARY KEY, AUTO INCREMENT
order_id   | INTEGER | FOREIGN KEY → orders(id)
product_id | INTEGER | FOREIGN KEY → products(id)
amount     | INTEGER |
```

---

## 🔐 Authentication

This API uses **JWT (JSON Web Tokens)** for authentication:

1. Register a new user via `POST /users`
2. Login via `POST /users/login` to receive a token
3. Include the token in the Authorization header for protected routes:
   ```
   Authorization: Bearer <your-token-here>
   ```

Passwords are hashed using **bcrypt** before storage.

---

## 🧪 Testing

The project includes comprehensive unit tests using Jasmine:

```bash
# Run all tests
npm run test

# For cross-platform compatibility
npm run test-fix
```

Tests cover:
- Model methods (CRUD operations)
- API endpoints
- Authentication flows
- Database interactions

---

## 📡 Server Information

- **Development Server**: `http://127.0.0.1:3000`
- **Database Host**: `localhost:5432`
- **Database Name**: `storefront`
- **Test Database**: `storefront_test`

---

## 📁 Project Structure

```
storefront-backend/
├── src/
│   ├── models/          # Database models
│   ├── handlers/        # Route handlers
│   ├── services/        # Business logic
│   ├── middleware/      # Auth middleware
│   ├── tests/           # Test specifications
│   └── server.ts        # Entry point
├── migrations/          # Database migrations
├── dist/                # Compiled JavaScript
├── .env                 # Environment variables
├── package.json
└── tsconfig.json
```

---

## 📝 Project Context

The base application structure was provided by **Udacity** as part of the Full Stack JavaScript Nanodegree Program.

**My Implementation:**
- Complete API endpoint development
- Database schema design and implementation
- JWT authentication system
- Password hashing with bcrypt
- Database migrations setup
- Comprehensive testing suite with Jasmine
- TypeScript configuration and implementation
- Error handling and validation
- RESTful API best practices

---

## 👤 Author

**Ibrahim Rezq**

- GitHub: [@Ibrahim-Rezq](https://github.com/Ibrahim-Rezq)
- Repository: [egfwd-storefront-api](https://github.com/Ibrahim-Rezq/egfwd-storefront-api)

**Role:** Backend Developer & API Implementation

---

## 🙏 Acknowledgments

- Udacity Full Stack JavaScript Nanodegree Program for providing the starter code
- PostgreSQL Documentation
- Express.js Documentation
- JWT Documentation

---

## 📄 License

Copyright © 2012 - 2020, Udacity, Inc.
This project contains educational content provided by Udacity and is subject to the Creative Commons Attribution-NonCommercial-NoDerivs 3.0 License (CC BY-NC-ND 3.0).


---

## 🔗 Additional Documentation

For detailed API requirements and specifications, please refer to the `REQUIREMENTS.md` file in the repository.
