# News Scraping API — Performance & Security Enhanced

A Node.js + Express + MongoDB news scraping API with production-ready performance and security improvements.

---

## 🚀 Features

### Reliability & Performance
- **Timeouts + Retries + Circuit Breaker**
  - Prevents frequent scraping failures (connection reset / recv failure).
  - Uses retry with exponential backoff and circuit breaker for unstable sources.

- **Queue / Worker Pool**
  - Heavy scraping jobs run in background workers (BullMQ + Redis or worker_threads).
  - Keeps HTTP request threads responsive.

- **Caching (Redis / In-Memory)**
  - Cache responses by URL or query parameters with TTL.
  - Reduces repeated scraping and improves response time.

- **MongoDB Indexes + Pagination**
  - Indexes on `createdAt`, `source`, `category`.
  - Cursor-based pagination for large datasets.

- **Graceful Shutdown**
  - Handles `SIGINT` / `SIGTERM`.
  - Stops accepting new requests.
  - Waits for running jobs.
  - Closes DB and worker connections cleanly.

- **Defensive Programming**
  - Fixes `Cannot read properties of undefined (reading 'likes')` by:
    - Checking document existence.
    - Using schema defaults (e.g., `likes: { type: Number, default: 0 }`).

---

## 🔐 Security

- **Input Validation & Sanitization**
  - Joi / Zod for validation.
  - `express-mongo-sanitize` to prevent NoSQL injection.

- **Rate Limiting & Slow Down**
  - Protects sensitive endpoints like `/like` and `/scrape`.

- **Helmet + Proper CORS**
  - Secure HTTP headers.
  - Origin allowlist.

- **Authentication & Authorization**
  - JWT-based authentication.
  - Simple RBAC (user / admin).
  - Prevents anonymous users from modifying likes.

- **Secrets Management**
  - Environment variables via `.env`.
  - Secrets are never committed to GitHub.
  - Supports key rotation.

- **Logging & Audit**
  - Structured logging with Pino/Winston.
  - `requestId` per request.
  - No tokens or PII in logs.

---

## 🛠 Tech Stack

- Node.js + Express
- MongoDB + Mongoose
- Redis (Caching + BullMQ)
- Axios (HTTP)
- worker_threads
- JWT Authentication
- Pino / Winston Logging

---

