


````markdown
# 🏭 Enterprise Warehouse Management System (WMS)

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
| ![Login Screen](INSERT_LINK_TO_LO<img width="648" height="1034" alt="2026-06-21 16_01_43-" src="https://github.com/user-attachments/assets/14ea14b2-e8ae-41a2-b508-5e3adab51e4a" />
<img width="645" height="1033" alt="2026-06-21 16_01_13-Settings" src="https://github.com/user-attachments/assets/a76cd0d9-955e-4b46-9d58-ebe7e26bf344" />
<img width="643" height="1036" alt="2026-06-21 16_00_22-" src="https://github.com/user-attachments/assets/7209fec2-09ac-4182-b6a7-83292a5db012" />
<img width="646" height="1036" alt="2026-06-21 15_59_41-" src="https://github.com/user-attachments/assets/f6bd6188-25a0-4e66-b5c0-19f977cb033d" />
<img width="644" height="1032" alt="2026-06-21 15_58_25-" src="https://github.com/user-attachments/assets/82f89ca9-f438-4697-b2f6-253556e84e0c" />
<img width="644" height="1032" alt="2026-06-21 15_58_25-" src="https://github.com/user-attachments/assets/555bce09-58a9-4077-aa5b-6b378b45a57c" />
GIN_IMAGE) | ![Warehouses](INSERT_LINK_TO_WAREHOUSE_IMAGE) | ![Transfers](INSERT_LINK_TO_TRANSFER_IMAGE) |

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
| **DevOps** | Docker, Nginx (Configured for deployment) |

---

## 🚀 Getting Started

### Prerequisites
- Flutter 3.x SDK
- .NET 8 SDK
- PostgreSQL 16
- Docker (Optional, for containerized DB)

### Backend Setup
```bash
cd WMS.API
# Update connection string in appsettings.json
dotnet restore
dotnet ef database update
dotnet run
```
*Swagger UI will be available at `http://localhost:5049/swagger`*

### Frontend Setup
```bash
cd wms_app
flutter pub get
flutter run
```

---

## 📄 License

This project is licensed under the MIT License.
````

---

### 2. `README_FA.md` (Persian Version)

````markdown
# 🏭 سیستم مدیریت انبار سازمانی (WMS)

