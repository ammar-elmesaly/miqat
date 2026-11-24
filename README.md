# Miqat (ميقات)

> A unified, cross-platform time-management workspace combining project categorization, task tracking, agenda scheduling, and an integrated Pomodoro focus timer.

![Version](https://img.shields.io/badge/version-1.4-2563EB?style=flat-square)
![Backend](https://img.shields.io/badge/backend-NestJS%20%2F%20Express-0F172A?style=flat-square)
![Web](https://img.shields.io/badge/web-Next.js-2563EB?style=flat-square)
![Mobile](https://img.shields.io/badge/mobile-Flutter-0F172A?style=flat-square)
![Database](https://img.shields.io/badge/database-PostgreSQL-2563EB?style=flat-square)

---

## Overview

**Miqat (ميقات)** is built as a Software Engineering Lab project demonstrating multi-tier architecture, RESTful API design, relational database modeling, and cross-platform client integration across Web and Mobile.

### Core Features

* **Authentication:** Stateless JWT-based user registration and login across Web and Mobile.
* **Project Categorization:** Create and manage color-coded projects to organize workloads.
* **Task Management (CRUD):** Create, read, update, and delete tasks with filtering by project, priority, due date, and completion status.
* **Integrated Pomodoro Timer:** Interactive 25-minute focus / 5-minute break countdown timer that logs completed focus sessions directly against specific tasks.
* **Agenda & Calendar View:** Visual daily and weekly task breakdown ordered by due date.
* **Adaptive Theme System:** Seamless Light (`#F8FAFC`) and Slate Dark (`#0F172A`) mode toggling with local state persistence (`localStorage` on Web, `SharedPreferences` on Mobile).

---

## Tech Stack

| Layer | Technology | Role |
| :--- | :--- | :--- |
| **Web Client** | React / Next.js (TypeScript) | Responsive desktop & web dashboard |
| **Mobile App** | Flutter (Dart) | Cross-platform iOS & Android client |
| **Backend API** | NestJS / Express.js (TypeScript) | Modular REST API & business logic |
| **Database** | PostgreSQL (Prisma / TypeORM) | Relational persistence (`Users`, `Projects`, `Tasks`, `FocusSessions`) |
| **Auth** | JSON Web Tokens (JWT) | Stateless authentication & route guards |

---

## Repository Structure

```text
miqat/
├── docs/
│   ├── diagrams/                # UML Use Case & Sequence diagrams (.simp, .drawio)
│   │   ├── sequence/
│   │   └── use-case-diagram.simp
│   └── prd.md                   # Product Requirements Document (v1.4)
├── backend/                     # TypeScript REST API (Auth, Projects, Tasks, Agenda, Pomodoro)
├── web/                         # Next.js web application
├── mobile/                      # Flutter mobile application
├── .gitignore
└── README.md
```

---

## REST API Reference

### Authentication
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new user account |
| `POST` | `/api/auth/login` | Authenticate user and issue JWT |

### Projects
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/projects` | Retrieve all projects for the authenticated user |
| `POST` | `/api/projects` | Create a new project with a custom color badge |
| `DELETE` | `/api/projects/:id` | Delete a project |

### Tasks
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/api/tasks` | List tasks (supports `?status=`, `?projectId=`, `?dueDate=`) |
| `POST` | `/api/tasks` | Create a new task |
| `PUT` | `/api/tasks/:id` | Update task details, priority, or completion status |
| `DELETE` | `/api/tasks/:id` | Delete a task |

### Focus Sessions (Pomodoro)
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/sessions` | Log a completed Pomodoro focus session |
| `GET` | `/api/sessions/summary` | Fetch total session counts and focus durations |

---

## Getting Started

### Prerequisites
* **Node.js** (`>= 18.x`) & **npm** / **pnpm**
* **PostgreSQL** (`>= 14.x`)
* **Flutter SDK** (`>= 3.x`)

### 1. Backend Setup
```bash
cd backend
cp .env.example .env   # Configure DATABASE_URL and JWT_SECRET
npm install
npx prisma migrate dev # Or run TypeORM migrations
npm run start:dev
```

### 2. Web Client Setup
```bash
cd web
cp .env.example .env.local # Set NEXT_PUBLIC_API_URL=http://localhost:3000/api
npm install
npm run dev
```

### 3. Mobile App Setup
```bash
cd mobile
flutter pub get
flutter run
```

---

## Development Roadmap

- [x] **Phase 0:** UML Use Case & Sequence Diagrams + PRD Specification (`docs/`)
- [ ] **Sprint 1:** Database schema, JWT Auth API, and base Web/Mobile clients with theme switching
- [ ] **Sprint 2:** Projects & Tasks CRUD endpoints, filtering, and UI boards
- [ ] **Sprint 3:** Interactive Pomodoro timer, session logging, and Agenda view
- [ ] **Sprint 4:** End-to-end integration testing, Postman collection, and UI polish

---

## Documentation

* [Product Requirements Document (`docs/prd.md`)](./docs/prd.md)
* [مستند متطلبات المنتج (بالعربية) (`docs/prd-arabic.md`)](./docs/prd-arabic.md)
* [System UML Diagrams (`docs/diagrams/`)](./docs/diagrams/)