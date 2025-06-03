# Product Requirements Document (PRD): Creator's Deal Hub (CDH) - Next.js Web Platform

## ****Date:**** June 5, 2025****Version:**** 1.7 (Incorporating Vibe CEO Feedback on SLC, Data Model & Deliverable Reminders)****Prepared by:**** Jack (Product Manager)

## 1. Goal, Objective and Context

### 1.1 Project Vision & Goals

## The Creator's Deal Hub (CDH) Next.js web application aims to transform the existing mobile-only platform into a comprehensive, mobile-first web application that serves as the primary platform for future development and feature enrichment. This strategic shift addresses several key objectives:* ****Expand Market Reach****: Overcome the limitations of the mobile-only approach to reach a wider audience of creators across all devices.

* ****Technical Evolution****: Leverage Next.js capabilities to overcome the technical constraints of the Expo framework, enabling richer features and a more polished user experience.

* ****Marketplace Foundation****: Establish the groundwork for evolving CDH into a dynamic marketplace-like platform that connects creators with brands for sponsorship opportunities.

* ****Future-Proof Architecture****: Create a foundation that supports progressive enhancement of features and can evolve with the needs of the creator economy.****Mission Statement****:> To empower creators of all levels by providing an accessible, professional, and efficient web-based platform for managing brand partnerships and fostering new monetization opportunities, ultimately simplifying the business side of content creation.

### 1.2 Target Audience

## The CDH Next.js web application targets:* ****Primary****: Nano to mid-tier influencers and content creators (1,000-100,000 followers) who are actively monetizing their content through brand partnerships and sponsorships.

* ****Secondary****: Emerging creators who are beginning to explore monetization opportunities and need tools to professionalize their business operations.

* ****Tertiary****: Brands and businesses looking to connect with relevant creators for promotional partnerships (future marketplace evolution).

### 1.3 User Personas

#### 1.3.1 Emma - The Emerging Creator

## - ****Demographics****: 24 years old, fashion and lifestyle content creator with 8,000 followers across Instagram and TikTok

- ****Goals****: Establish consistent income from brand deals, appear professional to potential partners, keep track of all agreements and payments

- ****Pain Points****: Manually tracks deals in spreadsheets, struggles with invoicing, often forgets follow-ups, feels overwhelmed by business aspects

- ****Behaviors****: Creates content primarily on mobile, checks analytics daily, responds to brand inquiries within 24 hours

- ****Needs from CDH****: Simple deal tracking, professional invoicing, reminders for deliverables and payments

#### 1.3.2 Marcus - The Mid-Tier Creator

## - ****Demographics****: 32 years old, tech reviewer with 75,000 subscribers on YouTube and 45,000 followers on Twitter

- ****Goals****: Scale his business operations, increase deal flow, maintain professional relationships with multiple brands simultaneously

- ****Pain Points****: Struggles to manage multiple ongoing partnerships, needs better organization for deliverables across different campaigns, wants to analyze which deal types perform best

- ****Behaviors****: Works across devices (mobile for communication, desktop for content editing and business management), delegates some tasks to a virtual assistant

- ****Needs from CDH****: Comprehensive deal management, team collaboration features, analytics on deal performance, integration with existing tools

#### 1.3.3 Sarah - The Brand Manager (Future Marketplace)

## - ****Demographics****: 29 years old, marketing manager at a D2C skincare brand

- ****Goals****: Find relevant creators who align with brand values, manage multiple creator partnerships efficiently, track ROI on creator campaigns

- ****Pain Points****: Spends hours searching for appropriate creators, struggles with consistent contract terms, manually tracks deliverables from multiple creators

- ****Behaviors****: Works primarily on desktop, needs to report campaign metrics to leadership, manages a quarterly creator budget

- ****Needs from CDH****: Creator discovery tools, standardized contract templates, centralized communication and deliverable tracking

### 1.4 Problem Statement

## Creators, particularly at the nano to mid-tier level, face significant operational challenges in managing their brand partnerships:1) ****Deal Management Complexity****: As creators scale, they struggle to track multiple deals across different stages (negotiation, active, completed) using makeshift solutions like spreadsheets or notes apps.

2) ****Professional Business Operations****: Many creators lack the tools to appear professional to brands, particularly in areas like invoicing, contract management, and organized communication.

