# Creator's Deal Hub (CDH) Next.js Web Application Architecture Document

Version: 1.2 (Expanded Content)

Date: June 2, 2025

Author: Fred (Architect)


## Introduction / Preamble

This document outlines the overall architecture for the Creator's Deal Hub (CDH) Next.js web application, including backend systems, shared services, and non-UI specific concerns. Its primary goal is to serve as the guiding architectural blueprint for development, ensuring consistency and adherence to chosen patterns and technologies.

The architecture described herein aligns with the requirements defined in the **Product Requirements Document (PRD) Version 1.7** (ID: `creator-deal-hub-prd.md`) and the vision set forth in the Project Brief (`web/docs/project-brief/project-brief.md`). It provides a comprehensive technical foundation for implementing the CDH web application, which aims to help creators manage deals and invoices efficiently.


## Table of Contents

1. [Introduction / Preamble](https://gemini.google.com/app/8af8248fd0f82386#introduction--preamble "null")

2. [Technical Summary](https://gemini.google.com/app/8af8248fd0f82386#technical-summary "null")

3. [High-Level Overview](https://gemini.google.com/app/8af8248fd0f82386#high-level-overview "null")

4. [Architectural / Design Patterns Adopted](https://gemini.google.com/app/8af8248fd0f82386#architectural--design-patterns-adopted "null")

5. [Component View](https://gemini.google.com/app/8af8248fd0f82386#component-view "null")

   - [Frontend Architecture - State Management](https://gemini.google.com/app/8af8248fd0f82386#frontend-architecture---state-management "null")

6. [Project Structure](https://gemini.google.com/app/8af8248fd0f82386#project-structure "null")

7. [API Reference](https://gemini.google.com/app/8af8248fd0f82386#api-reference "null")

   - [External APIs Consumed](https://gemini.google.com/app/8af8248fd0f82386#external-apis-consumed "null")

   - [Internal APIs Provided](https://gemini.google.com/app/8af8248fd0f82386#internal-apis-provided "null")

8. [Data Models](https://gemini.google.com/app/8af8248fd0f82386#data-models "null")

   - [Core Application Entities (Reconciled with PRD v1.7)](https://gemini.google.com/app/8af8248fd0f82386#core-application-entities-reconciled-with-prd-v17 "null")

   - [Database Schema (Reconciled with PRD v1.7)](https://gemini.google.com/app/8af8248fd0f82386#database-schema-reconciled-with-prd-v17 "null")

9. [Authentication & Authorization](https://gemini.google.com/app/8af8248fd0f82386#authentication--authorization "null")

   - [Authentication Flow](https://gemini.google.com/app/8af8248fd0f82386#authentication-flow "null")

   - [Authorization Strategy & Future RBAC](https://gemini.google.com/app/8af8248fd0f82386#authorization-strategy--future-rbac "null")

10. [Non-Functional Requirements Implementation](https://gemini.google.com/app/8af8248fd0f82386#non-functional-requirements-implementation "null")

    - [Performance](https://gemini.google.com/app/8af8248fd0f82386#performance "null")

    - [Scalability](https://gemini.google.com/app/8af8248fd0f82386#scalability "null")

    - [Security](https://gemini.google.com/app/8af8248fd0f82386#security "null")

    - [PWA Capabilities](https://gemini.google.com/app/8af8248fd0f82386#pwa-capabilities "null")

    - [Accessibility & Internationalization](https://gemini.google.com/app/8af8248fd0f82386#accessibility--internationalization "null")

11. [Deployment Strategy](https://gemini.google.com/app/8af8248fd0f82386#deployment-strategy "null")

    - [CI/CD Pipeline](https://gemini.google.com/app/8af8248fd0f82386#cicd-pipeline "null")

    - [Hosting](https://gemini.google.com/app/8af8248fd0f82386#hosting "null")

    - [Monitoring & Backup](https://gemini.google.com/app/8af8248fd0f82386#monitoring--backup "null")

12. [Error Handling & Logging](https://gemini.google.com/app/8af8248fd0f82386#error-handling--logging "null")

    - [Error Handling Strategy](https://gemini.google.com/app/8af8248fd0f82386#error-handling-strategy "null")

    - [Logging Approach](https://gemini.google.com/app/8af8248fd0f82386#logging-approach "null")

13. [Future Considerations & Scalability](https://gemini.google.com/app/8af8248fd0f82386#future-considerations--scalability "null")

    - [Marketplace Evolution](https://gemini.google.com/app/8af8248fd0f82386#marketplace-evolution "null")

    - [Team Collaboration](https://gemini.google.com/app/8af8248fd0f82386#team-collaboration "null")

    - [Analytics & Reporting](https://gemini.google.com/app/8af8248fd0f82386#analytics--reporting "null")

14. [Key Reference Documents](https://gemini.google.com/app/8af8248fd0f82386#key-reference-documents "null")

15. [Change Log](https://gemini.google.com/app/8af8248fd0f82386#change-log "null")


## Technical Summary

The Creator's Deal Hub Next.js web application is designed as a mobile-first, responsive web application built on a modern tech stack centered around Next.js and Supabase. The architecture follows a modular monolith pattern with clear separation of concerns, leveraging Next.js App Router for routing and React Server Components for optimal performance. The system uses Supabase for authentication, database, and storage needs, with a focus on scalability, security, and maintainability. The application is designed to support the core functionalities of user authentication, deal management, invoice generation, deliverable tracking, and reminders, with a path for future expansion into a marketplace platform.


## High-Level Overview

The CDH Next.js web application follows a modular monolith architecture. The primary user interaction flow involves creators signing up, creating and managing deals (including deliverables and reminders) with clients/brands, and generating invoices based on those deals. The system handles authentication, data persistence, and business logic processing through a combination of Next.js API routes and Supabase services.

    C4Context
        title System Context Diagram for Creator's Deal Hub (v1.1)

        Person(creator, "Creator", "A content creator who wants to manage deals, deliverables, invoices, and reminders")
        System(cdhSystem, "Creator's Deal Hub Web App", "Allows creators to manage deals, deliverables, invoices, and generate reminders. Facilitates interaction with brands/clients for invoicing.")

        System_Ext(emailService, "Email Service", "Sends notifications, invoices, and reminders")
        System_Ext(authProviderGoogle, "Google Auth", "Provides social authentication for creators")
        System_Ext(brandClient, "Brand/Client System", "External system or email of the brand/client receiving invoices/communications. (Future: Potential direct interaction for marketplace features)")

        Rel(creator, cdhSystem, "Uses to manage deals and invoices")
        Rel(cdhSystem, brandClient, "Sends invoices and communications to")
        Rel(cdhSystem, emailService, "Sends emails through")
        Rel(cdhSystem, authProviderGoogle, "Authenticates creators with")

**Figure 1: System Context Diagram for Creator's Deal Hub**

_Note on "Client" in C4 Diagram: For MVP, the "Brand/Client System" primarily represents the recipient of communications (like invoices). Direct login/interaction for brands/clients is a future marketplace consideration._


## Architectural / Design Patterns Adopted

- **Modular Monolith:** The application is structured as a single deployable unit with clear internal module boundaries. _Rationale:_ Appropriate for the initial MVP scope while allowing for future extraction of services if needed.

- **Server Components First:** Leveraging Next.js React Server Components for improved performance and reduced client-side JavaScript. _Rationale:_ Aligns with the performance requirements and mobile-first approach specified in the PRD.

- **Repository Pattern (Conceptual):** While not strictly implementing a full repository pattern with interfaces for MVP due to Supabase's client library capabilities, data access logic will be encapsulated within specific service modules or utility functions in `lib/db/` to maintain separation from business logic in API routes and server components. _Rationale:_ Improves testability and maintainability by decoupling business logic from direct data access details.

- **Feature-based Organization:** Code is organized primarily by feature rather than technical layer, promoting cohesion and easier navigation. _Rationale:_ Improves developer experience and maintainability as the application grows.

- **Progressive Web App (PWA):** Implementing PWA capabilities for offline functionality and mobile-like experience. _Rationale:_ Meets the PWA requirements specified in the PRD and enhances user experience on mobile devices.


## Component View

The CDH web application consists of the following major logical components:

- **Authentication Module:** Handles user registration, login, and session management using Supabase Auth.

- **Deal Management Module:** Manages the creation, updating, and retrieval of deals, including associated deliverables.

- **Invoice Module:** Handles the generation, management, and sending of invoices based on deals.

- **Reminder Module:** Manages creation and notification for reminders related to deals, deliverables, and invoices.

- **User Settings Module:** Manages user profile information, notification preferences, security settings, and invoice defaults.

- **API Layer:** Next.js API routes that provide server-side functionality and interact with Supabase.

- **Database Layer:** Supabase PostgreSQL database with Row Level Security (RLS) policies for data access control.

<!---->

    graph TD
    subgraph "Creator's Deal Hub Web App"
        AuthMod[Authentication Module] --> DB[(Supabase Database)]
        DealMod[Deal Management Module] --> DB
        InvoiceMod[Invoice Module] --> DB
        ReminderMod[Reminder Module] --> DB
        SettingsMod[User Settings Module] --> DB

        AuthMod --> APILayer[API Layer]
        DealMod --> APILayer
        InvoiceMod --> APILayer
        ReminderMod --> APILayer
        SettingsMod --> APILayer

        APILayer --> UI[User Interface - Next.js Frontend]
    end

    UI --> User((Creator User))

    %% Core Flow Examples
    subgraph "Core Flow Examples"
        direction TB
        SD_DealCreate[Deal Creation Flow<br/>Sequence Diagram]
        SD_InvoiceGen[Invoice Generation Flow<br/>Sequence Diagram]
        SD_Auth[Authentication Flow<br/>Sequence Diagram]
        SD_Reminder[Reminder System Flow<br/>Sequence Diagram]
    end

    %% Optional: Show relationship between flows and modules
    DealMod -.-> SD_DealCreate
    InvoiceMod -.-> SD_InvoiceGen
    AuthMod -.-> SD_Auth
    ReminderMod -.-> SD_Reminder

    classDef moduleClass fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef dbClass fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef userClass fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef flowClass fill:#fff3e0,stroke:#e65100,stroke-width:2px

    class AuthMod,DealMod,InvoiceMod,ReminderMod,SettingsMod,APILayer,UI moduleClass
    class DB dbClass
    class User userClass
    class SD_DealCreate,SD_InvoiceGen,SD_Auth,SD_Reminder flowClass

**Figure 2: High-Level Component View of CDH Web App**

_Note: Detailed sequence diagrams for core flows like Deal Creation and Invoice Generation will be added as the design progresses to clarify interactions between UI, Next.js API Routes, and Supabase._


### Frontend Architecture - State Management

As per PRD Section 10.1, global state management will primarily be handled using **React Context API**. This choice is suitable for the MVP's complexity, offering a built-in React solution without adding external dependencies for global state. Local component state will be managed using `useState` and `useReducer` where appropriate. For more complex client-side data caching and synchronization with the server (especially for data fetched via client components), libraries like SWR or React Query will be considered, as noted in the Performance NFR section.


## Project Structure

    cdh-web/
    ├── .github/                    # CI/CD workflows
    │   └── workflows/
    │       └── main.yml
    ├── .vscode/                    # VSCode settings
    │   └── settings.json
    ├── app/                        # Next.js App Router structure
    │   ├── (auth)/                 # Authentication routes
    │   │   ├── sign-in/page.tsx
    │   │   ├── sign-up/page.tsx
    │   │   └── layout.tsx
    │   ├── (dashboard)/            # Protected dashboard routes
    │   │   ├── deals/
    │   │   │   ├── [id]/page.tsx   # Single deal view (incl. deliverables)
    │   │   │   ├── create/page.tsx # Create deal form
    │   │   │   └── page.tsx        # Deals list
    │   │   ├── invoices/
    │   │   │   ├── [id]/page.tsx   # Single invoice view
    │   │   │   ├── create/page.tsx # Create invoice form (linked from deal)
    │   │   │   └── page.tsx        # Invoices list
    │   │   ├── reminders/page.tsx  # Reminders overview (Future)
    │   │   ├── settings/page.tsx   # User settings
    │   │   └── layout.tsx          # Dashboard layout
    │   ├── api/                    # API routes
    │   │   ├── auth/[...nextauth]/route.ts # If using NextAuth with Supabase adapter
    │   │   ├── deals/route.ts
    │   │   ├── deals/[id]/route.ts
    │   │   ├── invoices/route.ts
    │   │   ├── invoices/[id]/route.ts
    │   │   ├── reminders/route.ts
    │   │   └── user-settings/route.ts
    │   ├── globals.css
    │   ├── layout.tsx              # Root layout
    │   └── page.tsx                # Landing page
    ├── components/                 # Reusable React components
    │   ├── auth/
    │   ├── deals/
    │   ├── deliverables/
    │   ├── invoices/
    │   ├── reminders/
    │   ├── settings/
    │   ├── ui/                     # shadcn/ui based components (buttons, inputs, etc.)
    │   └── layout/
    ├── lib/                        # Shared utilities and services
    │   ├── auth.ts                 # Authentication utilities (Supabase client interactions)
    │   ├── db/                     # Database utilities and schema
    │   │   ├── schema.ts           # Drizzle schema / Zod schemas for validation
    │   │   └── queries.ts          # Supabase query functions / services
    │   ├── api-helpers.ts          # API route helpers
    │   ├── validation/             # Zod validation schemas
    │   └── utils.ts
    ├── public/                     # Static assets
    │   ├── favicon.ico
    │   ├── manifest.json           # PWA manifest
    │   └── service-worker.js       # PWA service worker
    ├── styles/                     # Additional global styles if needed
    ├── types/                      # TypeScript type definitions (global, or per feature)
    ├── docs/                       # Project documentation (PRD, this doc, etc.)
    │   ├── prd/
    │   ├── architecture/
    │   ├── project-brief/
    │   └── research/
    ├── supabase/                   # Supabase specific configurations
    │   └── migrations/             # SQL migration files (if using Supabase CLI)
    ├── tests/                      # Test files (Jest/React Testing Library)
    ├── .env.example
    ├── .gitignore
    ├── next.config.js
    ├── package.json
    ├── tailwind.config.js
    ├── tsconfig.json
    └── README.md


### Key Directory Descriptions (Updated)

- **app/**: Next.js App Router structure. Route groups `(auth)` and `(dashboard)` manage layouts and access control.

- **components/**: Reusable React components, organized by feature or common UI elements (e.g., `components/ui` for shadcn-inspired elements).

- **lib/**: Shared utilities, Supabase client interactions, database schema definitions (e.g., using Drizzle ORM or Zod for validation), and query functions/services.

- **public/**: Static assets including PWA manifest and service worker.

- **supabase/migrations/**: (New) Suggested location for SQL migration files if using Supabase CLI for schema management.

- **docs/**: Project documentation, now with subfolders for better organization.


## API Reference

### External APIs Consumed

#### Email Service API

- **Purpose:** Send notification emails (deal updates, reminders) and invoices to clients.

- **Potential Candidates & Considerations:**

  1. **Supabase Auth Email (for Auth-related emails):** Handles verification, password resets.

  2. **Resend (resend.com):** Modern email API, good for transactional emails. Simple integration.

  3. SendGrid / Postmark: Robust, feature-rich services, potentially more complex/costly for MVP.

     Architectural Implication: Choice affects setup complexity and cost. For MVP, leveraging Supabase for auth emails and a simple service like Resend for other transactional emails is recommended.

- **Authentication:** API Key (stored in environment variables).

- **Key Endpoints Used (Example using a generic service like Resend):**

  - **`POST https://api.resend.com/emails`:**

    - Description: Sends an email.

    - Request Body Schema (Simplified):

          {
            from: string; // e.g., 'CDH <notifications@cdh.com>'
            to: string | string[];
            subject: string;
            html: string; // HTML content of the email
            // attachments (if sending PDF invoices directly)
          }

    - Success Response: `{ id: string }`


### Internal APIs Provided (Next.js API Routes)

_General principles: All API routes will enforce authentication using Supabase JWTs. Input validation will be performed using Zod schemas. Consistent error handling will be applied._


#### Deals API (`/api/deals`)

- **Endpoints:**

  - **`GET /api/deals`:**

    - Description: Get all deals for the authenticated creator.

    - Query Parameters: `status` (optional), `page` (optional), `limit` (optional).

    - Success Response Schema: `{ deals: Array<Deal>, pagination: { total: number, page: number, limit: number } }`

  - **`GET /api/deals/:id`:**

    - Description: Get a specific deal by ID.

    - Success Response Schema: `Deal`

  - **`POST /api/deals`:**

    - Description: Create a new deal.

    - Request Body Schema: `CreateDealRequest` (aligns with Deal entity, excluding server-generated fields).

    - Success Response Schema: `Deal`

  - **`PUT /api/deals/:id`:**

    - Description: Update an existing deal.

    - Request Body Schema: `UpdateDealRequest` (partial Deal entity).

    - Success Response Schema: `Deal`

  - **`DELETE /api/deals/:id`:** (Or `PATCH /api/deals/:id/cancel` for soft delete/cancellation)

    - Description: Cancel or delete a deal.

    - Success Response Schema: `{ success: true }` or updated `Deal` with 'cancelled' status.


#### Deliverables API (`/api/deals/:dealId/deliverables`) - _**New**_

- **Purpose:** Manage deliverables for a specific deal.

- **Authentication:** Required (JWT from Supabase Auth).

- **Endpoints:**

  - `GET /`: List deliverables for a deal.

    - Success Response Schema: `{ deliverables: Array<Deliverable> }`

  - `POST /`: Create a new deliverable for a deal.

    - Request Body Schema: `CreateDeliverableRequest`.

    - Success Response Schema: `Deliverable`.

  - `PUT /:deliverableId`: Update a deliverable.

    - Request Body Schema: `UpdateDeliverableRequest`.

    - Success Response Schema: `Deliverable`.

  - `DELETE /:deliverableId`: Delete a deliverable.

    - Success Response Schema: `{ success: true }`.


#### Invoices API (`/api/invoices`)

- **Endpoints:**

  - **`GET /api/invoices`:**

    - Description: Get all invoices for the authenticated creator.

    - Query Parameters: `status` (optional), `page` (optional), `limit` (optional).

    - Success Response Schema: `{ invoices: Array<Invoice>, pagination: { total: number, page: number, limit: number } }`

  - **`GET /api/invoices/:id`:**

    - Description: Get a specific invoice by ID.

    - Success Response Schema: `Invoice`

  - **`POST /api/invoices`:**

    - Description: Create a new invoice from a deal.

    - Request Body Schema: `CreateInvoiceRequest` (likely `dealId` and any overrides/notes).

    - Success Response Schema: `Invoice`

  - **`PUT /api/invoices/:id`:**

    - Description: Update an existing invoice (e.g., status, notes).

    - Request Body Schema: `UpdateInvoiceRequest`.

    - Success Response Schema: `Invoice`

  - **`POST /api/invoices/:id/send`:**

    - Description: Mark an invoice as sent and trigger email to client.

    - Success Response Schema: `{ success: true, messageId?: string }` (messageId if email sent directly).


#### Reminders API (`/api/reminders`) - _**New**_

- **Purpose:** Manage reminders for deals, deliverables, and invoices.

- **Authentication:** Required (JWT from Supabase Auth).

- **Endpoints:**

  - `GET /`: List reminders for the user (can be filtered by `related_type`, `related_id`).

    - Success Response Schema: `{ reminders: Array<Reminder> }`.

  - `POST /`: Create a new reminder.

    - Request Body Schema: `CreateReminderRequest`.

    - Success Response Schema: `Reminder`.

  - `PUT /:reminderId`: Update a reminder.

    - Request Body Schema: `UpdateReminderRequest`.

    - Success Response Schema: `Reminder`.

  - `DELETE /:reminderId`: Delete a reminder.

    - Success Response Schema: `{ success: true }`.


#### User Settings API (`/api/user-settings`)

- **Endpoints:**

  - **`GET /api/user-settings`:**

    - Description: Get current user's profile and application settings.

    - Success Response Schema: `CombinedUserSettings` (including profile from `users` table and settings from `user_settings` table).

  - **`PUT /api/user-settings`:**

    - Description: Update user's profile and application settings.

    - Request Body Schema: `UpdateCombinedSettingsRequest`.

    - Success Response Schema: `CombinedUserSettings`.

  - **`POST /api/user-settings/export-data`:**

    - Description: Initiate data export for the user (CSV format as per PRD).

    - Success Response Schema: `{ success: true, message: "Data export initiated. You will receive an email." }` or direct CSV download if feasible.


## Data Models

### Core Application Entities (Reconciled with PRD v1.7)

_Justification for `Clients` Entity: While not explicitly a top-level entity in the PRD's initial data model, the concept of a "brand" or "counterparty" is central to deals and invoices. Creating a `Clients` entity allows for better organization of counterparty information (name, email, company details), reduces data redundancy if a creator works with the same client on multiple deals, and lays a better foundation for future marketplace features where brands/clients might have more direct interaction. A `Deal` will typically have one `Client` associated with it, and a `Client` record will be owned by a `User` (the creator)._


#### User (Aligns with PRD)

- **Schema Definition (Conceptual - see SQL for DB fields):**

      interface User {
        id: string; // (from Supabase Auth)
        email: string;
        name?: string; // PRD: name, profile_image, business_name, business_address
        profile_image_url?: string;
        business_name?: string;
        business_address?: string; // Could be a JSONB object
        created_at: Date;
        updated_at: Date;
      }


#### Client (New, Justified Above)

- **Description:** Represents the brand or counterparty a creator is dealing with.

- **Schema Definition:**

      interface Client {
        id: string; // UUID
        user_id: string; // FK to User (creator who owns this client record)
        name: string; // Brand/Company Name or Contact Person
        email?: string;
        contact_person_name?: string;
        // Additional fields like phone, address can be added
        created_at: Date;
        updated_at: Date;
      }


#### Deal (Aligned with PRD, status reconciled)

- **Schema Definition:**

      interface Deal {
        id: string; // UUID
        user_id: string; // FK to User
        client_id: string; // FK to Client
        brand_name: string; // Kept for simplicity, could be derived from Client.name
        description: string;
        value: number; // in cents
        currency: string; // e.g., 'USD'
        status: 'negotiation' | 'active' | 'completed' | 'cancelled'; // Aligned with PRD
        start_date?: Date;
        end_date?: Date;
        created_at: Date;
        updated_at: Date;
      }


#### Deliverable (Added from PRD)

- **Description:** Specific tasks or items to be delivered as part of a deal.

- **Schema Definition:**

      interface Deliverable {
        id: string; // UUID
        deal_id: string; // FK to Deal
        user_id: string; // FK to User (for RLS convenience)
        description: string;
        due_date?: Date;
        status: 'pending' | 'in_progress' | 'completed';
        created_at: Date;
        updated_at: Date;
      }


#### Invoice (Aligned with PRD, status reconciled)

- **Schema Definition:**

      interface Invoice {
        id: string; // UUID
        deal_id: string; // FK to Deal
        user_id: string; // FK to User (creator)
        // client_id: string; // FK to Client (can be derived from deal)
        invoice_number: string; // Auto-generated or user-input
        issue_date: Date;
        due_date: Date;
        amount: number; // in cents
        currency: string;
        status: 'draft' | 'sent' | 'paid' | 'overdue'; // Aligned with PRD
        // items: InvoiceItem[]; // For MVP, amount might be total from deal. Line items are future.
        notes?: string;
        created_at: Date;
        updated_at: Date;
      }


#### Reminder (Added from PRD)

- **Description:** Reminders for deals, deliverables, or invoices.

- **Schema Definition:**

      interface Reminder {
        id: string; // UUID
        user_id: string; // FK to User
        related_id: string; // ID of the deal, deliverable, or invoice
        related_type: 'deal' | 'deliverable' | 'invoice';
        reminder_date: Date; // TIMESTAMPTZ in DB
        description?: string; // Optional note for the reminder
        status: 'pending' | 'sent' | 'dismissed';
        created_at: Date;
        updated_at: Date;
      }


#### UserSettings (AD addition, ensure covers PRD)

- **Schema Definition (Conceptual):**

      interface UserSettings {
        user_id: string; // PK, FK to User
        notifications: { // Matches PRD 2.4
          email_deal_updates: boolean;
          in_app_deal_updates: boolean;
          email_invoice_reminders: boolean;
          in_app_invoice_reminders: boolean;
          // frequency (Future)
        };
        invoice_defaults: { // Matches PRD 2.4
          payment_terms?: string;
          business_details_for_invoice?: string; // e.g., address, tax ID
          preferred_payment_methods_text?: string;
          logo_url?: string;
        };
      }


### Database Schema (Reconciled with PRD v1.7)

    -- Users Table (public.users for profile information, linked to auth.users)
    CREATE TABLE public.users (
      id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
      email TEXT UNIQUE NOT NULL, -- Mirrored from auth.users for convenience, or joined
      name TEXT,
      profile_image_url TEXT,
      business_name TEXT,
      business_address TEXT, -- Consider JSONB for structured address: { street, city, state, postalCode, country }
      created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can only select/update their own profile.
    -- Trigger: Create a function to copy user from auth.users to public.users on new auth user creation.

    -- Clients Table
    CREATE TABLE public.clients (
      id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
      user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE,
      name TEXT NOT NULL, -- Brand/Company Name or Contact Person
      email TEXT,
      contact_person_name TEXT,
      -- other fields like phone TEXT, address JSONB
      created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can manage (CRUD) their own clients.

    -- Deals Table
    CREATE TABLE public.deals (
      id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
      user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE,
      client_id UUID REFERENCES public.clients(id) ON DELETE SET NULL, -- Can be NOT NULL if a client is always required
      brand_name TEXT NOT NULL, -- As per PRD. Can be denormalized from clients.name or a separate field.
      description TEXT,
      value INTEGER NOT NULL DEFAULT 0, -- In cents
      currency TEXT NOT NULL DEFAULT 'USD',
      status TEXT NOT NULL DEFAULT 'negotiation' CHECK (status IN ('negotiation', 'active', 'completed', 'cancelled')), -- Aligned with PRD
      start_date TIMESTAMPTZ,
      end_date TIMESTAMPTZ,
      created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can manage their own deals.

    -- Deliverables Table
    CREATE TABLE public.deliverables (
      id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
      deal_id UUID NOT NULL REFERENCES public.deals(id) ON DELETE CASCADE,
      user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE, -- Denormalized for easier RLS at deliverable-level if needed
      description TEXT NOT NULL,
      due_date TIMESTAMPTZ,
      status TEXT NOT NULL DEFAULT 'pending' CHECK (status IN ('pending', 'in_progress', 'completed')),
      created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can manage deliverables associated with their own deals.

    -- Invoices Table
    CREATE TABLE public.invoices (
      id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
      deal_id UUID NOT NULL REFERENCES public.deals(id) ON DELETE CASCADE, -- Invoice is always linked to a deal
      user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE, -- Denormalized for easier RLS
      -- client_id is implicitly known via deal_id -> deals.client_id
      invoice_number TEXT NOT NULL UNIQUE, -- Should be unique per user or globally? Per user is simpler.
      issue_date DATE NOT NULL,
      due_date DATE NOT NULL,
      amount INTEGER NOT NULL DEFAULT 0, -- In cents, typically sum of items or deal value portion
      currency TEXT NOT NULL DEFAULT 'USD',
      status TEXT NOT NULL DEFAULT 'draft' CHECK (status IN ('draft', 'sent', 'paid', 'overdue')), -- Aligned with PRD
      notes TEXT,
      -- items JSONB DEFAULT '[]'::jsonb, -- For future line items; MVP might use deal description
      created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can manage their own invoices.

    -- Reminders Table
    CREATE TABLE public.reminders (
      id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
      user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE,
      related_id UUID NOT NULL, -- FK to deals.id, deliverables.id, or invoices.id
      related_type TEXT NOT NULL CHECK (related_type IN ('deal', 'deliverable', 'invoice')),
      reminder_date TIMESTAMPTZ NOT NULL,
      description TEXT,
      status TEXT NOT NULL DEFAULT 'pending' CHECK (status IN ('pending', 'sent', 'dismissed')),
      created_at TIMESTAMPTZ DEFAULT NOW() NOT NULL,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can manage their own reminders.
    -- Index: Consider an index on (user_id, reminder_date, status) for efficient querying of pending reminders.

    -- User Settings Table
    CREATE TABLE public.user_settings (
      user_id UUID PRIMARY KEY REFERENCES public.users(id) ON DELETE CASCADE,
      notifications JSONB DEFAULT '{
        "email_deal_updates": true, 
        "in_app_deal_updates": true, 
        "email_invoice_reminders": true, 
        "in_app_invoice_reminders": true
      }'::jsonb,
      invoice_defaults JSONB DEFAULT '{
        "payment_terms": "Net 30", 
        "business_details_for_invoice": "", 
        "preferred_payment_methods_text": "",
        "logo_url": ""
      }'::jsonb,
      updated_at TIMESTAMPTZ DEFAULT NOW() NOT NULL
    );
    -- RLS: Enable RLS. Users can manage their own settings.


## Authentication & Authorization

### Authentication Flow

The CDH web application uses Supabase Auth for authentication, supporting both email/password and Google social authentication as specified in the PRD (Google for MVP). The authentication flow is as follows:

1. **User Registration (Email/Password):**

   - User enters email, password, and name.

   - Client-side validation is performed (e.g., using Zod).

   - Request is sent from the client (or via a Next.js API route for extra logic) to Supabase Auth (`supabase.auth.signUp`).

   - Supabase creates a new user in the `auth.users` table.

   - A Supabase Auth trigger (SQL function) is configured to automatically create a corresponding entry in the `public.users` table, populating initial profile fields.

   - Supabase (if configured for email confirmation) sends a verification email to the user.

2. **User Registration (Google Social Login):**

   - User clicks "Sign up with Google".

   - Client initiates Supabase Google OAuth flow (`supabase.auth.signInWithOAuth({ provider: 'google' })`).

   - User authenticates with Google.

   - Upon successful Google authentication, Supabase creates/updates the user in `auth.users` and the trigger populates/updates `public.users`.

   - User is redirected back to the application with an active session.

3. **Email Verification:**

   - User clicks the verification link in the email sent by Supabase.

   - Supabase verifies the email and updates the user's `email_confirmed_at` status in `auth.users`.

   - User is typically redirected to a confirmation page or the application dashboard.

4. **User Login (Email/Password):**

   - User enters email and password.

   - Client sends credentials to Supabase Auth (`supabase.auth.signInWithPassword`).

   - Upon successful authentication, Supabase returns a session object containing a JWT.

   - The Supabase client library securely stores the JWT (typically in localStorage).

   - User is redirected to the dashboard.

5. **User Login (Google Social Login):**

   - Similar to registration, user clicks "Sign in with Google".

   - Supabase handles the OAuth flow and establishes a session.

6. **Password Reset:**

   - User requests a password reset from the login page, providing their email.

   - Client calls `supabase.auth.resetPasswordForEmail`.

   - Supabase sends a password reset email with a unique link.

   - User clicks the link, is taken to a password reset page in the app, enters a new password.

   - Client calls `supabase.auth.updateUser` with the new password.

   - User is redirected to login with the new credentials.

7. **Session Management:**

   - The Supabase client library handles session persistence and refresh tokens automatically.

   - Middleware in Next.js will check for a valid session on protected routes.

_Trigger for public.users creation: A Supabase Auth trigger should be configured to automatically create a corresponding record in `public.users` upon new user sign-up in `auth.users`. This is standard practice and its setup (e.g., via SQL function and trigger) should be documented or part of the Supabase project setup checklist._

    sequenceDiagram
        actor User
        participant Frontend
        participant NextApp as Next.js (Client/Server)
        participant SupabaseAuth as Supabase Auth
        participant SupabaseDB as Supabase DB (public.users)
        participant EmailService as Email Service

        User->>Frontend: Fills Registration Form (Email/Pass)
        Frontend->>NextApp: (Client) Calls supabase.auth.signUp()
        NextApp->>SupabaseAuth: signUp({email, password})
        SupabaseAuth->>SupabaseAuth: Creates user in auth.users
        SupabaseAuth-->>EmailService: (If email confirm enabled) Send Verification Email
        SupabaseAuth->>SupabaseDB: (Via Trigger) Insert into public.users
        SupabaseAuth-->>NextApp: Returns session/user
        NextApp-->>Frontend: Registration Success
        Frontend-->>User: Shows Confirmation / Prompts to Verify Email

        User->>Frontend: Clicks "Sign in with Google"
        Frontend->>NextApp: (Client) Calls supabase.auth.signInWithOAuth({provider:'google'})
        NextApp->>SupabaseAuth: Initiates Google OAuth flow
        SupabaseAuth-->>User: Redirects to Google for Auth
        User-->>SupabaseAuth: Authenticates with Google
        SupabaseAuth->>SupabaseAuth: Creates/Updates auth.users
        SupabaseAuth->>SupabaseDB: (Via Trigger) Inserts/Updates public.users
        SupabaseAuth-->>NextApp: Returns session/user (Redirect back to app)
        NextApp-->>Frontend: Login Success
        Frontend-->>User: Redirects to Dashboard

**Figure 3: Authentication Flow Sequence Diagram (Illustrative)**


### Authorization Strategy & Future RBAC

Authorization in the CDH web application is implemented using a combination of:

1. **Protected Routes (Client-side & Middleware):**

   - Next.js middleware (e.g., in `middleware.ts`) checks for a valid Supabase session (JWT) on requests to protected routes (e.g., `/dashboard/*`).

   - Unauthenticated users are redirected to the login page (`/sign-in`).

   - Client-side checks using Supabase auth state also protect components and redirect if the session is lost.

   - Route groups in the App Router (e.g., `(dashboard)`) are used to apply specific layouts and protection logic.

2. **Row Level Security (RLS) in Supabase:**

   - Supabase PostgreSQL RLS policies are the primary mechanism for restricting data access at the database level.

   - Each table (`deals`, `invoices`, `clients`, `deliverables`, `reminders`, `user_settings`) has policies ensuring users can only perform CRUD operations on their own data (typically by checking `auth.uid() = user_id`).

   - Example RLS policy for the `deals` table:

         -- Allow users to select their own deals
         CREATE POLICY "Users can select their own deals"
         ON public.deals FOR SELECT
         USING (auth.uid() = user_id);

         -- Allow users to insert their own deals
         CREATE POLICY "Users can insert their own deals"
         ON public.deals FOR INSERT
         WITH CHECK (auth.uid() = user_id);

         -- Allow users to update their own deals
         CREATE POLICY "Users can update their own deals"
         ON public.deals FOR UPDATE
         USING (auth.uid() = user_id)
         WITH CHECK (auth.uid() = user_id);

         -- Allow users to delete their own deals
         CREATE POLICY "Users can delete their own deals"
         ON public.deals FOR DELETE
         USING (auth.uid() = user_id);

   - RLS is enabled by default on tables, and specific permissive policies are added.

3. **API Route Protection (Server-side in Next.js):**

   - Next.js API routes (e.g., `/api/deals`) that perform CUD operations or fetch sensitive data will verify the JWT from the Supabase session on the server using the Supabase Admin SDK or by validating the user's session cookie.

   - Requests without valid authentication are rejected with appropriate HTTP status codes (e.g., 401 Unauthorized).

   - Further business logic checks can be performed within API routes if needed, beyond RLS.

Future RBAC Considerations: The current user\_id centric RLS provides a strong foundation. For future "Team Collaboration" features (PRD Section 9.3), the architecture can be extended by introducing:

\* A teams table.

\* A team\_memberships table linking users to teams with specific roles (e.g., 'owner', 'admin', 'member').

\* RLS policies would then be updated to check for team membership and roles in addition to user\_id for shared resources. This could involve more complex SQL functions in RLS policies to check permissions based on team roles.

This approach allows for granular control without a major overhaul of the current auth model.


## Non-Functional Requirements Implementation

### Performance

To meet the performance targets specified in the PRD (initial page load < 2s, Time to Interactive < 3s, UI interactions < 100ms, API response < 500ms):

1. **React Server Components (RSC) & Server-Side Rendering (SSR):**

   - Leveraging Next.js App Router's server components by default to reduce client-side JavaScript bundle size and move data fetching to the server.

   - Utilizing SSR for dynamic, authenticated pages (e.g., dashboard views) that require fresh, user-specific data on each request.

   - Employing `loading.tsx` conventions and React Suspense for improved perceived performance during data fetching in RSCs.

2. **Static Site Generation (SSG) & Incremental Static Regeneration (ISR):**

   - Using SSG for marketing pages, documentation, and other static content (e.g., landing page `app/page.tsx`).

   - Considering ISR for pages with data that changes infrequently but still benefits from static generation (e.g., blog, public creator profiles if added later).

3. **Client-Side Data Fetching & Caching:**

   - For client components requiring data or for mutations, libraries like SWR or React Query will be used for efficient data fetching, caching, optimistic updates, and background revalidation. This helps in making UI interactions feel instantaneous.

4. **Code Splitting:**

   - Automatic code splitting by Next.js based on routes and dynamic imports (`next/dynamic`) for large components or libraries not needed on initial load.

5. **Image Optimization:**

   - Using the `next/image` component for automatic image optimization (resizing, format conversion like WebP, lazy loading).

6. **Efficient Data Fetching from Supabase:**

   - Implementing pagination for all list views (deals, invoices, etc.) in API routes and frontend queries.

   - Selecting only necessary columns from Supabase tables (`select('column1, column2')`).

   - Using appropriate filters and indexing in Supabase to speed up queries.

7. **Bundle Analysis:**

   - Regularly using tools like `@next/bundle-analyzer` to inspect JavaScript bundles and identify areas for optimization.

8. **CDN Usage:**

   - Leveraging Vercel's Edge Network (or other CDN if applicable) for caching static assets and delivering content closer to the user.


### Scalability

To support the long-term goal of 10,000 concurrent users (PRD Section 3.1):

1. **Stateless Application Logic:**

   - Next.js API routes and server components will be designed to be stateless. User session state is managed via JWTs handled by Supabase Auth, allowing for horizontal scaling of the Next.js application instances on Vercel (serverless functions).

2. **Scalable Backend (Supabase):**

   - Supabase is built on PostgreSQL and designed for scalability. As load increases, Supabase offers options for scaling the database instance.

   - Efficient database design (proper indexing, normalized where appropriate) and optimized queries are crucial.

3. **Connection Pooling:**

   - Supabase manages database connections efficiently. Ensure client-side and server-side Supabase clients are used correctly to leverage this.

4. **Asynchronous Operations:**

   - For potentially long-running tasks (e.g., complex report generation in the future, bulk email sending), consider using background jobs or queues (e.g., Supabase Edge Functions with a message queue, or external services) to avoid blocking main application threads.

5. **Rate Limiting:**

   - Implement rate limiting on critical API endpoints to prevent abuse and ensure fair usage (PRD Section 3.3).

6. **Monitoring and Auto-scaling (Hosting Platform):**

   - Vercel's serverless infrastructure generally auto-scales based on demand. Monitoring application performance and Supabase database load will be key to identifying scaling needs or bottlenecks.


### Security

To implement comprehensive security measures (PRD Section 3.3 & 10.3):

1. **Authentication Security:**

   - Secure password hashing, JWT management, and social login security are handled by Supabase Auth.

   - Enforce strong password policies client-side and rely on Supabase's defaults.

   - Implement CSRF protection (Next.js often handles this with modern patterns, but verify, especially for API routes handling form data not via standard form submissions). For API routes, ensure correct HTTP methods are used and consider custom CSRF tokens if needed.

   - Rate limiting for authentication attempts (e.g., login, password reset) to prevent brute-force attacks, potentially via Supabase Auth settings or custom API logic.

2. **Data Security & Access Control:**

   - **Row Level Security (RLS)** in Supabase is the cornerstone, ensuring users can only access their own data. Policies will be defined for all tables.

   - **Input Validation:** Comprehensive validation on **both client-side** (using Zod with forms for immediate feedback) **and server-side** (in Next.js API Routes using Zod before any database operation) to prevent injection attacks (SQLi, XSS via stored data) and ensure data integrity.

   - **Parameterized Queries:** Using Supabase client libraries ensures parameterized queries, preventing SQL injection.

   - **Data Encryption:** Data in transit is secured by HTTPS. Supabase encrypts data at rest.

3. **API Security:**

   - All Next.js API routes performing sensitive operations will require valid JWT authentication.

   - Proper HTTP methods (GET, POST, PUT, DELETE) will be enforced.

   - Sensitive information should not be exposed in GET request URLs.

   - Rate limiting on critical API endpoints.

4. **Frontend Security:**

   - **XSS Protection:** React inherently escapes content rendered in JSX. Use `dangerouslySetInnerHTML` with extreme caution and only with sanitized HTML. Sanitize any user-generated content that might be rendered as HTML.

   - **Content Security Policy (CSP):** Implement CSP headers via Next.js configuration (`next.config.js`) to restrict sources of scripts, styles, images, etc., reducing XSS risk.

   - **Secure Cookie Handling:** If using cookies directly (though Supabase client often manages tokens in localStorage), ensure they are HttpOnly, Secure, and SameSite.

   - **Dependency Management:** Regularly update dependencies and use tools like `npm audit` or Snyk to identify and mitigate vulnerabilities in third-party packages.

5. **HTTPS Enforcement:** Ensure the application is always served over HTTPS (typically handled by the hosting platform like Vercel).


### PWA Capabilities

To implement PWA features for an installable, mobile-like experience (PRD Section 5.4):

1. **Service Worker (`public/service-worker.js`):**

   - Implement a service worker for caching strategies (cache-first for static assets, network-first or stale-while-revalidate for API data).

   - Handle offline functionality: For MVP, enable viewing of cached deals and invoices (read-only API responses for GET requests). The service worker's caching strategy for API responses will specifically target GET requests for deals and invoices to enable this read-only access.

   - Consider background sync for future features (e.g., queueing actions made offline).

2. **Web App Manifest (`public/manifest.json`):**

   - Create `manifest.json` with application metadata: `name`, `short_name`, `icons` (various sizes), `start_url`, `display` (e.g., `standalone`), `theme_color`, `background_color`.

3. **Installation Experience:**

   - Ensure the app meets PWA installability criteria (HTTPS, manifest, service worker).

   - Optionally, implement a custom install prompt (`beforeinstallprompt` event) for better UX.

4. **Push Notifications (Post-MVP or if critical for reminders):**

   - If implemented for MVP reminders, this would involve:

     - Requesting user permission for notifications.

     - Using the Push API and Notification API.

     - Managing push subscriptions (e.g., storing them in Supabase linked to the user).

     - Sending notifications from a backend service (e.g., Next.js API route or Supabase Edge Function) when a reminder is due.


### Accessibility & Internationalization

To ensure the application is usable by a wide range of users (PRD Sections 3.4, 3.5):

1. **Accessibility (WCAG 2.1 AA):**

   - **Semantic HTML:** Use HTML5 elements correctly to define structure and meaning.

   - **ARIA Attributes:** Use ARIA (Accessible Rich Internet Applications) attributes where necessary to enhance accessibility for dynamic content and custom components, but prioritize native HTML semantics.

   - **Keyboard Navigation:** Ensure all interactive elements are focusable and operable via keyboard alone, in a logical order.

   - **Focus Management:** Manage focus appropriately, especially in modals and dynamic UI changes.

   - **Color Contrast:** Adhere to minimum contrast ratios for text and UI elements (e.g., 4.5:1 for normal text).

   - **Image Alt Text:** Provide descriptive alt text for all informative images.

   - **Form Accessibility:** Ensure all form inputs have associated labels and clear error messages.

   - **Testing:** Regularly test with screen readers (e.g., NVDA, VoiceOver) and automated accessibility checking tools (e.g., Axe, Lighthouse).

2. **Internationalization (i18n):**

   - **Framework:** Use a library like `next-intl` or `react-i18next` for managing translations.

   - **Locale Detection:** For MVP, detect user locale from browser/OS settings (`navigator.language`) to format dates, numbers, and currency.

   - **Translation Files:** Structure translation strings in JSON or similar files, organized by locale (e.g., `locales/en/common.json`, `locales/es/common.json`).

   - **Architecture for Future Languages:** Design components and services to easily consume translated strings based on the active locale. Ensure the database schema can support localized content if needed in the future (though UI text is the primary focus for MVP).

   - **Date/Currency Formatting:** Utilize browser's `Intl` object or libraries like `date-fns` (with locale support) for correct formatting based on detected locale.


## Deployment Strategy

### CI/CD Pipeline

The CDH web application will be deployed using a robust CI/CD pipeline to automate testing and deployment:

1. **Version Control System:** Git, hosted on GitHub.

2. **CI/CD Platform:** GitHub Actions (as indicated in project structure `/.github/workflows/main.yml`).

3. **Workflow Triggers:**

   - On pushes to the `main` branch (for production-like or staging deployments).

   - On pushes to feature branches or pull requests to `main` (for running tests, linting, and preview deployments).

4. **Pipeline Stages:**

   - **Checkout Code:** Fetch the latest code.

   - **Setup Environment:** Install Node.js, dependencies (`pnpm install`).

   - **Lint & Format Check:** Run ESLint, Prettier.

   - **Type Check:** Run TypeScript compiler (`tsc --noEmit`).

   - **Run Tests:** Execute unit tests, integration tests (e.g., using Jest, React Testing Library).

   - **Build Application:** Build the Next.js application (`pnpm build`).

   - **Deploy:** Deploy to the appropriate environment on Vercel.

     - Preview deployments for Pull Requests.

     - Staging deployment (e.g., from `develop` branch or manually triggered from `main`).

     - Production deployment (e.g., from `main` branch after successful staging, potentially with manual approval).

5. **Notifications:** Notify the team of build/deployment status (e.g., via Slack or email).


### Hosting

As specified in the PRD (Section 5.1), the application will be hosted on **Vercel**:

1. **Vercel Project Configuration:**

   - Connected to the GitHub repository for seamless Git integration.

   - Automatic deployments triggered by pushes to configured branches and PRs.

   - Environment variables configured securely in Vercel project settings for different environments (Development, Preview, Production). These will include Supabase URL/keys, email service API keys, etc.

2. **Custom Domains:**

   - Configured for production (e.g., `cdh.app`).

   - Automatic preview URLs for each deployment/PR.

   - Potentially a staging domain (e.g., `staging.cdh.app`).

3. **Edge Network:**

   - Leverage Vercel's global Edge Network for fast content delivery and caching of static assets.

   - Next.js API Routes will run as Edge Functions or Serverless Functions depending on configuration and needs.


### Monitoring & Backup

To ensure application health and data integrity (PRD Section 10.4):

1. **Monitoring:**

   - **Application Performance Monitoring (APM):** Vercel Analytics provides insights into frontend performance (Web Vitals). For backend/API route monitoring, consider integrating a service like Sentry, Logtail, or Vercel's built-in logging for serverless functions.

   - **Error Tracking:** Sentry or similar for capturing and alerting on frontend and backend errors.

   - **Uptime Monitoring:** External service (e.g., UptimeRobot, Better Uptime) to monitor the availability of the production application.

   - **Supabase Monitoring:** Utilize Supabase's built-in dashboard for database performance, query analysis, and resource usage.

2. **Backup Strategy (Supabase):**

   - Supabase provides automated daily backups for PostgreSQL databases.

   - Point-In-Time Recovery (PITR) capabilities should be confirmed based on the Supabase plan.

   - Define a backup retention policy (e.g., 7-30 days, depending on plan and requirements).

   - Regularly test the restore process (e.g., to a staging environment).

   - Consider manual backups before major schema changes or data migrations.


## Error Handling & Logging

### Error Handling Strategy

A consistent error handling strategy will be implemented across the application:

1. **Frontend Error Handling (Next.js/React):**

   - **React Error Boundaries:** Wrap major UI sections or components with Error Boundaries (`componentDidCatch` or `static getDerivedStateFromError` for class components, or custom hooks for functional components) to catch rendering errors in their children, display a fallback UI, and log the error.

   - **Global Error Handler:** Implement a global JavaScript error handler (`window.onerror`, `window.onunhandledrejection`) to catch unhandled exceptions and report them to an error tracking service (e.g., Sentry).

   - **User-Friendly Error Messages:** Display clear, non-technical error messages to users. Avoid exposing raw error details. Provide guidance or next steps where possible.

   - **API Call Errors:** Gracefully handle errors from Next.js API routes or external API calls (e.g., network errors, 4xx/5xx responses) in client-side data fetching logic. Implement retry mechanisms for transient network errors where appropriate.

   - **Form Validation Errors:** Display inline validation errors next to form fields.

2. **API Route Error Handling (Next.js API Routes):**

   - **Consistent Error Response Format:** API routes will return errors in a standardized JSON format, e.g.:

         { "success": false, "error": { "code": "ERROR_CODE", "message": "Descriptive error message" } }

     Or for validation errors:

         { "success": false, "errors": [{ "field": "fieldName", "message": "Validation message" }] }

   - **Appropriate HTTP Status Codes:** Use standard HTTP status codes (e.g., 400 for bad request/validation, 401 for unauthorized, 403 for forbidden, 404 for not found, 500 for internal server error).

   - **Error Logging:** Log detailed error information server-side, including stack traces and request context, especially for 500 errors. For client-facing errors (4xx), log appropriately but avoid exposing sensitive internal details in the response.

   - **Centralized Error Handling Middleware/Utility:** Consider a utility function or middleware for API routes to standardize error responses and logging.

3. **Error Types to Handle:**

   - Validation Errors (user input, data integrity).

   - Authentication Errors (invalid credentials, token expiration, insufficient permissions for social login).

   - Authorization Errors (user trying to access resources they don't have permission for, caught by RLS or API logic).

   - Not Found Errors (e.g., trying to access a deal or invoice that doesn't exist or doesn't belong to the user).

   - Server Errors (unexpected issues in API routes or Supabase interactions).

   - Network Errors (client-side).


### Logging Approach

A structured logging approach will be adopted for debugging, monitoring, and auditing:

1. **Log Levels:** Standard log levels will be used:

   - **DEBUG:** Detailed information for development and troubleshooting.

   - **INFO:** General operational information about application flow (e.g., user login, deal creation).

   - **WARN:** Potential issues or unexpected situations that don't necessarily break functionality.

   - **ERROR:** Errors that affect functionality but don't crash the application.

   - **FATAL/CRITICAL:** Severe errors that might lead to application termination or instability.

2. **Log Storage & Management:**

   - **Development:** Logs will primarily go to the console (`console.log`, `console.error`, etc.).

   - **Production/Staging:**

     - Next.js API routes running on Vercel: Utilize Vercel's built-in logging for serverless functions.

     - Consider integrating with a dedicated logging service (e.g., Logtail, Axiom, Sentry for error context) for centralized log management, searching, and alerting.

     - Supabase provides its own logging for database queries and auth events, accessible via the Supabase dashboard.

3. **Log Content (Structured Logging):** Logs should be structured (e.g., JSON format) to include:

   - `timestamp`

   - `level` (DEBUG, INFO, WARN, ERROR)

   - `message` (descriptive log message)

   - `requestId` (a unique ID to trace a request through different services/components)

   - `userId` (if the user is authenticated and relevant to the log)

   - `context` (an object containing relevant contextual data, e.g., route, method, input parameters – sanitized for PII)

   - `stackTrace` (for ERROR level logs)

4. **Privacy Considerations in Logging:**

   - **No Sensitive PII:** Avoid logging personally identifiable information (PII) like full names in contexts where not strictly necessary, passwords, API keys, tokens, or full financial details directly in logs.

   - **Data Masking:** If sensitive data might inadvertently appear, implement masking for such fields.

   - **Compliance:** Ensure logging practices comply with relevant data protection regulations (e.g., GDPR, CCPA).

   - Log retention policies should be defined for the chosen logging service.


## Future Considerations & Scalability

The architecture is designed to support the future evolution of the CDH web application into a marketplace platform, as outlined in the "Out of Scope Ideas Post MVP" section of the PRD (Section 9):


### Marketplace Evolution

(PRD Section 9.1) The current modular design and Supabase backend provide a solid foundation.

1. **Extensible Data Model:** The `Users` and `Clients` tables can be extended with profiles. New tables for `Listings` (brand campaigns or creator service offerings), `Proposals/Bids`, `Contracts`, and `Reviews` can be added.

2. **API Design:** New API endpoints under `/api/marketplace/` or similar can be introduced.

3. **Authentication & Authorization:** The existing Supabase Auth can handle brand user types if they need to log in. RLS policies would be extended to manage permissions between creators and brands within the marketplace context.

4. **Payment Processing:** Integration with services like Stripe Connect would be required to facilitate payments between creators and brands. This would involve significant architectural additions for handling transactions, payouts, and compliance.


### Team Collaboration

(PRD Section 9.3) To support future "Team Collaboration" features:

1. **Multi-User Access & Roles:**

   - The data model would need a `teams` table and a `team_memberships` table (linking `users` to `teams` with roles like 'owner', 'admin', 'editor', 'viewer').

   - RLS policies would become more complex, checking `user_id` directly or via team membership and role-based permissions.

2. **Real-Time Collaboration:** For features like shared editing or activity feeds, Supabase Realtime subscriptions can be leveraged.


### Analytics & Reporting

(PRD Section 9.2) For future advanced analytics:

1. **Data Aggregation:** While Supabase can handle basic reporting, for complex analytics, data might be periodically exported or streamed to a data warehouse (e.g., BigQuery, Snowflake) or an analytics-focused database.

2. **Event Tracking:** Implement comprehensive event tracking (user actions, feature usage) using a service like Segment, Mixpanel, or custom logging to feed into analytics systems.


## Key Reference Documents

- **Product Requirements Document (PRD):** `web/docs/prd/creator-deal-hub-prd.md` (Version 1.7)

- **Project Brief:** `web/docs/project-brief/project-brief.md`

- **Market Analysis:** `web/docs/research/Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis.md`


## Change Log

|             |               |                |                                                                                                                                                                                                                                                                                                       |
| ----------- | ------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Version** | **Date**      | **Author**     | **Description**                                                                                                                                                                                                                                                                                       |
| 1.0         | June 15, 2023 | Fred (Initial) | Initial architecture document (as provided by user)                                                                                                                                                                                                                                                   |
| 1.1         | June 2, 2025  | Fred (BMAD)    | Comprehensive update based on critique: Data model reconciliation (Clients, Deliverables, Reminders, status enums), Auth RBAC note, State Management clarification, Email service candidates, NFR details (Offline, Validation), Migration folder, Diagram notes, Doc paths/versions, Changelog date. |
| 1.2         | June 2, 2025  | Fred (BMAD)    | Expanded sections to remove "(As Previously Defined)" shorthand, ensuring each section is self-contained with full details.a                                                                                                                                                                          |
