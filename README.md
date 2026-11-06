# PEN Global Student Management System

A full-stack student management application developed as part of the PEN Global assessment. The platform provides a centralized system for managing student enrolment, academic programmes, fee payments, assessment submissions, and academic results.

Built with **Next.js, TypeScript, PostgreSQL, and Prisma ORM**.

---

## Project Overview

The PEN Global Student Management System is designed to simplify academic administration by bringing essential student management operations into one application.

The system provides administrative tools for managing student records, monitoring outstanding fees, tracking assessment submissions, and recording and publishing academic results.

## Key Features

### 1. Student Enrolment Management
- Register new students.
- Automatically generate unique Student IDs.
- Manage student details and academic years.
- Track enrolment statuses: Enrolled, Deferred, Withdrawn, and Completed.
- Manage programme assignments.

### 2. Programme Management
- Create and manage academic programmes.
- Assign programme codes.
- Configure programme tuition fees.
- Associate students with their respective programmes.

### 3. Fees and Payment Management
- Track student fee records.
- Record individual payments.
- Calculate outstanding balances.
- Monitor payment statuses: Paid, Partial, and Unpaid.
- Identify overdue payments.

### 4. Assessment Management
- Create assessments and assign modules.
- Set assessment deadlines.
- View assessment records.
- Track student submission information.
- Identify late submissions.

### 5. Marksheets and Results
- Enter student assessment scores.
- Validate grades between 0 and 100.
- Automatically calculate academic classifications:
  - Fail: 0–39
  - Pass: 40–59
  - Merit: 60–69
  - Distinction: 70–100
- Publish or withhold individual results.

### 6. Dashboard
- Centralized application dashboard.
- Access to the main management modules.
- Overview of student and academic administration.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Next.js 16 | Full-stack application framework |
| React 19 | User interface |
| TypeScript | Type-safe development |
| PostgreSQL | Relational database |
| Prisma ORM 7 | Database access and schema management |
| Tailwind CSS 4 | Styling and responsive interface |
| n8n | Workflow automation (separate integration project) |

---

## Application Architecture

```text
PEN Global Student Management System
│
├── Frontend
│   ├── Dashboard
│   ├── Student Management
│   ├── Programme Management
│   ├── Fees & Payments
│   ├── Assessments
│   └── Marksheets & Results
│
├── Backend
│   └── Next.js API Routes
│       ├── Students API
│       ├── Programmes API
│       ├── Fees API
│       ├── Assessments API
│       ├── Submissions API
│       └── Grades API
│
└── Database
    └── PostgreSQL
        ├── Student
        ├── Programme
        ├── Fee
        ├── Payment
        ├── Assessment
        ├── Submission
        └── Grade
```

---

## Getting Started

Follow these instructions to install and run the project locally.

### Prerequisites

Make sure you have installed:

- Node.js 20.9 or later
- npm
- PostgreSQL
- Git

### 1. Clone the Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

Navigate into the project directory:

```bash
cd pen-student-management-system
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create your local environment file:

```bash
cp .env.example .env
```

Open `.env` and configure your PostgreSQL database connection:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:5432/DATABASE?schema=public"
```

Replace the placeholders with your own PostgreSQL database credentials.

**Important:** Never upload your `.env` file or database credentials to GitHub.

### 4. Generate Prisma Client

```bash
npx prisma generate
```

### 5. Apply Database Migrations

```bash
npx prisma migrate deploy
```

### 6. Populate Sample Data

```bash
npm run seed
```

### 7. Start the Development Server

```bash
npm run dev
```

Open your browser:

**http://localhost:3000**

---

## Available Commands