3) ****Platform Limitations****: The current mobile-only approach limits accessibility and functionality, preventing creators from effectively managing their business across devices.

4) ****Marketplace Inefficiency****: Finding relevant brand partnerships is often a manual, time-consuming process for creators, with 3-10 hours spent per deal on outreach, negotiation, and administration.

5) ****Technical Constraints****: The existing Expo framework imposes limitations on feature development and user experience that hinder the platform's ability to evolve with creator needs.

## 2. Functional Requirements (MVP)

## The following features are all considered essential core components for the Minimum Viable Product (MVP) of the Next.js web application.

### 2.1 User Authentication

#### User Stories

## - As a new user, I want to create an account so that I can start managing my creator business.

- As a returning user, I want to securely sign in to access my deals and account information.

- As a user, I want to sign out of my account to protect my information when using shared devices.

- As a user, I want to reset my password if I forget it so I can regain access to my account.

#### Acceptance Criteria

## - Users can create a new account using email/password.

- Users can create a new account using ****Google**** social authentication (MVP).

- Email verification is required before account activation for email/password sign-ups.

- Users can sign in with their credentials or Google social authentication.

- Users can request a password reset via email.

- Users can sign out from any page via the account menu.

- Authentication state persists across browser sessions until explicitly signed out.

#### Functional Requirements

## - Implement Supabase authentication for email/password sign-up and sign-in.

- Support social authentication with ****Google (MVP)****. (Future: Apple).

- Implement email verification flow.

- Create password reset functionality.

- Develop secure session management.

- Implement protected routes that require authentication.

### 2.2 Deal Management

#### User Stories

## - As a creator, I want to add new brand deals with all relevant details so I can keep track of my partnerships.

- As a creator, I want to view all my deals in one place so I can understand my current workload and commitments.

- As a creator, I want to filter and sort my deals by status, date, or value so I can focus on what's most important.

- As a creator, I want to update deal statuses as they progress so I can track their lifecycle.

- As a creator, I want to set and receive reminders for key deliverables associated with a deal so I don't miss deadlines.

- As a creator, I want to set reminders for specific deliverables within a deal so I can manage my tasks effectively.

#### Acceptance Criteria

## - Users can create new deals with fields for brand name, deal value, timeline, deliverables, and status.

- Users can view a list of all their deals with key information displayed.

- Users can filter deals by status (negotiation, active, completed, cancelled).

- Users can sort deals by date, value, or brand name.

- Users can edit any deal details and update statuses.

- Users can set reminders for important dates related to a deal (e.g., overall deal deadline) and receive ****in-app and email notifications (MVP)****.

- Users can set reminders for individual deliverables linked to a deal and receive ******in-app and email notifications (MVP)******.

- Users can archive completed or cancelled deals to keep their active list clean.

#### Functional Requirements

## - Create a deal entity with appropriate fields (brand, value, timeline, deliverables, status, notes).

- Develop a deal creation form with validation.

- Implement a deals dashboard with list and optional grid views.

- Create filtering and sorting functionality for deals.

- Implement status update workflow.

- Develop a reminder system with ****in-app and email notification capabilities (MVP)**** that can be associated with deals and individual deliverables.

- Create archiving functionality for completed deals.

### 2.3 Invoicing

#### User Stories

## - As a creator, I want to generate professional invoices for my brand deals so I can get paid promptly.

- As a creator, I want to customize my invoice template with my branding so it represents my business.

- As a creator, I want to track the payment status of my invoices so I know which ones require follow-up.

- As a creator, I want to download my invoices as PDFs so I can share them with brands via email.

- As a creator, I want to view a history of all my invoices so I can reference past transactions.

#### Acceptance Criteria

## - Users can generate invoices directly from deal information.

- Users can customize invoice templates with their logo, colors, and business information.

- Users can mark invoices as sent, paid, or overdue.

- Users can download invoices as PDF files.

- Users can view a history of all invoices with their current status.

- ****System automatically sends payment reminders for overdue invoices based on due dates (MVP).****

#### Functional Requirements

## - Develop an invoice generation system that pulls data from deals.

- Create customizable invoice templates.

- Implement invoice status tracking.

- Develop PDF generation and download functionality.

- Create an invoice history view with search and filter capabilities.

- Implement ****automated payment reminder functionality (MVP)****.

### 2.4 Settings

#### User Stories

