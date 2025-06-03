## Prompt for Architect (Fred): Creator's Deal Hub (CDH) Next.js Web Application Architecture Document

# To: Architect Agent (Fred)From: BMAD OrchestratorDate: June 2, 2025Subject: Creation of Architecture Document for Creator's Deal Hub (CDH) - Next.js Web Platform

### 1. Objective

# Your primary objective is to create a comprehensive ****Architecture Document**** for the new Creator's Deal Hub (CDH) Next.js web application. This document will serve as the technical blueprint for the development team, outlining the system's structure, components, interactions, and key technical decisions. It must align with the requirements defined in the ****Product Requirements Document (PRD) Version 1.7**** (ID: `creator-deal-hub-prd.md`) and the vision set forth in the ****Project Brief**** (`web/docs/project-brief/project-brief.md`).

### 2. Key Inputs & References

# - ****Primary Inputs****:

  - `creator-deal-hub-prd.md` (Version 1.7): "Product Requirements Document (PRD): Creator's Deal Hub (CDH) - Next.js Web Platform" – This is your main source for functional and non-functional requirements, user stories, epics, the initial data model (Section 10.2), and technical assumptions (Section 5 & 10).

  - `web/docs/project-brief/project-brief.md`: "Project Brief: CDH Next.js Web Application" – For understanding the overall project vision, goals, target audience, and strategic context.

- ****Supporting Contextual Documents & BMAD Resources****:

  - `web/docs/research/Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis.md`: For market context and potential future architectural considerations (e.g., marketplace evolution).

  - `bmad-agent/data/bmad-kb.md`: For understanding BMAD principles, your role as Architect, and interaction with other agents.

  - `bmad-agent/templates/architecture-tmpl.md`: Use this as the structural template for your Architecture Document.

  - `bmad-agent/checklists/architect-checklist.md`: As a guide and checklist for your process.

  - `bmad-agent/data/technical-preferences.txt` (if applicable and contains relevant preferences from the Vibe CEO).

  - Existing mobile application structure (`mobile/` directory in `tree_output.json`) for understanding current Supabase usage and data, but remember the Next.js app is a new build.

### 3. Scope of the Architecture Document

# Your Architecture Document should detail, at a minimum:1) ****Introduction & Overview****:

   - Purpose of the document.

   - Brief overview of the CDH Next.js web application and its goals (referencing PRD & Project Brief).

   - Architectural goals (e.g., scalability, maintainability, security, performance as per PRD NFRs Section 3).

2) ****System Architecture****:

   - High-level architectural diagrams (e.g., C4 model context or container diagrams).

   - Chosen architectural patterns (e.g., Layered, Microservices (if any part is planned as such), Modular Monolith).

   - Justification for key architectural decisions.

3) ****Technology Stack****:

   - Confirm and elaborate on the stack defined in PRD Section 5.1 (Next.js, Supabase, Tailwind CSS, etc.).

   - Specify versions or any particular libraries/frameworks to be used within this stack.

4) ****Frontend Architecture (Next.js)****:

   - Application structure (e.g., using Next.js App Router as per PRD Section 10.1).

   - Key Next.js features to be leveraged (SSR, SSG, ISR, API Routes as per PRD Section 5.2 & 10.1).

   - Approach to state management (React Context or other solutions as per PRD Section 10.1).

   - Component strategy (high-level, to be detailed further by Design Architect).

5) ****Backend Architecture (Supabase & Next.js API Routes)****:

   - Detailed plan for Supabase integration (database schema, RLS policies, authentication flow).

   - Design of Next.js API routes (for server-side logic not directly handled by Supabase client libraries).

   - Data access patterns and strategies.

6) ****Data Model & Database Design****:

   - Review, validate, and expand upon the initial Data Model provided in PRD Section 10.2.

   - Define relationships, constraints, and any necessary indexing.

   - Outline data migration considerations if any data from the old mobile app's backend needs to be preserved or transformed (though the brief implies a fresh start, this should be confirmed).

7) ****Authentication & Authorization****:

   - Detailed flow for user registration, login (email/password and Google social auth as per PRD 2.1), session management, and password reset using Supabase Auth.

   - Strategy for implementing role-based access control (RBAC) if applicable (even for future features like "Team Collaboration" noted in PRD Section 9.3).

   - Implementation of protected routes.

8) ****Integration Points****:

   - Identify any planned third-party service integrations (e.g., email services for notifications, payment gateways for future marketplace).

   - API design for internal services (Next.js API routes).

9) ****Non-Functional Requirements Implementation Strategy****:

   - ****Performance****: How the architecture will support the performance targets in PRD Section 3.1 (caching, efficient data fetching, Next.js rendering strategies).

   - ****Scalability****: Architectural provisions for the long-term goal of 10,000 concurrent users (PRD Section 3.1).

   - ****Security****: Detailed security measures beyond Supabase RLS (PRD Section 3.3 & 10.3), including input validation strategies, protection against common web vulnerabilities.

   - ****PWA Capabilities****: Architectural considerations for implementing PWA features (Service Workers, Web App Manifest, Push Notifications as per PRD Section 5.4).

   - ****Accessibility & Internationalization****: Architectural support for these NFRs (PRD Sections 3.4, 3.5).

10) ****Deployment Strategy****:

    - Elaborate on the CI/CD pipeline, environment management (dev, staging, prod), monitoring, and backup strategy outlined in PRD Section 10.4.

    - Confirm Vercel hosting or propose alternatives if necessary.

11) ****Error Handling & Logging****:

    - Strategy for consistent error handling across the application.

    - Approach to logging for debugging and monitoring.

12) ****Future Considerations & Scalability (Marketplace, etc.)****:

    - How the current architecture will support the "Out of Scope Ideas Post MVP" (PRD Section 9), particularly the marketplace evolution.

### 4. Key Tasks for the Architect (Fred)

# 1. ****Deep Dive into PRD and Project Brief****: Ensure full understanding of all requirements and the product vision.

2. ****Make & Justify Key Architectural Decisions****: Select appropriate patterns, technologies (within the given stack), and approaches.

3. ****Design System Components****: Define the major components of the system and how they interact.

4. ****Address NFRs****: Explicitly design the architecture to meet the specified non-functional requirements.

5. ****Document the Architecture****: Create the Architecture Document using the `bmad-agent/templates/architecture-tmpl.md` template. Diagrams are highly encouraged.

6. ****Collaborate with Design Architect****: Liaise with the Design Architect (Millie) regarding frontend architecture aspects that overlap (e.g., component design philosophy, state management impact on UI).

7. ****Review & Iterate****: Present the architecture for review by the Vibe CEO and potentially other agents, and iterate based on feedback.

8. ****Complete Architect Checklist****: Utilize and complete the `bmad-agent/checklists/architect-checklist.md`.

### 5. Deliverable

# A comprehensive ****Architecture Document**** for the Creator's Deal Hub - Next.js Web Platform, submitted for review.

### 6. Timeline

# This is a critical next step. Please outline your estimated timeline for delivering the first draft of the Architecture Document.Confirm your understanding of this prompt, Fred. You can begin by thoroughly reviewing the PRD Version 1.7 and the Project Brief, and then start structuring your Architecture Document using the provided template.
