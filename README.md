# 🏭 Enterprise Warehouse Management System (WMS)

[🇮🇷 نسخه فارسی](README_FA.md)

![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter)
![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?logo=postgresql)
![License](https://img.shields.io/badge/License-MIT-green)

A production-ready, highly scalable Warehouse Management System designed to handle complex inventory operations across a multi-level hierarchy. Built with a **Clean Architecture** backend and an **Event-Sourced** database engine to ensure 100% data integrity, full audit trails, and zero data loss.

> **Note:** This project was designed with a Farsi (RTL) UI as the primary interface, demonstrating internationalization and localization capabilities.

---

## 📸 Application Mockups

| Login & Dashboard | Warehouse Inventory | Transfer & Stock Validation |
| :---: | :---: | :---: |
| ![login](https://github.com/user-attachments/assets/505d91c6-725c-4493-abfa-31f605f3a0b3) | ![Warehouses](https://github.com/user-attachments/assets/3396791d-8f74-4cb8-a3d2-420d56fccc2b) | ![Transfers](https://github.com/user-attachments/assets/51d426f3-5192-4dfd-8038-dbbfd5ddfa12) |

---

## ✨ Key Features

- **4-Level Warehouse Hierarchy:** Strict enforcement of inventory flow (Central → Regional → Local → Disposed/Consumed) using PostgreSQL triggers.
- **Event Sourcing Engine:** Immutable audit log. Every stock movement is recorded as an event. Automated snapshotting every 100 events.
- **Real-time Stock Validation:** The UI prevents users from transferring more stock than available, updating dynamically as they type.
- **Instant Farsi Search:** Debounced search with Arabic-to-Farsi Unicode normalization for flawless Persian text querying.
- **Offline-First Caching:** Transfer history implements a Stale-While-Revalidate (SWR) pattern using local storage for instant offline access.
- **Daily JSON Dumps:** Automated daily export of the event store to JSON files for external backups and data lakes.

---

## 🏗️ System Architecture

This project strictly follows **Clean Architecture** and **Domain-Driven Design (DDD)** principles.

#### Backend (ASP.NET Core 8)
- **API Layer:** RESTful endpoints, JWT Authentication, Swagger UI.
- **Application Layer:** Use cases, DTOs, Business Logic interfaces.
- **Infrastructure Layer:** Entity Framework Core, Repository implementations.
- **Domain Layer:** Aggregates, Enums, pure business entities.

#### Database (PostgreSQL 16)
- **Triggers & Stored Procedures:** Business logic (e.g., stock deduction, hierarchy validation) is offloaded to the DB level using `pg_advisory_xact_lock` to prevent race conditions.
- **Materialized Views:** Pre-calculated aggregate data for lightning-fast reporting.
- **Native Enums:** Strict type checking for roles and warehouse levels.

#### Frontend (Flutter)
- **State Management:** `flutter_bloc` (Event-Driven UI).
- **Networking:** `Dio` with interceptors for automated JWT injection and 401 Auto-Logout.
- **UI/UX:** Custom theming, RTL support, Vazirmatn font, glassmorphism design.

---

## 🗄️ Database & Event Sourcing

Instead of standard CRUD operations that overwrite data, this system uses an append-only event store.

1. **Command:** User requests a stock transfer.
2. **Event Appended:** `TransferCreated`, `StockDecreased`, and `StockIncreased` events are appended to the `events` table.
3. **Projection:** The `warehouse_inventory` (Read Model) table is updated atomically within the same transaction.
4. **Snapshot:** If the aggregate version hits a multiple of 100, a snapshot is auto-generated to speed up future state rebuilds.

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| **Frontend** | Flutter, Dart, BLoC, Dio, SharedPreferences |
| **Backend** | ASP.NET Core 8, C#, EF Core 8 |
| **Database** | PostgreSQL 16, PL/pgSQL |
| **Architecture**| Clean Architecture, Event Sourcing, CQRS-lite |
| **DevOps** | Docker, Nginx |

---

## 📁 Project Structure

```
WMS/
├── WMS.API/                # Presentation layer — RESTful endpoints, JWT auth, Swagger
├── WMS.Application/        # Use cases, DTOs, business logic interfaces
├── WMS.Domain/             # Aggregates, enums, pure domain entities
├── WMS.Infrastructure/     # EF Core, repository implementations, PostgreSQL
└── wms_app/                # Flutter mobile client
    └── lib/
        ├── core/           # Theme, API client, shared constants
        └── features/       # Auth, Warehousing, Transfers (BLoC + Pages)
```

---

## 📄 License

This project is licensed under the MIT License.