## - As a creator, I want to update my profile information so brands can identify me correctly.

- As a creator, I want to customize my notification preferences so I only receive relevant alerts.

- As a creator, I want to manage my account security settings to protect my business information.

- As a creator, I want to set default values for invoices so I don't have to re-enter information each time.

#### Acceptance Criteria

## - Users can update their profile information (name, email, profile picture, business details).

- Users can customize notification settings (email, in-app, frequency).

- Users can change their password and manage connected social accounts.

- Users can set default values for invoices (payment terms, business details, preferred payment methods).

- Users can export their data for backup purposes ****in CSV format (MVP)****.

#### Functional Requirements

## - Develop a user profile management system.

- Create notification preference settings.

- Implement account security management features.

- Develop invoice default settings.

- Create data export functionality ****(CSV for MVP)****.

## 3. Non-Functional Requirements

### 3.1 Performance

## - ****Page Load Time****: Initial page load must be under 2 seconds on average mobile connections.

- ****Time to Interactive****: Users should be able to interact with the page within 3 seconds of initial load.

- ****Responsiveness****: UI interactions should respond within 100ms to feel instantaneous.

- ****API Response Time****: Backend API calls should complete within 500ms for 95% of requests.

- ****Scalability****: The system should be architected with a ****long-term scalability goal**** to handle up to 10,000 concurrent users without degradation in performance.

### 3.2 Mobile-First Design

## - ****Responsive Design****: The application must function flawlessly across all screen sizes, with particular emphasis on mobile devices.

- ****Touch Optimization****: All interactive elements must be appropriately sized and spaced for touch interaction.

- ****Offline Capabilities****: For MVP, users should be able to ****view existing deals and invoices**** when offline. Data synchronization will occur when the connection is restored.

- ****Mobile Network Consideration****: The application should minimize data usage and function well on variable network conditions.

### 3.3 Security

## - ****Authentication****: Implement secure authentication using Supabase with appropriate token management.

- ****Data Protection****: All sensitive user data must be encrypted at rest and in transit.

- ****Input Validation****: All user inputs must be validated and sanitized to prevent injection attacks.

- ****CSRF Protection****: Implement protection against Cross-Site Request Forgery attacks.

- ****Rate Limiting****: Implement rate limiting to prevent brute force attacks.

### 3.4 Accessibility

## - ****WCAG Compliance****: The application must meet WCAG 2.1 AA standards.

- ****Screen Reader Support****: All functionality must be accessible via screen readers.

- ****Keyboard Navigation****: The application must be fully navigable using keyboard only.

- ****Color Contrast****: All text must meet minimum contrast requirements.

### 3.5 Internationalization

## - ****Language Support****: Initially support English, with architecture in place for adding additional languages.

- ****Date and Currency Formatting****: Support localized date and currency formats ****based on the user's browser/OS locale settings (MVP)****.

## 4. User Interaction and Design Goals

### 4.1 User Experience Principles

## - ****Simplicity****: Prioritize clarity and ease of use over feature complexity.

- ****Efficiency****: Minimize the number of steps required to complete common tasks.

- ****Consistency****: Maintain consistent design patterns and interaction models throughout the application.

- ****Feedback****: Provide clear feedback for all user actions.

- ****Progressive Disclosure****: Reveal features and options progressively as users need them.

### 4.2 Key User Flows

#### 4.2.1 Onboarding Flow

## 1. User arrives at landing page

2. User selects "Sign Up"

3. User completes registration form

4. User verifies email

5. User completes profile setup (optional but encouraged)

6. User is introduced to key features via brief tutorial

7. User lands on dashboard

#### 4.2.2 Deal Creation Flow

## 1. User navigates to Deals section

2. User selects "Create New Deal"

3. User completes deal details form

4. User reviews and confirms deal information

5. User is returned to deals dashboard with new deal visible

6. User receives confirmation of deal creation

#### 4.2.3 Invoice Generation Flow

## 1. User navigates to specific deal

2. User selects "Generate Invoice"

3. User reviews pre-populated invoice details

4. User makes any necessary adjustments

5. User previews invoice

6. User finalizes and downloads/sends invoice

### 4.3 Design System

## - ****Component Library****: Utilize a component library inspired by shadcn/ui for consistent UI elements.