![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter)
![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?logo=postgresql)
![License](https://img.shields.io/badge/License-MIT-green)

یک سیستم مدیریت انبار آماده تولید (Production-Ready) و بسیار مقیاس‌پذیر که برای مدیریت عملیات پیچیده موجودی در یک سلسله‌مراتب چند سطحی طراحی شده است. این سیستم با استفاده از **معماری تمیز (Clean Architecture)** در بک‌اند و موتور دیتابیس **مبتنی بر رویداد (Event Sourcing)** توسعه یافته تا یکپارچگی داده‌ها، تاریخچه کامل ممیزی و عدم از دست رفتن اطلاعات را تضمین کند.

---

## 📸 رابط کاربری اپلیکیشن

| ورود و داشبورد | موجودی انبارها | انتقال کالا و اعتبارسنجی |
| :---: | :---: | :---: |
| ![صفحه ورود](INSERT_LINK_TO_LOGIN_IMAGE) | ![انبارها](INSERT_LINK_TO_WAREHOUSE_IMAGE) | ![انتقالات](INSERT_LINK_TO_TRANSFER_IMAGE) |

---

## ✨ ویژگی‌های کلیدی

- **سلسله‌مراتب ۴ سطحی انبارها:** اعمال سخت‌گیرانه جریان موجودی (مرکزی → منطقه‌ای → محلی → مصرف/دورریختن) با استفاده از تریگرهای دیتابیس.
- **موتور Event Sourcing:** لاگ تغییرناپذیر (Immutable). هر حرکت موجودی به عنوان یک رویداد ثبت می‌شود. ایجاد اسنپ‌شات خودکار در هر ۱۰۰ رویداد.
- **اعتبارسنجی لحظه‌ای موجودی:** رابط کاربری از انتقال بیشتر از ظرفیت موجودی جلوگیری کرده و به صورت لحظه‌ای هنگام تایپ کاربر به‌روزرسانی می‌شود.
- **جستجوی لحظه‌ای فارسی:** جستجوی Debounce با نرمال‌سازی یونیکد عربی به فارسی برای کوئری‌دهی بی‌نقص متون فارسی.
- **کشینگ آفلاین (Offline-First):** تاریخچه انتقالات با استفاده از الگوی Stale-While-Revalidate به صورت محلی ذخیره می‌شود تا دسترسی آنی در حالت آفلاین فراهم باشد.
- **خروجی روزانه JSON:** خروجی‌گیری خودکار روزانه از Event Store به فایل‌های JSON برای بکاپ‌گیری اکسترنال.

---

## 🏗️ معماری سیستم

این پروژه به شدت از اصول **معماری تمیز (Clean Architecture)** و **طراحی دامنه‌محور (DDD)** پیروی می‌کند.

#### بک‌اند (ASP.NET Core 8)
- **لایه API:** اندپوینت‌های RESTful، احراز هویت JWT، رابط کاربری Swagger.
- **لایه Application:** موارد استفاده (Use Cases)، DTOها، رابط‌های منطق تجاری.
- **لایه Infrastructure:** Entity Framework Core، پیاده‌سازی ریپازیتوری‌ها.
- **لایه Domain:** Aggregateها، Enumها، موجودیت‌های خالص تجاری.

#### دیتابیس (PostgreSQL 16)
- **تریگرها و رویه‌های ذخیره شده:** منطق تجاری (مانند کسر موجودی، اعتبارسنجی سلسله‌مراتب) به سطح دیتابیس منتقل شده و با استفاده از `pg_advisory_xact_lock` از رخ دادن Race Condition جلوگیری می‌کند.
- **Materialized Views:** داده‌های تجمیع‌شده از پیش محاسبه شده برای گزارش‌دهی بسیار سریع.
- **Native Enums:** بررسی دقیق نوع داده‌ها برای نقش‌ها و سطوح انبار.

#### فرانت‌اند (Flutter)
- **مدیریت وضعیت:** `flutter_bloc` (رابط کاربری مبتنی بر رویداد).
- **شبکه:** `Dio` به همراه اینترسپتورها برای تزریق خودکار توکن JWT و خروج خودکار در صورت خطای 401.
- **رابط کاربری:** تم‌بندی سفارشی، پشتیبانی RTL، فونت وزیرمتن، طراحی Glassmorphism.

---

## 🗄️ دیتابیس و Event Sourcing

به جای عملیات استاندارد CRUD که داده‌ها را بازنویسی می‌کنند، این سیستم از یک Event Store با قابلیت افزودن (Append-only) استفاده می‌کند.

1. **درخواست (Command):** کاربر درخواست انتقال موجودی می‌دهد.
2. **ثبت رویداد (Event Appended):** رویدادهای `TransferCreated`، `StockDecreased` و `StockIncreased` به جدول `events` اضافه می‌شوند.
3. **بروزرسانی مدل خواندن (Projection):** جدول `warehouse_inventory` به صورت اتمیک در همان تراکنش بروزرسانی می‌شود.
4. **اسنپ‌شات (Snapshot):** اگر نسخه Aggregate به مضرب ۱۰۰ برسد، یک اسنپ‌شات برای تسریع بازسازی وضعیت در آینده ایجاد می‌شود.

---

## 🛠️ پشته فناوری (Tech Stack)

| دسته | تکنولوژی |
|----------|------------|
| **فرانت‌اند** | Flutter, Dart, BLoC, Dio, SharedPreferences |
| **بک‌اند** | ASP.NET Core 8, C#, EF Core 8 |
| **دیتابیس** | PostgreSQL 16, PL/pgSQL |
| **معماری**| Clean Architecture, Event Sourcing, CQRS-lite |
| **DevOps** | Docker, Nginx (پیکربندی شده برای استقرار) |

---

## 🚀 نحوه اجرا

### پیش‌نیازها
- Flutter 3.x SDK
- .NET 8 SDK
- PostgreSQL 16
- Docker (اختیاری، برای دیتابیس کانتینری)

### راه‌اندازی بک‌اند
```bash
cd WMS.API
# آپدیت کانکشن استرینگ در فایل appsettings.json
dotnet restore
dotnet ef database update
dotnet run
```
*رابط کاربری Swagger در آدرس `http://localhost:5049/swagger` در دسترس خواهد بود.*

### راه‌اندازی فرانت‌اند
```bash
cd wms_app
flutter pub get
flutter run
```

---

## 📄 لایسنس

این پروژه تحت لایسنس MIT منتشر شده است.
````

### How to use this on GitHub:
1. Create a new repository on GitHub.
2. Upload both `README.md` and `README_FA.md` to the root of your repository.
3. On your repository page on GitHub, you can add a link at the top of the English README saying: `[🇮🇷 نسخه فارسی](README_FA.md)` and at the top of the Persian one saying: `[🇬🇧 English Version](README.md)`.
4. Drag and drop your images directly into the GitHub markdown editor to replace the `INSERT_LINK_TO_IMAGE` placeholders.

This README positions you not just as a developer, but as a **Software Architect** who understands enterprise patterns!
