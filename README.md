# Buyer Lead Intake App

A comprehensive lead management system built with Next.js, featuring real-time data processing, CSV import/export capabilities, and role-based access controls.

## Setup

### Prerequisites

- Node.js (v18 or higher)
- PostgreSQL database
- pnpm package manager

### Installation

1. **Clone the repository**

   ```shell
   git clone https://github.com/Sahil-Makhija/esahayak_assignment
   cd buyer-lead-intake-app
   ```

2. **Configure environment variables**
   Create a `.env.local` file in the root directory and add:

   ```shell
   DATABASE_URL="your-postgresql-connection-string"
   ```

3. **Install dependencies**

   ```shell
   pnpm install
   ```

4. **Initialize the database**

   ```shell
   bun src/lib/db/seed.ts
   ```

5. **Start the development server**
   ```shell
   pnpm run dev
   ```

### Demo Access

For testing and demonstration purposes, use the following credentials:

| Username | Password   | User Type | Access Level                                                        |
| -------- | ---------- | --------- | ------------------------------------------------------------------- |
| `demo`   | `demo`     | User      | Standard user access - can view all buyers, create/edit own records |
| `admin`  | `password` | Admin     | Full system access - can perform all CRUD operations on any record  |

---

## Project Architecture

### System Overview

The application follows a modern three-tier architecture:

1. **Frontend Layer** - Next.js application with Tailwind CSS for styling
2. **API Layer** - RESTful API built with Hono.js for CRUD operations
3. **Data Layer** - PostgreSQL database with Prisma ORM for data management

### Design Philosophy

This architecture was chosen to provide:

- **Complete type safety** through Zod validation implemented across both frontend and API layers
- **Scalable authentication** with custom Hono.js middleware
- **Maintainable codebase** following established design patterns

### Component Architecture

The frontend implements **Atomic Design** methodology:

- **Atoms** - Basic UI components, primarily from shadcn/ui library with custom extensions
- **Molecules** - Composite components such as form fields (fullname, email, etc.)
- **Organisms** - Complex components like complete forms utilizing molecule-level components
- **Templates** - High-level components responsible for data fetching and state management

---

## Validation & Type Safety

### Client-Side Validation

- **Form Management**: All forms utilize `react-hook-form` with `zodResolver` for seamless validation
- **Field-Level Validation**: Each form field includes dedicated validation rules
- **Type-Safe API Calls**: `@tanstack/react-query` ensures 100% type-safe API interactions

### Server-Side Validation

- **Schema Validation**: Hono.js API implements `zValidator` to validate incoming data using identical schema objects
- **Data Integrity**: Ensures data consistency between client and server validation layers

---

## Performance & Data Fetching

### Server-Side Rendering (SSR)

The following pages implement SSR for optimal performance:

- Buyer details view
- Buyer edit interface
- Buyer listings with filters

All SSR implementations utilize direct database client connections for efficient data retrieval.

---

## Security & Access Control

### Authorization Framework

- **Endpoint Protection**: All API endpoints implement comprehensive access control checks
- **Role-Based Permissions**:
  - Admins have full system access
  - Buyer owners can edit/delete their own records
  - All authenticated users have read access to buyer data
- **Secure Operations**: Edit and delete operations require proper ownership verification

---

## Core Features

### Lead Management

- **Lead Creation**: Streamlined lead intake process with comprehensive validation
- **Lead Listings**:
  - URL-synchronized filtering system
  - Sortable by `updatedAt` field
  - Responsive data table interface
- **Individual Lead View**: Detailed lead information display

### Data Import/Export

- **CSV Import**:
  - Bulk data import with row-level validation
  - Selective import of valid records only
  - Comprehensive error reporting for invalid entries
- **CSV Export**: Export currently filtered/displayed records

### User Experience

- **Buyer History**: Complete audit trail showing all modifications to buyer entries
- **Tag Management**: Visual tag chips for easy categorization
- **Quick Actions**: Contextual dropdown menus in data tables
- **Enhanced Error Handling**: Detailed, user-friendly form validation messages

### Data Validation

- **Budget Validation**: Automatic validation of `minBudget` and `maxBudget` relationships
- **Import Data Quality**: Comprehensive validation for CSV-imported data

---

### Features left

- **Field Rollback**: Ability to revert specific field changes from history
- **Rate Limiting**: API request throttling for enhanced security and performance

---

## Development

### Tech Stack

- **Frontend**: Next.js, React, Tailwind CSS, shadcn/ui
- **Backend**: Hono.js, Prisma ORM
- **Database**: PostgreSQL
- **Validation**: Zod
- **Forms**: React Hook Form
- **State Management**: TanStack Query, Zustand
