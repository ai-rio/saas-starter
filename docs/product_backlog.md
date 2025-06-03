# Product Backlog: Creator's Deal Hub (CDH) - Next.js Web Platform

## Version: 2.0 (Incorporating Critique Feedback)PRD Reference: Version 1.7 (creator-deal-hub-prd.md)

## Prioritization Approach

## Items in this backlog are prioritized based on their contribution to the Minimum Viable Product (MVP) as defined in the PRD, business value, urgency, and dependencies. The primary goal for initial sprints is to deliver core functionality for Authentication, Deal Management, Invoicing, and Settings. Priorities are categorized as:* ****High (MVP Core):**** Essential for the MVP launch. These items represent the core user flows and functionality.

* ****Medium (MVP Supporting):**** Important for the MVP but can be addressed after core features are stable. Often includes enhancements or secondary features.

* ****Low (Post-MVP):**** Desirable features that are out of scope for the initial MVP but may be considered for future iterations.Priorities will be reviewed and adjusted at the beginning of each sprint planning session in collaboration with the development team and stakeholders.****Note on Non-Functional Requirements (NFRs):**** All user stories must also consider and incorporate relevant Non-Functional Requirements as outlined in Section 3 of the PRD (Performance, Security, Accessibility, etc.). Specific NFR-related tasks or acceptance criteria may be added during backlog refinement.

## Epics

## 1. ****Epic 1: Authentication System****

   - ****Description:**** Enable users to securely register, log in, and manage their accounts.

   - ****PRD Reference:**** Section 2.1, Section 7.1

   - ****Priority:**** High (MVP Core)

2. ****Epic 2: Deal Management System****

   - ****Description:**** Allow users to create, track, and manage deals with brands or creators, including managing deliverables and reminders.

   - ****PRD Reference:**** Section 2.2, Section 7.2

   - ****Priority:**** High (MVP Core)

3. ****Epic 3: Invoicing System****

   - ****Description:**** Facilitate the creation, management, and tracking of invoices for completed deals, including automated reminders.

   - ****PRD Reference:**** Section 2.3, Section 7.3

   - ****Priority:**** High (MVP Core)

4. ****Epic 4: User Settings and Profile Management****

   - ****Description:**** Provide users with options to manage their profile, notification preferences, data export, and other account settings.

   - ****PRD Reference:**** Section 2.4, Section 7.4

   - ****Priority:**** High (MVP Core)

5. ****Epic 5: Mobile-First Responsive Design****

   - ****Description:**** Ensure the application is fully responsive and provides an optimal experience on mobile devices. This applies across all features.

   - ****PRD Reference:**** Section 3.2, Section 4.3, Section 7.5

   - ****Priority:**** High (MVP Core)

## User Stories

### To Do

#### Epic: Authentication System

## - ****US-AUTH-001:**** As a new user (Emma, Marcus), I want to be able to register for an account using my email and password so that I can access the platform.

  - ****Acceptance Criteria:****

    - Registration form includes fields for email, password, and password confirmation.

    - Password strength requirements are enforced (e.g., minimum length, character types - __Specific requirements to be defined__).

    - Successful registration creates a new user account in the system.

    - Appropriate error messages are displayed for invalid input or existing email.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** None

- ****US-AUTH-002:**** As a registered user (Emma, Marcus), I want to be able to log in to my account using my email and password so that I can access my deals and settings.

  - ****Acceptance Criteria:****

    - Login form includes fields for email and password.

    - Successful login redirects the user to their dashboard.

    - Appropriate error messages are displayed for incorrect credentials or non-existent accounts.

    - "Forgot Password" link is present (links to US-AUTH-005).

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-001

- ****US-AUTH-003:**** As a logged-in user (Emma, Marcus), I want to be able to log out of my account so that my session is securely terminated.

  - ****Acceptance Criteria:****

    - Logout option is clearly visible and accessible (e.g., in account menu).

    - Clicking logout terminates the user's session.

    - User is redirected to the login page or homepage after logout.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-002

- ****US-AUTH-004 (New):**** As a new user who registered with email (Emma, Marcus), I want to receive a verification email and click a link to activate my account, so that my email address is confirmed and my account is secured.

  - ****Acceptance Criteria:****

    - Upon successful email/password registration, a verification email is sent to the user's provided email address.

    - The email contains a unique, time-limited verification link.

    - Clicking the link activates the user's account.

    - User is informed of successful verification.

    - Users attempting to log in with an unverified email are prompted to check their email for verification.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-001

