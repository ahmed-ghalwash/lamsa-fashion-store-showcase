# Lamsa - Fashion E-Commerce

A minimal, editorial fashion shopping experience built around modern essentials.

Full-stack concept application: a **React 18** single-page client, a **PHP 8 REST API**
(framework-free, PDO with prepared statements) and a **MySQL** database.

## Features

- Catalog with category filter, search and price/newest sorting
- Server-side cart: variants are validated against the product, quantities capped
- Transactional checkout that recomputes totals from the products table
- Guarded stock decrement (UPDATE ... WHERE stock >= q) so items cannot be oversold
- Order history with snapshotted names and prices

## Interface

The client ships a hand-written motion layer - CSS keyframes plus a few small React
helpers, no animation library: staged entrances with per-card stagger, hover lift and
cover zoom, numbers that count up, charts that draw themselves, an animated seat map and
boarding pass, confetti only on real success states, and shimmering skeletons while a
request is in flight. All of it switches off under `prefers-reduced-motion: reduce`.

## Tech stack

| Layer | Tech |
| --- | --- |
| Front end | React 18, Vite, React Router |
| Back end | PHP 8.1+, PDO (native prepared statements), PHP sessions |
| Database | MySQL 8 (InnoDB, foreign keys, transactions) |

## Screenshots

| Screen | Desktop | Mobile |
| --- | --- | --- |
| Storefront with filters | ![shop](screenshots/shop.png) | ![shop mobile](screenshots/shop-mobile.png) |
| Product detail with size and color | ![product](screenshots/product.png) | ![product mobile](screenshots/product-mobile.png) |
| Cart and checkout | ![cart](screenshots/cart.png) | ![cart mobile](screenshots/cart-mobile.png) |
| Order history | ![orders](screenshots/orders.png) | ![orders mobile](screenshots/orders-mobile.png) |

## Engineering

- **API test suite:** 24 end-to-end tests (79 assertions) that start the real PHP front controller and drive it over HTTP: registration and sessions, validation, ownership checks, cart rules, checkout totals and shipping, stock decrement and full rollback when an item sells out, order privacy and cancellation with restock. They run against SQLite so no database server is needed; real MySQL is covered by the smoke test below.
- **Docker Compose:** MySQL 8.4, the PHP API and nginx serving the React client start with one command.
- **CI (GitHub Actions):** PHP lint and tests on PHP 8.3, the client production build, and a Docker smoke test that boots the whole stack and checks health, registration and the session endpoint against real MySQL.
- **Endpoints added in this round:** `GET /api/orders/{id}`, `POST /api/orders/{id}/cancel` (stock goes back in the same transaction) and `GET /api/health`.

## Source code

The full source code for this project - the React client, the PHP REST API, and the
database schema with seed data - is kept in a **private repository**.

It is available on request: reach out through my
[GitHub profile](https://github.com/ahmed-ghalwash) and I will be happy to share it.
