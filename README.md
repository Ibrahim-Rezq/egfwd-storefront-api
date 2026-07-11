# Storefront API

Backend for an online store, from the EGFWD fullstack JavaScript track. Udacity provided the requirements and a bare starter; the database design, the endpoints, the auth, and the tests are mine.

It handles users, products, and orders. Passwords get hashed with bcrypt, protected routes want a JWT, and everything is covered by Jasmine tests with Supertest for the HTTP side.

## Setting it up

You'll need Node 14+ and PostgreSQL 12+.

```bash
git clone https://github.com/Ibrahim-Rezq/egfwd-storefront-api.git
cd egfwd-storefront-api
npm install
```

Create the two databases:

```sql
CREATE DATABASE storefront;
CREATE DATABASE storefront_test;
```

Then a `.env` file in the root:

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

Run the migrations and start:

```bash
npm run up          # migrations
npm run start-dev   # dev server with nodemon
```

Other scripts: `npm run build` compiles the TypeScript, `npm run start` builds and runs production, `npm run down` rolls migrations back, `npm run test` runs the Jasmine suite. If `npm run test` misbehaves on your OS, use `npm run test-fix` and set `ENV=dev` in `.env` yourself first.

## Endpoints

Products:

| Endpoint | Method | Body / params | Auth |
|----------|--------|---------------|------|
| `/products` | GET | | no |
| `/products/:id` | GET | id | no |
| `/products` | POST | name, price | yes |

Users:

| Endpoint | Method | Body / params | Auth |
|----------|--------|---------------|------|
| `/users` | GET | | no |
| `/users/:id` | GET | id | no |
| `/users` | POST | firstname, lastname, username, password | no |
| `/users/login` | POST | username, password | no |

Orders:

| Endpoint | Method | Body / params | Auth |
|----------|--------|---------------|------|
| `/orders` | GET | | no |
| `/orders/:id` | GET | id | no |
| `/orders` | POST | amount, state, user_id | yes |

Auth flow: register through `POST /users`, log in through `POST /users/login` to get a token, then send it as `Authorization: Bearer <token>` on protected routes.

## Database

Four tables: `products` (name, price), `users` (names, username, hashed password), `orders` (state, user_id), and an `order_products` junction table connecting orders to products with an amount. Migrations are handled with db-migrate.

## Stack

Node, Express, TypeScript, PostgreSQL. JWT and bcrypt for auth, Jasmine and Supertest for tests.
