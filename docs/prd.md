# Software Engineering Lab PRD: Miqat (ميقات)

**Project Name:** Miqat (ميقات)  
**Context:** University Software Engineering Lab / Course Project  
**Document Version:** 1.4 (Final Lab Specification)  
**Primary Color Theme:** Modern Electric Blue (`#2563EB`) with Slate Dark (`#0F172A`)

---

## 1. Project Overview

**Miqat (ميقات)** is a modern, unified time-management workspace designed to combine project categorization, task tracking, scheduling, and a Pomodoro focus timer into a single cohesive application.

The project demonstrates core software engineering principles, multi-tier architecture, RESTful API design, dark mode theme system implementation, and cross-platform frontend integration (Web & Mobile) within a university semester framework.

---

## 2. Project Goals & Non-Goals

To keep the project manageable for a university lab deadline and ensure clear assessment boundaries, the project scope is divided into explicit **Goals** and **Non-Goals**.

### 2.1 Primary Goals (Core MVP Deliverables)

* **Functional Authentication:** Implement secure JWT-based register and login flows for single-user accounts across both web and mobile.
* **Project Categorization:** Enable users to create and manage Projects with custom color codes to organize their workloads.
* **Full Task CRUD:** Provide robust Task management (Create, Read, Update, Delete) with filtering options by project, priority, and completion status.
* **Integrated Pomodoro Timer:** Implement an interactive 25-minute focus / 5-minute break countdown timer, with the ability to log focus sessions directly against specific tasks.
* **Basic Calendar/Agenda View:** Display tasks visually according to their due dates in a daily or weekly agenda format.
* **Dark Mode & Light Mode Theme Toggle:** Support a seamless UI theme switcher between a modern Light mode (Off-white/Blue) and Dark mode (`#0F172A` Slate Dark) across both Next.js Web and Flutter Mobile clients.
* **Cross-Platform Delivery:** Build a responsive web client (Next.js) and a mobile app (Flutter) that consume a shared backend REST API (NestJS or Express).

### 2.2 Stretch Goals (Post-MVP / Wish List)

* **Mobile Offline Caching (SQLite / `sqflite`):** Store tasks locally on the mobile device so users can view tasks offline, syncing with the backend when online.
* **Basic Productivity Analytics:** Display simple aggregated stats (e.g., total focus minutes per project).

### 2.3 Non-Goals (Explicitly Out of Scope)

* **Multi-User Collaboration:** No shared projects, real-time co-working, or team permission roles (strictly single-user per account).
* **Third-Party Calendar Integration:** No external sync with Google Calendar, Apple Reminders, or Outlook APIs.
* **Complex Real-Time Sync:** No WebSocket engine or complex conflict-resolution for live instant synchronization across simultaneous devices.
* **AI/Automated Scheduling:** No machine learning or automated task prioritization algorithms.
* **Production DevOps Infrastructure:** No complex microservices, Kubernetes clusters, or multi-stage CI/CD pipelines (local hosting and basic cloud deployment like Render/Vercel are sufficient).

---

## 3. Tech Stack Specification

| Layer | Technology | Key Responsibilities |
| :--- | :--- | :--- |
| **Frontend (Web)** | React / Next.js (TypeScript) | Web client, responsive desktop view, main dashboard, dark mode context. |
| **Frontend (Mobile)** | Flutter (Dart) | iOS & Android app, material/cupertino dark theme support. |
| **Backend API** | NestJS or Express.js (TypeScript) | Modular REST API server, authentication, business logic. |
| **Database** | PostgreSQL (TypeORM or Prisma) | Relational data storage (Users, Projects, Tasks, Focus Sessions). |
| **Authentication** | JWT (JSON Web Tokens) | Stateless user authorization. |

---

## 4. MVP Functional & Technical Requirements

### 4.1 Backend Architecture & Database Schema

#### **Database Entities**
1. **`User` Entity:** `id`, `email`, `password_hash`, `full_name`, `created_at`
2. **`Project` Entity:** `id`, `name`, `color_code`, `description`, `user_id` (FK)
3. **`Task` Entity:** `id`, `title`, `description`, `status`, `priority`, `due_date`, `project_id` (FK, nullable), `user_id` (FK)
4. **`FocusSession` Entity:** `id`, `duration_minutes`, `completed_at`, `task_id` (FK, optional), `user_id` (FK)

#### **REST API Routes**
* **Auth:**
  * `POST /api/auth/register` — Create account.
  * `POST /api/auth/login` — Return JWT.
* **Projects:**
  * `GET /api/projects` — Fetch user's projects.
  * `POST /api/projects` — Create project.
  * `DELETE /api/projects/:id` — Remove project.
* **Tasks:**
  * `GET /api/tasks` — Fetch user's tasks (filterable via query params: `?status=`, `?projectId=`, `?dueDate=`).
  * `POST /api/tasks` — Create task.
  * `PUT /api/tasks/:id` — Update status, priority, or details.
  * `DELETE /api/tasks/:id` — Delete task.
* **Focus Sessions:**
  * `POST /api/sessions` — Record a completed Pomodoro run.
  * `GET /api/sessions/summary` — Retrieve session counts and focus durations.

---

## 5. UI/UX & Theme Guidelines

* **Primary Color:** Modern Electric Blue (`#2563EB`)
* **Secondary Accent:** Slate Navy (`#1E293B`)
* **Light Theme Background:** Off-white (`#F8FAFC`)
* **Dark Theme Background:** Deep Slate (`#0F172A`)
* **Theme State Management:** Local preference persistence (localStorage on Web, SharedPreferences in Flutter) to store dark/light preference.
* **Visual Style:** Minimalist card-based layout, clear project color badges, modern rounded corners (`12px`), clean input forms.

---

## 6. Academic Evaluation & Success Metrics

| Metric Category | Standard / Target | Evaluation Method |
| :--- | :--- | :--- |
| **Functional Completeness** | 100% execution of core MVP Goals (Auth, Projects, Tasks, Timer, Dark Mode). | Live Lab Demo |
| **Software Architecture** | Proper layer separation (Controllers, Services, Repositories). | Source Code Review |
| **Database Design** | Properly normalized relational schema with FK constraints. | ERD / Schema Inspection |
| **API Quality** | Clean RESTful endpoints, appropriate HTTP status codes, error handling. | Postman Collection Test |
| **UI Polish & Themes** | Responsive Next.js Web UI & smooth Flutter Mobile screens with functioning dark/light mode toggle. | Visual Review |

---

## 7. 4-Sprint Development Roadmap

```
Sprint 1: System Design, Auth & Database Schema
├── Set up NestJS/Express, PostgreSQL, and Prisma/TypeORM
├── Implement User entity & JWT Auth endpoints (/register, /login)
└── Set up Next.js and Flutter base projects with API client and dark theme provider setup

Sprint 2: Projects & Tasks CRUD
├── Build Project & Task API endpoints
├── Implement Project creation and sidebar management (Web & Mobile)
└── Build Task management boards with Project filtering and Dark Mode styling

Sprint 3: Pomodoro Timer & Agenda View
├── Build interactive Pomodoro Timer component (Web & Mobile)
├── Connect timer completion logic to Backend Session API
└── Create Agenda/Calendar view displaying tasks by due date

Sprint 4: Integration, Polish & Submission Prep
├── Perform end-to-end integration testing (Web/Mobile -> Backend)
├── Finalize Dark/Light theme switching and UI polish
├── Document Postman API collection & repo README
└── [Optional Stretch Goal] Implement SQLite local caching on Mobile
```