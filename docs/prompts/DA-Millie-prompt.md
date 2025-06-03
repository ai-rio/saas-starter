## Prompt for Design Architect (Millie): Creator's Deal Hub (CDH) Next.js Web App UX/UI & Frontend Architecture

## To: Design Architect Agent (Millie)From: BMAD OrchestratorDate: June 2, 2025Subject: UX/UI Specification and Frontend Architecture Plan for Creator's Deal Hub (CDH) - Next.js Web Platform

### 1. Objective

## Your primary objectives are to:1) Create a comprehensive ****UX/UI Specification**** for the new Creator's Deal Hub (CDH) Next.js web application. This includes user flows, wireframes, mockups, and interaction design, ensuring a mobile-first, accessible, and user-friendly experience that fully leverages the capabilities of ****Next.js**** and ****shadcn/ui****.

2) Develop a detailed ****Frontend Architecture Plan**** that outlines the component strategy, state management approach, data fetching patterns, and overall structure for the Next.js frontend, designed to integrate seamlessly with ****Supabase**** as the backend.

3) (Optional) Produce ****AI UI Generation Prompts**** if deemed beneficial for accelerating design or exploring visual concepts.These deliverables must align with the ****Product Requirements Document (PRD) Version 1.7**** (ID: `creator-deal-hub-prd.md`) and the ****Architecture Document Version 1.2**** (ID: `creator-deal-hub-architecture.md`).

### 2. Key Inputs & References

## - ****Primary Inputs****:

  - `creator-deal-hub-prd.md` (Version 1.7): "Product Requirements Document (PRD)" – Your main source for user personas (Section 1.3), functional requirements (Section 2), user flows (Section 4.2), NFRs (Section 3, especially Mobile-First Design 3.2 & Accessibility 3.4), and Design System initial thoughts (Section 4.3).

  - `creator-deal-hub-architecture.md` (Version 1.2): "Creator's Deal Hub (CDH) Next.js Web Application Architecture Document" – For understanding the overall system architecture, ****specifically the confirmed technology stack (Next.js, Tailwind CSS, Supabase)****, frontend architecture initial thoughts (Section 5 - State Management), project structure (Section 6), and PWA capabilities (Section 10 - PWA). ****Ensure your designs and frontend architecture fully align with and leverage these core technologies.****

- ****Supporting Contextual Documents & BMAD Resources****:

  - `web/docs/project-brief/project-brief.md`: "Project Brief: CDH Next.js Web Application" – For overall project vision, goals, and target audience.

  - `web/docs/research/Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis.md`: For market context, creator pain points, and the SLC framework.

  - `bmad-agent/data/bmad-kb.md`: For understanding BMAD principles and your role.

  - `bmad-agent/templates/front-end-spec-tmpl.md`: Use as a template for the UX/UI Specification.

  - `bmad-agent/templates/front-end-architecture-tmpl.md`: Use as a template for the Frontend Architecture Plan.

  - `bmad-agent/checklists/frontend-architecture-checklist.md`: As a guide for your process.

  - `bmad-agent/tasks/create-uxui-spec.md`, `bmad-agent/tasks/create-frontend-architecture.md`, `bmad-agent/tasks/create-ai-frontend-prompt.md`: For task guidance.

  - Existing mobile application's design philosophy (conceptual reference from `mobile/docs/components-and-styling.md` and components `mobile/components/ui/`) but note PRD 1.7 Section 4.3 specifies the web UI will be a fresh build using web-native shadcn/ui patterns.

### 3. Scope of Deliverables

#### A. UX/UI Specification

## (Utilize `bmad-agent/templates/front-end-spec-tmpl.md`)1) ****Introduction****: Purpose, goals, alignment with PRD.

2) ****User Personas****: Elaborate or confirm personas from PRD (Section 1.3: Emma, Marcus, future Sarah) and how their needs drive UX decisions.

3) ****User Flows****:

   - Visualize and refine key user flows from PRD Section 4.2 (Onboarding, Deal Creation, Invoice Generation).

   - Develop flows for other MVP features: Deal Listing/Filtering, Deal Detail View, Invoice Listing/Filtering, Invoice Detail View, Settings management.

4) ****Information Architecture****: Site map, navigation structure for the web application, considering ****Next.js App Router capabilities****.

5) ****Wireframes****:

   - Low to medium-fidelity wireframes for all key screens and views identified in the user flows for the MVP.

   - Focus on layout, content hierarchy, and core interactions, ensuring mobile-first responsiveness.

6) ****Mockups / High-Fidelity Designs****:

   - Visually polished designs for key screens, demonstrating the look and feel, leveraging ****shadcn/ui components and Tailwind CSS styling****.

   - Apply the Design System principles (see below).

7) ****Interaction Design****:

   - Specify animations, transitions, and micro-interactions that enhance usability.

   - Detail states for interactive elements (hover, focus, active, disabled).

8) ****Mobile-First Responsive Design Strategy****:

   - Detailed breakpoints and how layouts/components adapt across screen sizes (mobile, tablet, desktop).

   - How touch interactions are optimized (PRD Section 3.2).

9) ****Accessibility Design****:

   - How designs adhere to WCAG 2.1 AA (PRD Section 3.4): color contrast, focus indicators, keyboard navigation considerations, ARIA attribute guidance for developers where custom components are used.

10) ****Design System / Component Library Details****:

    - Elaborate on PRD Section 4.3 and Architecture Document Section 4.3.

    - Specific guidance on ****effectively utilizing and customizing shadcn/ui components for the web, styled with Tailwind CSS****, to build the CDH interface.

    - Define the color palette, typography scale, iconography, spacing system, and grid system, ensuring harmony with the ****shadcn/ui aesthetic and Tailwind CSS capabilities****.

    - Style guide for custom components that extend or complement shadcn/ui.

