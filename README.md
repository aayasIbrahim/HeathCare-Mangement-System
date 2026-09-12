# Healthcare System Backend

A modern healthcare backend built with TypeScript, Express, Prisma, and PostgreSQL for managing patient, doctor, appointment, schedule, and authentication workflows.

This project is designed to support a healthcare platform where patients can register, authenticate, and book consultations, while doctors and administrative users manage schedules, approvals, and operational workflows.

## Status

This repository is in active development. Core authentication and user-related functionality are already implemented, while additional healthcare workflows such as scheduling, appointment booking, payments, and doctor management are being expanded according to the product requirements.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Available Scripts](#available-scripts)
- [API Overview](#api-overview)
- [Database & Prisma](#database--prisma)
- [Known Limitations](#known-limitations)
- [Contributing](#contributing)
- [License](#license)

## Overview

PH Healthcare System Backend provides the API layer for a digital healthcare platform. It handles user identity, authentication, role-based access control, and healthcare-specific business flows that connect patients, doctors, and admins.

The application follows a modular backend architecture, with each domain organized into dedicated route, controller, service, and interface layers.

## Features

- User registration and login
- Role-based access control with JWT authentication
- Patient profile access and session validation
- Doctor and admin-related modules
- Appointment and schedule support
- Prisma ORM integration with PostgreSQL
- Email / notification support
- Cloudinary media handling
- Redis integration for supporting infrastructure
- Payment and healthcare workflow hooks
- Seed data support for default admin and test accounts

## Technology Stack

- TypeScript
- Node.js
- Express.js
- Prisma ORM
- PostgreSQL
- Redis
- JWT Authentication
- bcryptjs
- Nodemailer
- Cloudinary
- CORS
- Zod validation support
- tsx for local development

## Project Structure

```text
.
├── .env
├── .env.example
├── .gitignore
├── biome.json
├── package-lock.json
├── package.json
├── prisma.config.ts
├── Project Requirements.md
├── README.md
├── tsconfig.json
├── dist/
│   └── (compiled TypeScript output)
├── prisma/
│   ├── migrations/
│   └── schema/
│       ├── appointment.prisma
│       ├── doctor.prisma
│       ├── enums.prisma
│       ├── patient.prisma
│       ├── payment.prisma
│       ├── schedule.prisma
│       ├── schema.prisma
│       └── user.prisma
├── src/
│   ├── app.ts
│   ├── server.ts
│   ├── app/
│   │   ├── config/
│   │   │   └── index.ts
│   │   ├── interfaces/
│   │   │   └── index.ts
│   │   ├── lib/
│   │   │   ├── bkash.ts
│   │   │   ├── cloudinary.ts
│   │   │   ├── cron.ts
│   │   │   ├── gogleAuth.ts
│   │   │   ├── multer.ts
│   │   │   ├── nodemailer.ts
│   │   │   ├── prisma.ts
│   │   │   └── redis.ts
│   │   ├── middleware/
│   │   │   ├── checkAuth.ts
│   │   │   ├── globalErrorHandler.ts
│   │   │   ├── notFound.ts
│   │   │   └── validateReques.ts
│   │   ├── module/
│   │   │   ├── appointment/
│   │   │   │   ├── appointment.controller.ts
│   │   │   │   ├── appointment.interface.ts
│   │   │   │   ├── appointment.route.ts
│   │   │   │   └── appointment.service.ts
│   │   │   ├── auth/
│   │   │   │   ├── auth.controller.ts
│   │   │   │   ├── auth.interface.ts
│   │   │   │   ├── auth.route.ts
│   │   │   │   ├── auth.service.ts
│   │   │   │   └── auth.validation.ts
│   │   │   ├── doctor/
│   │   │   │   ├── doctor.controller.ts
│   │   │   │   ├── doctor.interface.ts
│   │   │   │   ├── doctor.route.ts
│   │   │   │   ├── doctor.service.ts
│   │   │   │   └── doctor.validation.ts
│   │   │   ├── schedule/
│   │   │   │   ├── schedule.controller.ts
│   │   │   │   ├── schedule.interface.ts
│   │   │   │   ├── schedule.route.ts
│   │   │   │   ├── schedule.service.ts
│   │   │   │   └── schedule.validation.ts
│   │   │   └── user/
│   │   │       ├── user.controllers.ts
│   │   │       ├── user.route.ts
│   │   │       ├── user.service.ts
│   │   │       └── user.validation.ts
│   │   ├── templates/
│   │   │   ├── doctor-application-approved.ejs
│   │   │   ├── doctor-application-rejected.ejs
│   │   │   ├── forgot-password.ejs
│   │   │   ├── patient-welcome-email.ejs
│   │   │   ├── registration-user-otp.ejs
│   │   │   └── reset-password-success.ejs
│   │   ├── utils/
│   │   │   ├── AppError.ts
│   │   │   ├── catchAsync.ts
│   │   │   ├── jwt.ts
│   │   │   ├── seed.ts
│   │   │   └── sendResponse.ts
│   │   └── interfaces/
│   │       └── index.ts
│   └── generated/
│       └── prisma/
│           ├── browser.ts
│           ├── client.ts
│           ├── commonInputTypes.ts
│           ├── enums.ts
│           ├── models.ts
│           └── internal/
│               └── ...
└── node_modules/
```

### Core backend directories

- `src/app/module/` — domain-specific feature modules such as auth, user, doctor, appointment, and schedule
- `src/app/middleware/` — authentication, error handling, and request flow middleware
- `src/app/lib/` — shared services and integrations such as Prisma, Redis, email, and cloud storage
- `src/app/config/` — environment configuration loader
- `src/app/utils/` — reusable helper utilities and support scripts
- `prisma/schema/` — Prisma schema split across logical domain files

## Prerequisites

Make sure the following tools are installed:

- Node.js 20+
- PostgreSQL 14+
- npm or another package manager

Verify your environment:

```bash
node -v
npm -v
psql -V
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/aayasIbrahim/HeathCare-Mangement-System.git
cd "health care mangem system"
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Copy the example environment file:

```bash
cp .env.example .env
```

Then update the values in `.env` to match your local setup.

Example:

```env
NODE_ENV=development
PORT=5000
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/ph_healthcare?schema=public"
JWT_ACCESS_SECRET=your_access_secret
JWT_REFRESH_SECRET=your_refresh_secret
JWT_ACCESS_EXPIRES_IN=1d
JWT_REFRESH_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:3000

SUPER_ADMIN_NAME=Super Admin 1
SUPER_ADMIN_EMAIL=superadmin@gmail.com
SUPER_ADMIN_PASSWORD=Super@admin12345

TESTER_ADMIN_NAME=Tester Admin 1
TESTER_ADMIN_EMAIL=testeradmin@gmail.com
TESTER_ADMIN_PASSWORD=Tester@admin12345

TESTER_DOCTOR_NAME=Tester Doctor 1
TESTER_DOCTOR_EMAIL=testerdoctor@gmail.com
TESTER_DOCTOR_PASSWORD=Tester@doctor12345
```

### Default seeded login accounts

These credentials are not required to be entered manually in the `.env` file for normal app usage. They are built-in seeded accounts that the application creates during startup for local testing and admin access.

| Role          | Email                    | Password             |
| ------------- | ------------------------ | -------------------- |
| Super Admin   | `superadmin@gmail.com`   | `Super@admin12345`   |
| Tester Admin  | `testeradmin@gmail.com`  | `Tester@admin12345`  |
| Tester Doctor | `testerdoctor@gmail.com` | `Tester@doctor12345` |

Use these email/password pairs when logging in through the app UI or API. Regular users can also register a new patient account directly with the register endpoint.

### 4. Generate the Prisma client

```bash
npx prisma generate
```

### 5. Run database migrations

```bash
npx prisma migrate dev
```

This will apply the current Prisma migration history and initialize the database schema.

### 6. Start the application

```bash
npm run dev
```

The server should start and log a successful database connection, followed by the application listening on the configured port.

### 7. Health check

```bash
curl http://localhost:5000/
```

Expected response:

```json
{
  "success": true,
  "message": "Welcome to Healthcare System Backend"
}
```

## Environment Variables

The application configuration is centralized in `src/app/config/index.ts` and reads from the environment file at runtime.

| Variable                 | Description                                           |
| ------------------------ | ----------------------------------------------------- |
| `NODE_ENV`               | Runtime environment such as development or production |
| `PORT`                   | Port used by the Express server                       |
| `DATABASE_URL`           | PostgreSQL connection string                          |
| `JWT_ACCESS_SECRET`      | Secret used to sign access tokens                     |
| `JWT_REFRESH_SECRET`     | Secret used to sign refresh tokens                    |
| `JWT_ACCESS_EXPIRES_IN`  | Access token lifetime                                 |
| `JWT_REFRESH_EXPIRES_IN` | Refresh token lifetime                                |
| `FRONTEND_URL`           | Frontend origin allowed by CORS                       |
| `GOOGLE_CLIENT_ID`       | Google OAuth client ID                                |
| `BCRYPT_SALT_ROUNDS`     | Password hashing cost factor                          |
| `REDIS_HOST`             | Redis host                                            |
| `REDIS_PORT`             | Redis port                                            |
| `SMTP_USER`              | Email provider username                               |
| `SMTP_PASSWORD`          | Email provider password                               |
| `EMAIL_SENDER`           | Sender email address                                  |
| `CLOUDINARY_*`           | Cloudinary credentials                                |
| `BKASH_*`                | BKash payment integration configuration               |

> Important: always generate strong JWT secrets before deploying to any non-local environment.

## Available Scripts

```bash
npm run dev
npm run build
npm run start
npm run test
npm run lint:check
npm run lint:fix
npm run format:check
npm run format:fix
```

### Script notes

- `npm run dev` — starts the app in development mode with automatic restarts
- `npm run build` — runs TypeScript compilation
- `npm run start` — starts the compiled app using Node
- `npm run lint:*` and `npm run format:*` — formatting and lint checks using Biome

## API Overview

Base URL:

```text
http://localhost:5000
```

### Core endpoints

| Method | Route | Auth | Description           |
| ------ | ----- | ---- | --------------------- |
| `GET`  | `/`   | No   | Health check endpoint |

### Authentication endpoints

| Method | Route                          | Auth | Description                      |
| ------ | ------------------------------ | ---- | -------------------------------- |
| `POST` | `/api/v1/auth/register`        | No   | Register a new patient           |
| `POST` | `/api/v1/auth/verify-email`    | No   | Verify patient email using OTP   |
| `POST` | `/api/v1/auth/login`           | No   | Log in with email and password   |
| `GET`  | `/api/v1/auth/me`              | Yes  | Fetch current authenticated user |
| `POST` | `/api/v1/auth/refresh-token`   | No   | Refresh the access token         |
| `POST` | `/api/v1/auth/google`          | No   | Google login flow                |
| `POST` | `/api/v1/auth/forgot-password` | No   | Request password reset OTP       |
| `POST` | `/api/v1/auth/reset-password`  | No   | Reset password using OTP         |

### Doctor endpoints

| Method | Route                                         | Auth                | Description                                   |
| ------ | --------------------------------------------- | ------------------- | --------------------------------------------- |
| `POST` | `/api/v1/doctor/apply-as-doctor`              | No                  | Submit a doctor application with upload files |
| `POST` | `/api/v1/doctor/apply-as-doctor/verify-email` | No                  | Verify doctor application email               |
| `POST` | `/api/v1/doctor/approve-doctor`               | Admin / Super Admin | Approve doctor record                         |
| `GET`  | `/api/v1/doctor/all-doctors`                  | Admin / Super Admin | Get all doctors                               |

### Schedule endpoints

| Method   | Route                                           | Auth                         | Description                   |
| -------- | ----------------------------------------------- | ---------------------------- | ----------------------------- |
| `POST`   | `/api/v1/schedule/create-schedule`              | Doctor                       | Create a new doctor schedule  |
| `GET`    | `/api/v1/schedule/my-schedules`                 | Doctor                       | Get doctor’s schedules        |
| `GET`    | `/api/v1/schedule/all-schedules`                | Admin / Super Admin          | Get all schedules             |
| `GET`    | `/api/v1/schedule/todays-schedule`              | No                           | Get today’s visible schedules |
| `PATCH`  | `/api/v1/schedule/update-schedule/:scheduleId`  | Doctor                       | Update a schedule             |
| `PATCH`  | `/api/v1/schedule/publish-schedule/:scheduleId` | Doctor                       | Publish a schedule            |
| `GET`    | `/api/v1/schedule/:scheduleId`                  | Doctor / Admin / Super Admin | Get schedule by ID            |
| `DELETE` | `/api/v1/schedule/:scheduleId`                  | Doctor                       | Delete a schedule             |

### Appointment endpoints

| Method | Route                                                   | Auth                          | Description                     |
| ------ | ------------------------------------------------------- | ----------------------------- | ------------------------------- |
| `POST` | `/api/v1/appointment/book-appointment`                  | Patient                       | Book a consultation appointment |
| `POST` | `/api/v1/appointment/pay-appointment`                   | Patient                       | Pay for an appointment          |
| `POST` | `/api/v1/appointment/cancel-appointment`                | Patient / Admin / Super Admin | Cancel an appointment           |
| `GET`  | `/api/v1/appointment/book-appointment/payment/callback` | No                            | Payment callback URL            |

### User endpoints

| Method  | Route                        | Auth                                   | Description                    |
| ------- | ---------------------------- | -------------------------------------- | ------------------------------ |
| `PATCH` | `/api/v1/user/profile-image` | Admin / Super Admin / Doctor / Patient | Upload or update profile image |

### Example registration

```bash
curl -X POST http://localhost:5000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test Patient",
    "email": "patient@example.com",
    "password": "password123"
  }'
```

### Example authenticated request

```bash
curl http://localhost:5000/api/v1/auth/me \
  -H "Authorization: Bearer <accessToken>"
```

## Database & Prisma

This project uses Prisma as the ORM layer and PostgreSQL as the primary database.

To work with the schema:

```bash
npx prisma generate
npx prisma migrate dev
npx prisma studio
```

Prisma schema files are organized by domain and merged through the project configuration setup.

## Known Limitations

This project is a backend foundation and should be treated as an evolving application rather than a fully finished production system.

- Authentication is implemented and actively used.
- Additional healthcare features are still being developed.
- Some environment variables may be required for features outside the current core flow.
- Not all validation, security, and production-hardening checks are complete yet.
- Unit and integration test coverage is still limited.

The product requirements are documented in [Project Requirements.md](./Project%20Requirements.md).

## Contributing

Contributions are welcome. Please follow a clean feature-based workflow:

1. Create a feature branch from the latest code.
2. Keep domain logic separated by module.
3. Follow the existing route/controller/service pattern.
4. Validate with the project build and lint checks.
5. Keep changes small and focused.

## License

This project is licensed under the ISC License.

---

Built for healthcare service workflows with a modular backend architecture and modern TypeScript tooling.
