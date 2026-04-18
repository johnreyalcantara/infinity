You are a senior software architect. Design a production-ready SaaS system called "Infinity".

## 🎯 Goal
Infinity is a multi-tenant SaaS platform where businesses can register and choose a system type (e.g., Sales/POS, Rental System, Inventory System). Each business gets its own isolated workspace, users, branches, and data.

The platform must support offline-first mobile apps (Android initially), with reliable synchronization when internet is available.

This system MUST be designed with strong emphasis on:
- Offline sync reliability
- Multi-tenant data isolation
- Clean, scalable architecture

---

## 🧱 CORE REQUIREMENTS

### 1. Multi-Tenant Architecture (CRITICAL)
- Each business = one tenant
- STRICT data isolation between tenants
- Support scaling to thousands of tenants

Provide and compare:
- Shared DB with tenant_id
- Separate DB per tenant
- Hybrid approach

Explain:
- Security implications
- Performance tradeoffs
- Recommended approach for MVP vs scaling stage

---

### 2. System Modules (Pluggable Architecture)
Each tenant selects a system type:
- Sales / POS System (PRIMARY MVP)
- Rental System
- Inventory Management
- (Suggest additional modules)

Each module must:
- Be modular and loosely coupled
- Share core services (auth, billing, sync)
- Be extendable without breaking existing modules

---

### 3. User Roles & Access Control
- Super Admin (platform owner)
- Business Owner (tenant admin)
- Staff (cashier, encoder, etc.)

Requirements:
- Role-Based Access Control (RBAC)
- Owner can create users and assign permissions
- Branch-level access restrictions

---

### 4. Mobile App (Offline-First Design) ⚠️ HIGH PRIORITY

Platform must support Android app (Kotlin or Flutter).

Core Features:
- Works WITHOUT internet
- Local database (SQLite / Room / Hive)
- Transactions saved locally first
- Manual SYNC button
- Background sync (optional future)

CRITICAL: Design for OFFLINE SYNC RELIABILITY

Include:
- Local transaction log / event queue
- Idempotency keys
- Retry mechanisms
- Conflict resolution strategy:
  - last-write-wins OR merge-based
- Handling:
  - duplicate transactions
  - partial sync failures
  - corrupted data recovery

Provide a step-by-step sync flow.

---

### 5. POS System Features (MVP Module)

Include:
- Product management (CRUD)
- Inventory tracking
- Barcode scanning support
- Point of Sale interface
- Receipt printing (Bluetooth printers)
- Daily sales auto-close (end-of-day reconciliation)
- Expense tracking
- Sales reports

---

### 6. Multi-Branch Support
- A tenant can have multiple branches
- Each branch:
  - has its own inventory
  - has its own staff
  - tracks its own sales
- Owner can view consolidated + per-branch reports

---

### 7. Backend System

Recommend stack (justify choice):
- Node.js (NestJS) OR Java (Spring Boot)

Architecture:
- Prefer Modular Monolith for MVP
- Explain migration path to Microservices

Core Services:
- Authentication Service
- Tenant Management Service
- Product & Inventory Service
- Transaction Service
- Expense Service
- Sync Service (CRITICAL)
- Reporting & Analytics Service
- Billing & Subscription Service

---

### 8. Subscription Billing System
- Monthly SaaS subscription model
- Tenant subscription plans (Basic, Pro, Enterprise)
- Feature-based access control
- Payment integration (suggest providers)
- Trial periods and account suspension

---

### 9. Cloud Backup & Sync
- Automatic cloud backup when online
- Manual sync trigger
- Data recovery strategy
- Backup versioning

---

### 10. Database Design

Recommend:
- PostgreSQL (main database)
- Redis (cache, queues, session store)

Core tables:
- tenants
- branches
- users
- roles
- products
- inventory
- transactions
- expenses
- subscriptions
- sync_logs

Requirements:
- tenant_id in all tables
- branch_id where applicable
- audit logs
- soft deletes

---

### 11. API Design
- REST or GraphQL (justify choice)
- Secure endpoints using JWT
- Rate limiting
- Request validation
- Logging & monitoring

Provide sample endpoints.

---

### 12. Admin Dashboard (Web)

Super Admin:
- View all tenants
- Monitor system health
- Manage subscriptions
- Control platform features

Business Owner Dashboard:
- Sales analytics
- Top-selling products
- Low-stock alerts
- Expense tracking overview
- Multi-branch insights

Frontend:
- React / Next.js recommended

---

### 13. Deployment & Infrastructure

Recommend:
- AWS / GCP
- Docker containers
- CI/CD pipeline

Components:
- API servers
- Database cluster
- Object storage (receipts, images)
- CDN
- Load balancer

---

### 14. Security (CRITICAL)
- Strong tenant isolation enforcement
- Encrypted communication (HTTPS)
- Password hashing (bcrypt)
- Role-based authorization
- Input validation & sanitization

---

### 15. Scalability & Clean Architecture ⚠️ HIGH PRIORITY

Design system to scale cleanly:
- Avoid tight coupling
- Use domain-driven design (DDD)
- Separation of concerns
- Event-driven patterns (if needed)

Explain:
- How system scales from 10 → 10,000 tenants
- Bottlenecks and mitigation strategies

---

## 📊 OUTPUT FORMAT

Provide:

1. High-level architecture diagram (text-based)
2. Detailed component breakdown
3. Database schema (tables + relationships)
4. API structure (sample endpoints)
5. Offline sync flow (step-by-step, detailed)
6. Multi-tenant strategy comparison + recommendation
7. Tech stack justification
8. MVP scope vs future expansion

Be specific, practical, and production-ready.
Avoid generic explanations.

make sure to have perfect database schema + sync model first