| Command | Description |
|---|---|
| `npm run dev` | Start development server |
| `npm run build` | Build production application |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npx prisma generate` | Generate Prisma Client |
| `npx prisma migrate deploy` | Apply database migrations |
| `npm run seed` | Populate sample database records |
| `npx prisma studio` | Open Prisma Studio |

---

## Database Schema

The application uses PostgreSQL with Prisma ORM.

The primary database models include:

- **Student:** Student identity, personal details, academic year, and enrolment status.
- **Programme:** Programme information, unique programme codes, and tuition fees.
- **Fee:** Student fee records, total amounts, due dates, and payment status.
- **Payment:** Individual payment transactions and reference numbers.
- **Assessment:** Assessment titles, modules, and deadlines.
- **Submission:** Student submission records, file references, and late-submission status.
- **Grade:** Assessment scores and publication status.

The Prisma schema is available at:

`prisma/schema.prisma`

---

## API Structure

The application uses Next.js Route Handlers for backend operations.

| Endpoint | Method | Purpose |
|---|---|---|
| `/api/students` | GET / POST | Retrieve and register students |
| `/api/programmes` | GET / POST | Retrieve and create programmes |
| `/api/fees` | GET / POST | Retrieve fee records and record payments |
| `/api/assessments` | GET / POST | Retrieve and create assessments |
| `/api/submissions` | GET / POST | Retrieve and register submissions |
| `/api/grades` | GET / POST | Retrieve and save student grades |
| `/api/db-check` | GET | Check database connectivity |

---

## Workflow Automation

The project also includes a separate n8n automation initiative designed to support administrative processes.

Planned and developed workflow areas include:

- Student enrolment automation.
- Fee and payment recording.
- Overdue fee notifications.
- Assessment deadline reminders.
- Assignment submission processing.
- Marksheets and results processing.

**Note:** The n8n workflow exports are maintained separately and are not included in this application repository package.

---

## Important Implementation Notes

- A PostgreSQL database connection is required.
- Assessment submission records currently store file names and file URLs; actual document storage requires a separate file-storage integration.
- Authentication and role-based authorization require further implementation and verification before production deployment.
- Configure your own environment variables before running the application.
- Review the seed script before running it against a database containing existing records.

---

## Future Improvements

- Secure staff and student authentication.
- Role-based access control.
- Actual PDF and DOCX upload and storage.
- Automated student email notifications.
- Advanced reporting and analytics.
- Deployment and production monitoring.

---

## Project Purpose

This project was developed as a practical full-stack application for the PEN Global Student Management System assessment, demonstrating database design, API development, frontend implementation, academic administration workflows, and automation integration.

---

**Built with Next.js, PostgreSQL, Prisma, and TypeScript.**



# PEN Global – n8n Workflow Documentation

## Overview

This directory contains exported n8n automation workflows developed for the PEN Global Student Management System.

The workflows connect the application’s REST APIs with n8n and Google Sheets to automate student enrolment, payment recording, assessment submissions, and academic result management.

## Technology & Integrations

- **n8n:** Workflow orchestration and automation
- **Next.js REST APIs:** Backend communication
- **PostgreSQL:** Primary application database
- **Google Sheets:** Administrative record-keeping
- **Webhook:** Receives external HTTP requests
- **HTTP Request:** Communicates with application APIs
- **Code nodes:** Data validation and business logic

---

## 1. Student Enrolment

**File:** `PEN Global - Student Enrollment.json`

**Purpose:** Automates the student registration process and creates new student records in the PEN Global application.

### Workflow sequence

1. **Student Enrolment – Webhook Trigger:** Receives student information through an HTTP POST request.
2. **Validate Student Data:** Checks required fields, email format, date of birth, academic year, and enrolment status.
3. **Prepare Student Enrolment Data:** Organizes the validated information.
4. **Student Data Valid?:** Routes valid and invalid records.
5. **Create Student Record:** Sends the student information to the `/api/students` endpoint.
6. **Return Enrolment Confirmation:** Returns the successful enrolment response.
7. **Return Validation Errors:** Explains missing or invalid information.
8. **Return Enrolment API Error:** Handles backend API failures.
9. **Update Google Sheet:** Records the new student's ID, name, programme code, fee amount, and timestamp.

### Required input

```json
{
  "fullName": "Michael Anderson",
  "email": "michael.anderson@example.com",
  "dateOfBirth": "2001-08-15",
  "programmeId": "YOUR_PROGRAMME_ID",
  "academicYear": "2026/2027",
  "enrolmentStatus": "ENROLLED"
}
```

### Supported enrolment statuses

- ENROLLED
- DEFERRED
- WITHDRAWN
- COMPLETED

---

## 2. Fees & Payments

**File:** `PEN Global - Fees & Payments.json`

**Purpose:** Records student fee payments, retrieves updated fee balances, and maintains payment transaction records.

### Workflow sequence

1. **Payment Recording – Webhook Trigger:** Receives payment details.
2. **Validate Payment Details:** Checks the fee ID, payment amount, payment date, and reference number.
3. **Prepare Payment Data:** Organizes the validated payment information.
4. **Payment Data Valid?:** Determines whether the payment can proceed.
5. **Record Student Payment:** Sends the transaction to the `/api/fees` endpoint.

