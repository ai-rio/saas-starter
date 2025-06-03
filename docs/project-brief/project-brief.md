## Project Brief: Creator's Deal Hub (CDH) - Next.js Web Application

**Date:** June 2, 2025

**Version:** 1.0

**Prepared by:** BMAD Analyst Agent


### 1. Project Title

Creator's Deal Hub (CDH) - Next.js Web Platform


### 2. Project Goal & Vision

- **Goal**: To develop a mobile-first, Next.js-based web application for the Creator's Deal Hub that reaches a new and wider audience, overcomes the technical constraints of the existing Expo mobile app, and serves as the primary platform for future development and feature enrichment.

- **Vision**: To evolve CDH into a more dynamic, marketplace-like platform that empowers a larger segment of the creator economy by simplifying deal management and potentially expanding into areas like micro-sponsorships. The Next.js web app will be the central focus, with the existing Expo app serving as a reference for its development.


### 3. Target Audience

- **Primary**: All creators, with a particular focus on nano to mid-tier influencers and content creators who are looking to monetize their work and manage brand partnerships more effectively.

- **Expansion**: The web platform aims to capture a "bigger target audience (Opportunity 2)" as identified in the market analysis, suggesting a focus on creators who may not have been reached by the mobile-only application or who prefer web-based tools for business management \[cite: Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis]. This includes creators seeking a marketplace-like environment for discovering and managing deals.


### 4. Problems to Solve / Opportunities

- **Reach & Accessibility**: The current mobile-only Expo app limits audience reach. A web platform will make CDH accessible to a broader range of creators across different devices.

- **Technical Limitations**: Overcome existing technical constraints associated with the Expo framework, allowing for richer feature possibilities and a more polished user experience.

- **Marketplace Potential (Opportunity 2)**: Address the pain point for creators (especially mid-tier) in finding and managing brand deals, particularly smaller "micro-sponsorships." The current process for many is manual and time-consuming \[cite: Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis].

- **Evolving Feature Set**: Provide a foundation for a more sophisticated application that can evolve with the needs of the creator economy.


### 5. Proposed Solution (High-Level)

Develop a new, mobile-first web application using Next.js. This platform will initially replicate the core functionalities of the existing Expo mobile app (deal management, user accounts, invoicing, settings) but will be architected to support future growth into a marketplace-like environment. The platform will prioritize performance and user experience, leveraging Next.js capabilities like SSR and SSG where appropriate. PWA functionality will be a key consideration for a potential future evolution into a polished mobile app experience derived from the web codebase.


### 6. Core Features (MVP for Web App)

- **User Authentication**: Sign-up, sign-in, sign-out (migrating or replicating existing Supabase authentication \[cite: mobile/docs/application-overview\.md]).

- **Deal Management**: Core features from the existing mobile app for tracking and managing brand deals.

- **Invoicing**: Core features from the existing mobile app for generating and managing invoices.

- **Settings**: Core user and application settings from the existing mobile app.

- **(Future Consideration for Marketplace Evolution - Post MVP)**:

  - Creator profiles for showcasing niches and audience demographics.

  - Brand/deal discovery features.

  - Basic communication and negotiation tools within the platform.

  - Standardized contract templates.

  - Automated payment processing integration.


### 7. Success Metrics

- **User Acquisition**: Number of new registered users on the web platform.

- **Traffic**: Overall website traffic, page views, and user session duration.

- **(Future for Marketplace)**: Number of deals initiated/managed through the platform.


### 8. Monetization Strategy (Initial Thoughts)

- **Free Tier**: Offer basic access to core deal management functionalities to attract a wide user base.

- **Pro Tier**: Introduce a subscription-based Pro tier for advanced features, higher usage limits, or premium marketplace functionalities.

- **BMAD Suggestions (To be explored by PM/Analyst)**:

  - **Commission on Deals (for Marketplace)**: A percentage-based commission on successful sponsorships facilitated through the platform (as suggested for "Opportunity 2: Automated Micro-Sponsorship Marketplace" which estimates a $15/mo value or commission basis \[cite: Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis]).

  - **Featured Listings**: For brands or creators in the marketplace.

  - **Premium Analytics/Insights**: Offer deeper analytics as a Pro feature.


### 9. Technical Considerations (High-Level)

- **Framework**: Next.js.

- **Rendering Strategy**: Utilize the best performant approach – SSR for dynamic content needing SEO, SSG for static content, and CSR where appropriate.

- **Styling**: Tailwind CSS (as it's already familiar from the NativeWind setup \[cite: mobile/docs/components-and-styling.md]).

- **Backend**: Continue leveraging Supabase for database and authentication needs, adapting client-side integrations for Next.js.

- **PWA Capabilities**: Design with PWA principles in mind from the outset to facilitate a potential future evolution into a polished mobile app experience directly from the web codebase. This is particularly important as the goal is for the Next.js app to be the main focus, replacing further Expo development.


### 10. Relationship to Existing Mobile App

- The Next.js web application will become the **main focus** for CDH.

- The existing Expo mobile application **will not be further developed**.

- The Expo app will serve **only as a reference** for features, business logic, and user flows during the development of the Next.js web app. There will be no coexistence in the long term.


### 11. Next Steps

- This Project Brief will be handed over to the **Product Manager (PM)** to develop a detailed Product Requirements Document (PRD).

- The **Design Architect** and **Architect (Fred)** will use this brief and the subsequent PRD to define the UX/UI and technical architecture for the Next.js web application.