#### B. Frontend Architecture Plan

## (Utilize `bmad-agent/templates/front-end-architecture-tmpl.md`)1) ****Introduction****: Purpose, alignment with overall Architecture Document, emphasizing the use of ****Next.js, shadcn/ui, and Supabase****.

2) ****Component Strategy****:

   - Philosophy for component design (e.g., Atomic Design principles, container vs. presentational components), focusing on reusability within a ****Next.js and shadcn/ui context****.

   - How ****shadcn/ui components**** will be the primary building blocks, how they will be utilized, customized, or extended.

   - Structure for custom components (e.g., `components/ui/`, `components/feature/`) within the ****Next.js project structure****.

3) ****State Management****:

   - Confirm and detail the implementation of React Context for global state (as per Arch Doc Section 5). Identify specific global states needed for MVP, considering how data from ****Supabase**** might influence this.

   - Guidelines for using local state (`useState`, `useReducer`).

   - Strategy for using SWR or React Query for client-side server state management (data from ****Supabase****), caching, and mutations (as per Arch Doc Section 5 & 10.1.3).

4) ****Data Fetching & Handling****:

   - Patterns for fetching data from ****Supabase**** in ****Next.js Server Components and Client Components**** within the App Router.

   - How data will be passed between components.

   - Client-side data validation approach (complementing server-side validation), potentially using Zod schemas that align with ****Supabase**** data structures.

5) ****Routing****:

   - Confirm usage of ****Next.js App Router**** (as per Arch Doc Section 6 & 10.1).

   - Define conventions for route parameters, dynamic routes, and layouts within `app/`.

6) ****Styling Architecture****:

   - Confirm ****Tailwind CSS**** usage (as per Arch Doc & PRD).

   - Conventions for organizing Tailwind classes, custom CSS if any (`globals.css`, component-level styles), in conjunction with ****shadcn/ui theming****.

7) ****Folder Structure (Frontend Focus)****:

   - Elaborate on the frontend-specific parts of the project structure outlined in Arch Doc Section 6 (e.g., `app/`, `components/`, `lib/` for frontend utilities/hooks leveraging ****Next.js and Supabase patterns****, `public/` for static assets).

8) ****Performance Best Practices (Frontend)****:

   - Code splitting (leveraging ****Next.js**** features like `next/dynamic`).

   - Lazy loading of images and components.

   - Memoization (React.memo, useMemo, useCallback).

   - Minimizing re-renders.

9) ****Error Handling (Frontend)****:

   - How React Error Boundaries will be used.

   - Displaying user-friendly error messages from API responses (originating from ****Next.js API routes/Supabase****).

10) ****PWA Considerations (Frontend)****:

    - How the frontend architecture supports the PWA capabilities outlined in Arch Doc Section 10.4 (e.g., service worker interaction, manifest integration).

#### C. (Optional) AI UI Generation Prompts

## - If applicable, develop prompts for AI UI generation tools to explore visual styles or generate initial component designs for specific parts of the application, keeping ****shadcn/ui and Tailwind CSS**** in mind.

### 4. Key Tasks for the Design Architect (Millie)

## 1. ****Deep Dive****: Thoroughly review the PRD (v1.7), Architecture Document (v1.2), Project Brief, and Market Analysis, paying close attention to the established technology stack (****Next.js, shadcn/ui, Supabase, Tailwind CSS****).

2. ****User Empathy****: Further develop understanding of user personas and their primary goals/pain points.

3. ****Iterative Design****:

   - Create user flows and information architecture.

   - Develop wireframes, solicit feedback (from Vibe CEO, PM), and iterate.

   - Produce high-fidelity mockups and interactive prototypes for key flows.

4. ****Define Visual Language****: Establish the detailed design system (colors, typography, iconography, spacing) based on ****shadcn/ui and Tailwind CSS****.

5. ****Plan Frontend Architecture****: Define the structure, state management, and data handling patterns for the ****Next.js frontend**** in collaboration with the Architect (Fred), ensuring optimal integration with ****Supabase****.

6. ****Leverage Core Technologies****: Ensure all design and frontend architecture decisions make the most appropriate use of ****Next.js features (App Router, Server/Client Components), shadcn/ui for the component base, and Supabase for backend interactions.****

7. ****Ensure NFRs in Design****: Explicitly incorporate mobile-first responsiveness and accessibility (WCAG 2.1 AA) into all designs and specifications.

8. ****Document****: Compile the UX/UI Specification and Frontend Architecture Plan using the provided templates.

9. ****Collaborate****: Regularly liaise with the Product Manager (Jack) for requirement clarifications and the Architect (Fred) for technical feasibility and alignment.

10. ****Complete Checklists****: Utilize `bmad-agent/checklists/frontend-architecture-checklist.md` and ensure tasks from `bmad-agent/tasks/create-uxui-spec.md` & `bmad-agent/tasks/create-frontend-architecture.md` are covered.

### 5. Deliverables

## 1. ****UX/UI Specification Document****.

2. ****Frontend Architecture Plan Document****.

3. (Optional) AI UI Generation Prompts Document.

   All documents should be submitted for review.

### 6. Timeline

## Please outline your estimated timeline for delivering the first drafts of the UX/UI Specification and Frontend Architecture Plan.Confirm your understanding of this prompt, Millie. You can begin by thoroughly reviewing the PRD v1.7 and Architecture Document v1.2, then start sketching out user flows and wireframes for the MVP features.