- ****US-AUTH-005 (New):**** As a registered user (Emma, Marcus) who has forgotten my password, I want to be able to request a password reset link via email, so that I can set a new password and regain access to my account.

  - ****Acceptance Criteria:****

    - "Forgot Password" link on the login page leads to a form where the user can enter their registered email.

    - If the email exists, a password reset email with a unique, time-limited link is sent.

    - Clicking the link allows the user to enter and confirm a new password.

    - New password must meet strength requirements.

    - User is notified of successful password change and can then log in with the new password.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-001

- ****US-AUTH-006 (New):**** As a new or returning user (Emma, Marcus), I want to be able to register or log in using my Google account, so that I can access the platform quickly and without creating separate credentials for CDH.

  - ****Acceptance Criteria:****

    - "Sign in/up with Google" button is available on login and registration pages.

    - User is redirected to Google's authentication flow.

    - Upon successful Google authentication, a new CDH account is created (if one doesn't exist for that Google email) or the user is logged into their existing CDH account.

    - User profile information (name, email, profile picture if available) is pre-filled from Google where appropriate.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** None (can be parallel to email/password auth)

#### Epic: Deal Management System

## - ****US-DEAL-001:**** As a user (Emma, Marcus), I want to be able to create a new deal, specifying details like brand/creator name, deal terms, and compensation, so that I can track my collaborations.

  - ****Acceptance Criteria:****

    - Form allows input for deal name, counterparty (brand/creator), key dates (start, end), deal description/scope, deliverables (as text initially), and compensation details (e.g., flat fee, rev share %, value). (__Specific required fields for MVP to be confirmed: e.g., Deal Name, Counterparty, Value, Status__).

    - Created deal is saved to the database and associated with the user.

    - User is redirected to a deal overview page or back to the deals list upon successful creation.

    - Validation is in place for required fields.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-002

- ****US-DEAL-002:**** As a user (Emma, Marcus), I want to be able to view a list of all my deals with key information like status, counterparty, and upcoming deadlines, so that I can get an overview of my ongoing and past collaborations.

  - ****Acceptance Criteria:****

    - Deals list displays deal name, counterparty, status (e.g., Negotiation, Active, Completed, Cancelled), value, and key dates (e.g., end date or next deliverable due date).

    - Users can sort deals (e.g., by creation date, end date, value).

    - Users can filter deals (MVP: by status; Future: by date range, counterparty).

    - Each deal in the list links to its detailed view (US-DEAL-003).

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-001

- ****US-DEAL-003:**** As a user (Emma, Marcus), I want to be able to view the detailed information of a specific deal, so that I can review all its terms and current status.

  - ****Acceptance Criteria:****

    - Deal detail page displays all information entered during deal creation (US-DEAL-001).

    - Displays current status of the deal.

    - Allows for editing the deal (US-DEAL-004).

    - Displays associated deliverables and invoices (once those features are built).

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-001

- ****US-DEAL-004:**** As a user (Emma, Marcus), I want to be able to edit the details of an existing deal (e.g., update terms, change status), so that I can keep my deal information accurate.

  - ****Acceptance Criteria:****

    - User can modify fields of a deal.

    - Changes are saved to the database.

    - (Audit trail of changes is considered out of scope for MVP, but noted for future).

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-003

- ****US-DEAL-005:**** As a user (Emma, Marcus), I want to be able to delete a deal (or mark as cancelled if it has financial implications), so that I can remove irrelevant or erroneous entries.

  - ****Acceptance Criteria:****

    - User can mark deals as 'Cancelled'. A true delete might be reserved for deals in a draft state with no associated financial records.

    - Confirmation prompt is shown before cancellation.

    - Cancelled deals are visually distinct or filterable in the deals list.

  - ****Priority:**** Medium (MVP Supporting)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-002

- ****US-DEAL-006 (New):**** As a creator (Emma, Marcus), I want to set reminders for important dates related to a deal (e.g., overall deal deadline, deliverable due dates), so I receive in-app and email notifications and don't miss them.

  - ****Acceptance Criteria:****

    - Within a deal's details, user can add one or more reminders with a date, time, and optional note.

    - User receives an in-app notification at the specified time.

    - User receives an email notification at the specified time.

    - Reminders are visible within the deal details.

    - User can edit or delete existing reminders.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-003

- ****US-DEAL-007 (New):**** As a creator (Emma, Marcus), I want to be able to list specific deliverables for a deal, each with its own due date and status (e.g., pending, completed), so I can track my work items.

  - ****Acceptance Criteria:****

    - Within a deal's details, user can add multiple deliverables (e.g., "Instagram Post", "YouTube Video Mention").

    - Each deliverable has a description, due date, and status (Pending, In Progress, Completed).

    - User can update the status of each deliverable.

    - Deliverables are visible within the deal details.

    - (Reminders for individual deliverables covered by US-DEAL-006, by allowing reminders to be linked to deliverable due dates).

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-003

#### Epic: Invoicing System

## - ****US-INV-001:**** As a user (Emma, Marcus), I want to be able to generate an invoice for a deal (or specific milestones/deliverables), so that I can request payment.

  - ****Acceptance Criteria:****

    - Invoice generation can be triggered from a deal.

    - Invoice automatically populates with deal information (counterparty, services based on deal description/deliverables, amount due based on deal value).

    - User can add custom notes to the invoice before finalizing. (Line items MVP if simple, otherwise notes only).

    - Generated invoice is assigned a unique, sequential invoice number.

    - Invoice is saved and viewable within the system.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-003

- ****US-INV-002:**** As a user (Emma, Marcus), I want to be able to view a list of all my invoices with their status (e.g., Draft, Sent, Paid, Overdue), so that I can track my income.

  - ****Acceptance Criteria:****

    - Invoices list displays invoice number, client name (from deal), amount, issue date, due date, and status.

    - Users can sort invoices (e.g., by issue date, due date, status).

    - Users can filter invoices (MVP: by status).

    - Each invoice in the list links to its detailed view.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-INV-001

- ****US-INV-003:**** As a user (Emma, Marcus), I want to be able to mark an invoice as 'Sent', 'Paid', or 'Overdue' (system might mark overdue automatically), so that I can keep track of its lifecycle.

  - ****Acceptance Criteria:****

    - User can manually update the status of an invoice (e.g., Draft to Sent, Sent to Paid).

    - System automatically updates status to 'Overdue' if payment due date passes and status is not 'Paid'.

    - Status changes are reflected in the invoice list and detail view.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-INV-001

- ****US-INV-004:**** As a user (Emma, Marcus), I want to be able to download an invoice as a PDF, so that I can send it to my client or keep it for my records.

  - ****Acceptance Criteria:****

    - A 'Download PDF' option is available for each invoice (likely for 'Sent' or 'Paid' invoices).

    - The downloaded PDF is well-formatted and contains all relevant invoice details, including user's business information if provided in settings.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-INV-001, US-SET-004 (for default invoice info)

- ****US-INV-005 (New):**** As a creator (Emma, Marcus), I want to be able to customize basic elements of my invoice template (e.g., upload a logo, add business address and payment details), so my invoices look professional and contain necessary information for payment.

  - ****Acceptance Criteria:****

    - User can upload a logo in settings (US-SET-004) that appears on invoices.

    - User can input business name, address, and payment details (e.g., bank info, PayPal email) in settings (US-SET-004) that appear on invoices.

    - Generated PDF invoices reflect these customizations.

  - ****Priority:**** Medium (MVP Supporting)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-INV-004, US-SET-004

- ****US-INV-006 (New):**** As a creator (Emma, Marcus), I want the system to automatically send payment reminders via email to clients for overdue invoices, so I can improve my cash flow and reduce manual follow-up.

  - ****Acceptance Criteria:****

    - System identifies invoices that are past their due date and not marked as 'Paid'.

    - Automated email reminders are sent to the client contact associated with the deal/invoice (client contact info needs to be captured).

    - Frequency of reminders is configurable (e.g., 3 days after due, 7 days after due - MVP might have a fixed schedule).

    - User is notified when automated reminders are sent.

  - ****Priority:**** Medium (MVP Supporting)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-INV-003, Email sending capability

#### Epic: User Settings and Profile Management

## - ****US-SET-001:**** As a logged-in user (Emma, Marcus), I want to be able to view and update my basic profile information (e.g., name, contact email, profile picture), so that my account details are current.

  - ****Acceptance Criteria:****

    - Profile page displays current user information.

    - User can edit fields like name, display name, and contact email.

    - User can upload or change their profile picture.

    - Changes are saved to the database.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-002

- ****US-SET-002:**** As a logged-in user (Emma, Marcus), I want to be able to change my password, so that I can maintain account security.

  - ****Acceptance Criteria:****

    - Password change form requires current password and new password (with confirmation).

    - New password must meet strength requirements.

    - Password is securely updated in the database.

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-AUTH-002

- ****US-SET-003:**** As a logged-in user (Emma, Marcus), I want to manage my notification preferences (e.g., email notifications for deal updates, invoice reminders), so that I can control how I am contacted by the platform.

  - ****Acceptance Criteria:****

    - Settings page provides options to toggle different types of email and in-app notifications (e.g., deal reminders, invoice payment reminders).

    - User's preferences are saved and respected by the notification system.

  - ****Priority:**** Medium (MVP Supporting)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-006, US-INV-006

- ****US-SET-004:**** As a logged-in user (Emma, Marcus), I want to be able to set default values for my invoices (e.g., payment terms, company address, logo, payment details), so that I don't have to enter them every time.

  - ****Acceptance Criteria:****

    - Settings page allows users to define default payment terms (e.g., Net 30), their business name, address, logo, and preferred payment methods/details.

    - These defaults are automatically applied when creating a new invoice but can be overridden.

  - ****Priority:**** Medium (MVP Supporting)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-INV-001

- ****US-SET-005 (New):**** As a creator (Emma, Marcus), I want to be able to export my core data (deals, invoices) in CSV format, so that I can have a backup or use it for external analysis or accounting.

  - ****Acceptance Criteria:****

    - An option to export data is available in the settings or relevant sections.

    - User can choose to export deals and/or invoices.

    - Data is exported into a well-structured CSV file.

    - Export includes key fields for deals (e.g., name, counterparty, value, status, dates) and invoices (e.g., number, client, amount, issue date, due date, status).

  - ****Priority:**** Medium (MVP Supporting)

  - ****Estimate:**** TBD

  - ****Dependencies:**** US-DEAL-002, US-INV-002

#### Epic: Mobile-First Responsive Design

## - ****US-RESP-001:**** As a user (Emma, Marcus), I want the application to be fully usable and visually appealing on my mobile phone (iOS and Android), so that I can manage my deals and invoices on the go.

  - ****Acceptance Criteria:****

    - All MVP features (Authentication, Deal Management, Invoicing, Settings) are accessible and functional on common mobile screen sizes (e.g., 360px width and up).

    - Layouts adapt to screen size, ensuring readability and ease of interaction (e.g., tappable targets are appropriately sized).

    - Navigation is mobile-friendly (e.g., hamburger menu, bottom navigation if appropriate).

    - No horizontal scrolling is required on mobile devices for primary content.

    - (__Note: This is a cross-cutting concern. Specific responsive behaviors for key views/components to be detailed during backlog refinement and design.__)

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD (Effort distributed across other stories, but specific testing/refinement needed)

  - ****Dependencies:**** Applies to all UI-related stories.

- ****US-RESP-002:**** As a user (Emma, Marcus), I want the application to provide a consistent and optimized experience on my tablet device, so that I can use it effectively on various screen sizes.

  - ****Acceptance Criteria:****

    - Application adapts to tablet screen sizes (portrait and landscape).

    - UI elements are appropriately scaled and spaced for tablet interaction.

    - Functionality remains consistent with desktop and mobile versions.

    - (__Note: Specific responsive behaviors for key views/components on tablets to be detailed during backlog refinement and design.__)

  - ****Priority:**** High (MVP Core)

  - ****Estimate:**** TBD (Effort distributed across other stories, but specific testing/refinement needed)

  - ****Dependencies:**** Applies to all UI-related stories.

### In Progress

## __(No stories in progress yet)__

### Done

## __(No stories done yet)__

## Sprint Backlog

## _(Initially empty. To be populated at the start of each sprint.)_
