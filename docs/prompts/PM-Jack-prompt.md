## Prompt for Product Manager (PM): Creator's Deal Hub (CDH) Next.js Web Application PRD Development

## To: Product Manager (PM) Agent (Jack)From: BMAD OrchestratorDate: June 2, 2025Subject: Initiation of Product Requirements Document (PRD) for Creator's Deal Hub (CDH) - Next.js Web Platform

### 1. Objective

## Your primary objective is to take the approved ****Project Brief: Creator's Deal Hub (CDH) - Next.js Web Application**** (referenced at `web/docs/project-brief/project-brief.md`) and develop a comprehensive ****Product Requirements Document (PRD)**** for this new web platform.This PRD will be the foundational document for the Design Architect, Architect, and subsequently the development team. It must clearly define the product's purpose, features, user stories, and success criteria, aligning with the strategic shift from the Expo mobile app to a Next.js mobile-first web application.

### 2. Key Inputs & References

## - ****Primary Input****:

  - `web/docs/project-brief/project-brief.md`: "Project Brief: CDH Next.js Web Application" – This document outlines the project goals, vision, target audience, problems to solve, proposed solution, core MVP features, success metrics, initial monetization strategy, high-level technical considerations, and the relationship with the existing mobile app.

- ****Supporting Contextual Documents (from existing mobile project and market analysis)****:

  - `mobile/docs/application-overview.md`: For understanding existing authentication and basic app flow.

  - `mobile/docs/components-and-styling.md`: For context on existing UI/UX philosophy (though this will be adapted for web).

  - `mobile/app/(protected)/(tabs)/index.tsx` and `mobile/app/(protected)/(tabs)/settings.tsx`: For reference to current deal management and settings features.

  - `web/docs/research/Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis.md`: Particularly "Opportunity 2: Automated Micro-Sponsorship Marketplace" and general insights into creator pain points and SLC framework.

  - `bmad-agent/templates/prd-tmpl.md`: Use this as the structural template for the PRD.

  - `bmad-agent/data/bmad-kb.md`: For general BMAD principles and guidance.

  - `bmad-agent/checklists/pm-checklist.md`: As a guide for your process.

### 3. Scope of the PRD

## The PRD must cover the following for the ****Next.js mobile-first web application****:* ****Introduction & Goals****:

  - Reiterate the project vision and goals from the Project Brief.

  - Clearly state the target audience for the web platform.

* ****User Personas (if applicable)****:

  - Based on the target audience (nano to mid-tier creators, potential for a bigger audience via a marketplace model), define key user personas.

* ****Proposed Solution****:

  - Elaborate on the Next.js web application, its mobile-first nature, and its role as the primary CDH platform.

* ****Features & Functionality (MVP Focus)****:

  - ****Detailed breakdown of MVP features**** listed in the Project Brief (Section 6):

    - User Authentication (Sign-up, Sign-in, Sign-out - leveraging Supabase).

    - Deal Management (translating core mobile features to web).

    - Invoicing (translating core mobile features to web).

    - Settings (translating core mobile features to web).

  - For each feature, define:

    - ****User Stories****: Clear, concise user stories from the perspective of the target audience.

    - ****Acceptance Criteria****: Measurable criteria for each user story.

    - ****Functional Requirements****: What the system should do.

    - ****Non-Functional Requirements (High-Level)****: Performance (as emphasized in the brief), usability on mobile web, security considerations for Supabase integration.

* ****Marketplace Evolution (Post-MVP Vision)****:

  - While the MVP focuses on core feature parity, the PRD should include a section outlining the ****vision and high-level requirements for the future marketplace evolution**** (as per Project Brief Section 6, "Future Consideration"). This will inform architectural decisions.

  - Consider how "Opportunity 2: Automated Micro-Sponsorship Marketplace" from the market analysis can be phased in.

* ****Monetization Strategy Integration****:

  - Detail how the Free Tier and Pro Tier (Project Brief Section 8) will manifest in terms of feature access.

  - Explore and propose initial thoughts on how BMAD suggestions for monetization (commission on deals, featured listings, premium analytics) could be integrated into the product roadmap and feature set.

* ****Success Metrics****:

  - Reiterate and, if necessary, expand on the success metrics from the Project Brief (Section 7 – User Acquisition, Traffic).

  - Define how these will be tracked.

* ****Technical Considerations (from a Product Perspective)****:

  - Acknowledge the Next.js framework, performant rendering strategies, Tailwind CSS, and Supabase backend as defined in the Project Brief (Section 9).

  - Emphasize the importance of PWA capabilities for future mobile app evolution.

* ****Out of Scope for MVP****:

  - Clearly list features or functionalities that are __not__ part of the initial MVP web release.

### 4. Key Tasks for the PM

## 1. ****Thoroughly Review**** all input documents, especially the Project Brief at `web/docs/project-brief/project-brief.md` and the "Microservice Opportunities" analysis at `web/docs/research/Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis.md`.

2. ****Collaborate/Clarify****: If any aspects of the Project Brief are unclear or require further Vibe CEO input, initiate that discussion.****Ideate & Detail****: Expand on the core MVP features, breaking them down into actionable user stories and requirements.1. ****Marketplace Vision****: Flesh out the initial thoughts on the marketplace evolution, considering how it aligns with "Opportunity 2" and the SLC framework (Simple, Lovable, Complete) from the market analysis.

2. ****Monetization Integration****: Think through how the proposed monetization tiers and suggestions will impact the feature set and user experience.

3. ****Draft the PRD****: Utilize the `bmad-agent/templates/prd-tmpl.md` template.

4. ****Iterate****: Be prepared for iterative refinement based on feedback from the Vibe CEO and other BMAD agents (Architect, Design Architect).

### 5. Deliverable

## A comprehensive ****Product Requirements Document (PRD)**** for the Creator's Deal Hub - Next.js Web Platform.

### 6. Timeline

## To be determined in collaboration with the Vibe CEO and other stakeholders, but this is the immediate next step in the planning process.Please confirm your understanding and begin drafting the PRD. Let the BMAD Orchestrator or Vibe CEO know if you have any initial questions.
