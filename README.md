🏭 Enterprise Warehouse Management System (WMS)
Flutter.NETPostgreSQLLicense

A production-ready, highly scalable Warehouse Management System designed to handle complex inventory operations across a multi-level hierarchy. Built with a Clean Architecture backend and an Event-Sourced database engine to ensure 100% data integrity, full audit trails, and zero data loss.

Note: This project was designed with a Farsi (RTL) UI as the primary interface, demonstrating internationalization and localization capabilities.

📸 Application Mockups
Login & Dashboard	Warehouse Inventory	Transfer & Stock Validation
Login Screen	Warehouses	Transfers
✨ Key Features
4-Level Warehouse Hierarchy: Strict enforcement of inventory flow (Central → Regional → Local → Disposed/Consumed) using PostgreSQL triggers.
Event Sourcing Engine: Immutable audit log. Every stock movement is recorded as an event. Automated snapshotting every 100 events.
Real-time Stock Validation: The UI prevents users from transferring more stock than available, updating dynamically as they type.
Instant Farsi Search: Debounced search with Arabic-to-Farsi Unicode normalization for flawless Persian text querying.
Offline-First Caching: Transfer history implements a Stale-While-Revalidate (SWR) pattern using local storage for instant offline access.
Daily JSON Dumps: Automated daily export of the event store to JSON files for external backups and data lakes.
🏗️ System Architecture
This project strictly follows Clean Architecture and Domain-Driven Design (DDD) principles.

Backend (ASP.NET Core 8)
API Layer: RESTful endpoints, JWT Authentication, Swagger UI.
Application Layer: Use cases, DTOs, Business Logic interfaces.
Infrastructure Layer: Entity Framework Core, Repository implementations.
Domain Layer: Aggregates, Enums, pure business entities.
Database (PostgreSQL 16)
Triggers & Stored Procedures: Business logic (e.g., stock deduction, hierarchy validation) is offloaded to the DB level using pg_advisory_xact_lock to prevent race conditions.
Materialized Views: Pre-calculated aggregate data for lightning-fast reporting.
Native Enums: Strict type checking for roles and warehouse levels.
Frontend (Flutter)
State Management: flutter_bloc (Event-Driven UI).
Networking: Dio with interceptors for automated JWT injection and 401 Auto-Logout.
UI/UX: Custom theming, RTL support, Vazirmatn font, glassmorphism design.
🗄️ Database & Event Sourcing
Instead of standard CRUD operations that overwrite data, this system uses an append-only event store.

Command: User requests a stock transfer.
Event Appended: TransferCreated, StockDecreased, and StockIncreased events are appended to the events table.
Projection: The warehouse_inventory (Read Model) table is updated atomically within the same transaction.
Snapshot: If the aggregate version hits a multiple of 100, a snapshot is auto-generated to speed up future state rebuilds.
🛠️ Tech Stack
Category	Technology
Frontend	Flutter, Dart, BLoC, Dio, SharedPreferences
Backend	ASP.NET Core 8, C#, EF Core 8
Database	PostgreSQL 16, PL/pgSQL
Architecture	Clean Architecture, Event Sourcing, CQRS-lite
DevOps	Docker, Nginx (Configured for deployment)
🚀 Getting Started
Prerequisites
Flutter 3.x SDK
.NET 8 SDK
PostgreSQL 16
Docker (Optional, for containerized DB)
Backend Setup
cd WMS.API# Update connection string in appsettings.jsondotnet restoredotnet ef database updatedotnet run
Swagger UI will be available at http://localhost:5049/swagger

Frontend Setup
cd wms_appflutter pub getflutter run
📄 License
This project is licensed under the MIT License.