- ****Styling****: Implement Tailwind CSS for styling, maintaining consistency with the existing mobile app's NativeWind approach. While conceptual consistency with the mobile app's UI is desired, the web UI will primarily be a fresh build leveraging web-native shadcn/ui patterns and components, rather than a direct port of existing mobile components.

- ****Color Palette****: Define a primary color palette that ensures accessibility while conveying the brand identity.

- ****Typography****: Establish a clear typography hierarchy with appropriate sizing and weights for different content types.

- ****Iconography****: Use a consistent icon set throughout the application.

## 5. Technical Assumptions

### 5.1 Technology Stack

## - ****Frontend Framework****: Next.js

- ****Styling****: Tailwind CSS

- ****Backend/Database****: Supabase (PostgreSQL)

- ****Authentication****: Supabase Auth

- ****Hosting****: Vercel (assumed)

### 5.2 Rendering Strategy

## - ****Server-Side Rendering (SSR)****: For dynamic, authenticated pages that require fresh data on each request.

- ****Static Site Generation (SSG)****: For marketing pages, documentation, and other static content.

- ****Client-Side Rendering (CSR)****: For highly interactive components after initial page load.

- ****Incremental Static Regeneration (ISR)****: For pages with data that changes infrequently.

### 5.3 API Architecture

## - ****RESTful API****: Primary API architecture for data operations.

- ****Real-time Subscriptions****: Utilize Supabase's real-time capabilities for live updates where appropriate.

### 5.4 PWA Capabilities

## - ****Service Workers****: Implement for offline functionality and caching.

- ****Web App Manifest****: Create for installable experience on mobile devices.

- ****Push Notifications****: Implement for important alerts and reminders.

## 6. Testing Requirements

### 6.1 Functional Testing

## - ****Unit Tests****: For individual components and functions.

- ****Integration Tests****: For feature workflows and API interactions.

- ****End-to-End Tests****: For critical user journeys.

### 6.2 Performance Testing

## - ****Load Testing****: Verify system performance under expected load.

- ****Stress Testing****: Identify breaking points under extreme conditions.

- ****Mobile Performance****: Specific testing for performance on various mobile devices and network conditions.

### 6.3 Usability Testing

## - ****User Testing Sessions****: With representatives from target user personas.

- ****A/B Testing****: For key conversion flows and UI elements.

- ****Accessibility Audits****: Regular testing with screen readers and accessibility tools.

## 7. Epic Overview

### Epic 1: Authentication System

## ****Goal****: Implement a secure, user-friendly authentication system using Supabase.****User Stories****:* User registration with email/password

* Social authentication options

* Password reset functionality

* Session management

* Protected routes****Success Criteria****:* 95% success rate for first-time registration attempts

* Average sign-in time under 10 seconds

* ****No known high or critical severity vulnerabilities identified in authentication flow post-security audit/testing.****

### Epic 2: Deal Management System

## ****Goal****: Create a comprehensive system for creators to manage their brand partnerships.****User Stories****:* Deal creation and editing

* Deal dashboard with filtering and sorting

* Deal status management

* Reminder system for deliverables

* Deal archiving****Success Criteria****:* Users can create a new deal in under 2 minutes

* 90% of users can successfully find and update deal statuses

* Reminder system delivers notifications on time with 99.9% reliability

### Epic 3: Invoicing System

## ****Goal****: Develop a professional invoicing system that streamlines payment processes.****User Stories****:* Invoice generation from deal data

* Customizable invoice templates

* Invoice status tracking

* PDF generation and download

* Invoice history and search****Success Criteria****:* Users can generate an invoice in under 1 minute

* PDF generation completes in under 3 seconds

* 95% of users rate the invoice templates as professional

### Epic 4: User Settings and Profile Management

## ****Goal****: Create a comprehensive settings system for user customization and profile management.****User Stories****:* Profile information management

* Notification preferences

* Security settings

* Invoice defaults

* Data export****Success Criteria****:* Users can update all profile information in a single session

* Settings changes apply immediately with visual confirmation

* Data export completes successfully for 99% of requests

### Epic 5: Mobile-First Responsive Design

## ****Goal****: Ensure optimal user experience across all devices with emphasis on mobile.****User Stories****:* Responsive layout for all screens

* Touch-optimized interface

* Offline capabilities

* Performance optimization for mobile networks****Success Criteria****:* Application functions correctly on 99% of tested mobile devices

