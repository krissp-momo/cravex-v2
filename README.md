# Cravex: Campus Food Ordering System

> Browse menus, place orders and track campus food from your phone. Skip the line, pick up when it's marked **Ready**.

**Note:** This README documents the planned scope, architecture, and development roadmap for Cravex v2. Features and technical details described here represent the current plan and may change during implementation.

**Status:** Solo rebuild in progress (v2)  |  **v1 :**  [View v1 source code](https://github.com/Animesh26526/Cravex-campus-food-ordering-system)

Cravex v1 was built as a 3-member Database Management System course project. v2 is a ground-up rebuild by me, following a full software-engineering process: Agile sprints, a written SRS, UML design, automated tests and documented retrospectives.

---

## Problem

Campus canteens have high-volume student traffic but rigid, manual ordering and payment, so students lose time in long queues during short breaks.

## Solution

Students browse menus, place orders from their phones, then track their orders until they are marked **Ready**. Shop staff get a simple dashboard to update order status.

## Features (Planned)

* Role-based accounts: **student** and **shop staff**
* Menu browsing with search and filters (category, veg/non-veg, price, availability)
* Persistent cart and **transactional checkout** (order + items + status history in one atomic step)
* 5-stage order lifecycle: `received -> accepted -> preparing -> ready -> completed`
* Unique pickup code per order
* Shop dashboard: incoming orders, status updates, menu management, open/close toggle
* Reviews and ratings with consistent shop-rating aggregates
* Loyalty points
* Full audit log of every status change

## What's planned for v2 (improvements over v1)

| Area             | v1 (course project) | v2 (planned improvements)                                        |
| ---------------- | ------------------- | ---------------------------------------------------------------- |
| Process          | Ad-hoc              | Agile sprints, SRS, UML, retrospectives                          |
| Password storage | SHA-256 hash        | bcrypt with salt                                                 |
| Auth             | Basic               | JWT + role-based middleware                                      |
| Testing          | Manual only         | Automated unit + integration tests (Jest, Supertest)             |
| Menu data        | Single SQL schema   | MongoDB catalog for flexible menu data (variants, add-ons, tags) |
| Status updates   | Page refresh        | Polling first, WebSocket upgrade planned                         |

## Tech stack

| Layer         | Choice                                                                      |
| ------------- | --------------------------------------------------------------------------- |
| Frontend      | React / Next.js                                                             |
| Backend       | Node.js + Express REST API                                                  |
| Relational DB | **MySQL**: users, shops, orders, order items, status history, cart, loyalty |
| Document DB   | **MongoDB**: menu catalog                                                   |
| Auth          | JWT, bcrypt                                                                 |
| Testing       | Jest, Supertest                                                             |
| Tooling       | Git/GitHub, Jira, draw.io (UML)                                             |

Why two databases? Orders require reliable transactional handling, so they are planned for MySQL. Menu items vary in shape (sizes, add-ons, tags), making MongoDB a potential fit for flexible menu documents. Order items will store a **snapshot** of item name and price, so past orders remain unchanged when a menu is edited.

## Documentation (software engineering artefacts)

| Document                                     | Contents                                                                     |
| -------------------------------------------- | ---------------------------------------------------------------------------- |
| [docs/SRS.md](docs/SRS.md)                   | Requirements analysis: FR/NFR, user stories, use cases                       |
| [docs/DESIGN.md](docs/DESIGN.md)             | Class design (CRC), sequence diagrams, activity diagram                      |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | Architecture style, component and deployment diagrams, data model            |
| [docs/TESTING.md](docs/TESTING.md)           | Test plan: unit, integration, system, bug report template                    |
| [ROADMAP.md](ROADMAP.md)                     | Agile roadmap, sprint plan, Kanban board, definition of done, retrospectives |

## Progress

* [ ] Sprint 0: Setup and SRS
* [ ] Sprint 1: Design and scaffolding
* [ ] Sprint 2: Core backend
* [ ] Sprint 3: Frontend and integration
* [ ] Sprint 4: Testing, quality, deployment
* [ ] Sprint 5: Final documentation and demo

## Future Scope

* **Online Payment Integration:** Integrate a payment gateway to enable students to pay for their campus food orders online.

## Getting started

Setup instructions will be added after the initial project structure and development scripts are in place.

## Planned project structure

```text
cravex/
  client/            # Next.js frontend
  server/
    src/
      routes/        # Express routes
      controllers/   # request handling
      services/      # business logic (checkout, status transitions)
      repositories/  # MySQL and MongoDB access
      middleware/    # auth, role guard, validation
    tests/           # unit and integration tests
  docs/              # SRS, design, architecture, testing
  ROADMAP.md
```

## Credits

Cravex v1 was built by Animesh, Shourya and Krishna for the DBMS course at PDEU. v2 is a solo rebuild by Krishna Patel.