* Core functionality works offline with successful data synchronization

* Performance metrics meet or exceed requirements on mobile devices

## 8. Key Reference Documents

## - Project Brief: `web/docs/project-brief/project-brief.md`

- Market Analysis: `web/docs/research/Microservice Opportunities in the Creator Economy: An SLC-Driven Market Analysis.md`

- Mobile App Overview: `mobile/docs/application-overview.md`

- Components and Styling: `mobile/docs/components-and-styling.md`

## 9. Out of Scope Ideas Post MVP

### 9.1 Marketplace Evolution

## Future development of these marketplace features should be guided by the SLC (Simple, Lovable, Complete) framework to ensure they effectively meet creator and brand needs.* ****Creator Profiles****: Public profiles showcasing creator niches, audience demographics, and past brand collaborations.

* ****Brand Discovery****: Search and filtering system for creators to find relevant brands seeking partnerships.

* ****In-Platform Communication****: Messaging system for creators and brands to discuss potential collaborations.

* ****Standardized Contracts****: Template library for different types of creator-brand partnerships.

* ****Payment Processing****: Integrated payment system for secure transactions between brands and creators.

### 9.2 Advanced Analytics

## - ****Deal Performance Metrics****: Analytics on which types of deals generate the most revenue.

- ****Growth Tracking****: Visualization of creator business growth over time.

- ****Comparative Analysis****: Benchmarking against industry averages (anonymized data).

- ****ROI Calculation****: Tools for creators to calculate return on investment for different content types.

### 9.3 Team Collaboration

## - ****Multi-User Access****: Ability to add team members with different permission levels.

- ****Task Assignment****: Delegate specific tasks to team members.

- ****Approval Workflows****: Review and approval processes for invoices and contracts.

- ****Activity Logs****: Track who made what changes and when.

### 9.4 Integration Ecosystem

## - ****Calendar Integration****: Sync deadlines and deliverables with Google Calendar, iCal, etc.

- ****CRM Integration****: Connect with popular CRM tools for relationship management.

- ****Accounting Software Integration****: Export financial data to accounting platforms.

- ****Content Platform Analytics****: Pull in performance data from YouTube, Instagram, etc.

## 10. Core Technical Decisions & Application Structure

### 10.1 Application Architecture

## - ****Next.js App Router****: Utilize the latest Next.js app router for improved routing and layouts.

- ****API Routes****: Implement Next.js API routes for server-side operations.

- ****Middleware****: Use middleware for authentication checks and request processing.

- ****State Management****: Implement React Context for global state with local state for component-specific needs.

### 10.2 Data Model

#### Users

## - id (PK)

- email

- name

- profile\_image

- business\_name

- business\_address

- created\_at

- updated\_at

#### Deals

## - id (PK)

- user\_id (FK)

- brand\_name

- description

- value

- start\_date

- end\_date

- status (negotiation, active, completed, cancelled)

- created\_at

- updated\_at

#### Deliverables

## - id (PK)

- deal\_id (FK)

- description

- due\_date

- status (pending, completed)

- created\_at

- updated\_at

#### Invoices

## - id (PK)

- deal\_id (FK)

- invoice\_number

- issue\_date

- due\_date

- amount

- status (draft, sent, paid, overdue)

- created\_at

- updated\_at

#### Reminders

## - id (PK)

- user\_id (FK)

- related\_id (polymorphic - deal\_id, invoice\_id, ******deliverable\_id******)

- related\_type (deal, invoice, or ******deliverable******)

- reminder\_date

- description

- status (pending, sent, dismissed)

- created\_at

- updated\_at

### 10.3 Security Considerations

## - ****Row-Level Security****: Implement Supabase RLS policies to ensure users can only access their own data.

- ****API Authentication****: Secure all API routes with proper authentication checks.

- ****Input Validation****: Implement comprehensive server-side validation for all user inputs.

- ****CORS Configuration****: Properly configure CORS to prevent unauthorized access.

- ****Rate Limiting****: Implement rate limiting to prevent brute force attacks.

### 10.4 Deployment Strategy

## - **CI/CD Pipeline**: Implement automated testing and deployment.

- **Environment Management**: Maintain separate development, staging, and production environments.

- **Monitoring**: Set up error tracking and performance monitoring.

- **Backup Strategy**: Regular database backups with point-in-time recovery capability.
