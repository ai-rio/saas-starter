# UX/UI Specification - Creator's Deal Hub

## Version: 1.0Date: June 2, 2025Author: Millie (Design Architect)

## 1. Introduction

### 1.1 Purpose

## This document outlines the UX/UI specifications for the Creator's Deal Hub (CDH) web application. It serves as a comprehensive guide for the design and implementation of the user interface, ensuring a consistent, intuitive, and engaging user experience that meets the needs of content creators managing their business deals and invoices.

### 1.2 Scope

## This specification covers the user experience design, information architecture, user flows, wireframes, component library, branding, accessibility requirements, and responsive design considerations for the Creator's Deal Hub web application.

### 1.3 Audience

## This document is intended for designers, developers, product managers, and stakeholders involved in the development of the Creator's Deal Hub web application.

### 1.4 Related Documents

## - [Creator's Deal Hub PRD (`web/docs/prd/creator-deal-hub-prd.md`)](https://gemini.google.com/app/web/docs/prd/creator-deal-hub-prd.md "null")

- [Creator's Deal Hub Architecture (`web/docs/architecture/creator-deal-hub-architecture.md`)](https://gemini.google.com/app/web/docs/architecture/creator-deal-hub-architecture.md "null")

- [Project Brief (`web/docs/project-brief/project-brief.md`)](https://gemini.google.com/app/web/docs/project-brief/project-brief.md "null")

## 2. UX Goals & Principles

### 2.1 Core UX Goals

## 1. ****Efficiency****: Streamline deal and invoice management workflows to save creators time.

2. ****Clarity****: Present information in a clear, organized manner to reduce cognitive load.

3. ****Confidence****: Build trust through transparent processes and reliable functionality.

4. ****Accessibility****: Ensure the application is usable by creators of all abilities.

5. ****Mobile-First****: Optimize the experience for mobile devices while ensuring desktop usability.

### 2.2 Design Principles

## 1. ****Simplicity Over Complexity****: Prioritize straightforward solutions and minimize unnecessary steps.

2. ****Progressive Disclosure****: Reveal information and options gradually as needed.

3. ****Consistency****: Maintain consistent patterns, components, and terminology throughout the application.

4. ****Feedback & Guidance****: Provide clear feedback and guidance to help users complete tasks.

5. ****Error Prevention****: Design interfaces that prevent errors before they occur.

### 2.3 User-Centered Approach

## The design process will be guided by the needs, goals, and pain points of our target users as defined in the PRD (Version 1.7, Section 1.3) \[cite: creator-deal-hub-prd.md]:* ****Emma - The Emerging Creator****: Needs simplicity for deal tracking, professional invoicing, and reminders.

* ****Marcus - The Mid-Tier Creator****: Needs comprehensive management, potential team features, and analytics.

* Sarah - The Brand Manager (Future Marketplace): (Considered for future-proofing) Needs creator discovery and campaign management tools.

  All design decisions will be evaluated against how well they serve these users, particularly Emma and Marcus for the MVP.

## 3. Information Architecture (IA)

### 3.1 Site Map

    flowchart TD
    Home["🏠 Home"] --> Auth["🔐 Authentication"]
    Home --> Dashboard["📊 Dashboard - Main authenticated view"]
    
    Auth --> SignIn["Sign In"]
    Auth --> SignUp["Sign Up"]
    Auth --> PasswordReset["Password Reset"]
    
    Dashboard --> Overview["📈 Overview - Summary, quick actions"]
    Dashboard --> Deals["🤝 Deals"]
    Dashboard --> Invoices["📄 Invoices"]
    Dashboard --> Reminders["⏰ Reminders - Future placeholder"]
    Dashboard --> Settings["⚙️ Settings"]
    
    Deals --> DealList["Deal List - View, Filter, Sort"]
    Deals --> DealDetails["Deal Details - [dealId]"]
    Deals --> CreateDeal["Create Deal - /deals/create"]
    Deals --> EditDeal["Edit Deal - /deals/[dealId]/edit"]
    
    Invoices --> InvoiceList["Invoice List - View, Filter, Sort"]
    Invoices --> InvoiceDetails["Invoice Details - [invoiceId]"]
    Invoices --> CreateInvoice["Create Invoice - /invoices/create from Deal"]
    Invoices --> EditInvoice["Edit Invoice - /invoices/[invoiceId]/edit"]
    
    Reminders --> ReminderList["Reminder List"]
    Reminders --> CreateEditReminder["Create/Edit Reminder"]
    
    Settings --> AccountProfile["👤 Account Profile"]
    Settings --> NotificationPrefs["🔔 Notification Preferences"]
    Settings --> InvoiceDefaults["🎨 Invoice Defaults - Branding/Payment"]
    Settings --> DataExport["📤 Data Export"]
    Settings --> TeamManagement["👥 Team Management - Future feature"]

    classDef homeClass fill:#e3f2fd,stroke:#1976d2,stroke-width:3px,color:#000
    classDef authClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#000
    classDef dashboardClass fill:#e8f5e8,stroke:#388e3c,stroke-width:2px,color:#000
    classDef moduleClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#000
    classDef pageClass fill:#fafafa,stroke:#616161,stroke-width:1px,color:#000
    classDef futureClass fill:#ffebee,stroke:#d32f2f,stroke-width:1px,stroke-dasharray: 5 5,color:#000

    class Home homeClass
    class Auth authClass
    class Dashboard,Overview dashboardClass
    class Deals,Invoices,Settings moduleClass
    class Reminders futureClass
    class SignIn,SignUp,PasswordReset,DealList,DealDetails,CreateDeal,EditDeal,InvoiceList,InvoiceDetails,CreateInvoice,EditInvoice,ReminderList,CreateEditReminder,AccountProfile,NotificationPrefs,InvoiceDefaults,DataExport pageClass
    class TeamManagement futureClass
    V****Figure 1: Site Map****
-----------------------------------------------------------------------------------

### 3.2 Navigation Structure

#### Primary Navigation (Authenticated State - e.g., Sidebar on Desktop, Bottom Nav/Hamburger on Mobile)

## - ****Dashboard****: Overview of recent activity, upcoming deadlines, and key metrics.

- ****Deals****: Management of all deals and deliverables.

- ****Invoices****: Creation and management of invoices.

- ****Settings****: User account and application settings.

- ****(User Profile/Logout)****

#### Secondary Navigation (Contextual, within sections)

## - ****Deal Management****: List View, Create Deal button, links to Deal Details.

- ****Invoice Management****: List View, Create Invoice button (contextual, e.g., from a deal), links to Invoice Details.

- ****Settings****: Sub-navigation for Account, Notifications, Invoice Defaults, etc.

### 3.3 Content Organization

#### Dashboard

## - Recent Activity (e.g., new deals, upcoming invoice due dates, recently completed deliverables).

- Upcoming Deadlines (Key deal dates, deliverable due dates, invoice due dates).

- Quick Actions (e.g., "Create New Deal", "Generate Invoice").

- Key Metrics (e.g., Total Active Deals, Pending Invoices Value, Recent Revenue).

#### Deals

## - ****Deal List****:

  - Display crucial info: Brand Name, Deal Value, Status, Key Date (e.g., End Date or Next Deliverable).

  - Filtering options: By Status (Negotiation, Active, Completed, Cancelled), Date Range, Client.

  - Sorting options: By Creation Date, End Date, Value, Brand Name.

  - Clear call-to-action to "Create New Deal".

- ****Deal Details****:

  - Comprehensive view: Client Info, Deal Terms, Deliverables List (with status), Timeline/Key Dates, Status Indicator, Notes, related Invoices.

  - Actions: Edit Deal, Generate Invoice, Add/Edit Deliverables, Set Reminders.

- ****Deal Creation/Editing Form****: Intuitive form fields as per PRD.

#### Invoices

## - ****Invoice List****:

  - Display crucial info: Invoice Number, Client Name, Amount, Issue Date, Due Date, Status (Draft, Sent, Paid, Overdue).

  - Filtering options: By Status, Date Range, Client.

  - Sorting options: By Issue Date, Due Date, Amount, Status.

- ****Invoice Details****:

  - Full invoice view: All header info, line items (or deal summary for MVP), notes, payment status.

  - Actions: Edit Invoice (if draft), Mark as Sent, Record Payment, Download PDF, Send Reminder (manual or view automated).

- ****Invoice Creation/Editing Form****: Pre-fill from Deal where applicable; allow customization.

#### Settings

## - ****Account Information****: Profile details, password change.

- ****Notification Preferences****: Toggles for different event types (deal updates, reminders) and channels (in-app, email).

- ****Invoice Defaults****: Business info, logo upload, default payment terms, payment instructions.

- ****Data Export****: Option to export data (e.g., deals, invoices) in CSV format.

## 4. User Flows

### 4.1 Authentication Flow

    flowchart TD
        A[Landing Page/Public Page] --> B{User has account?}
        B -->|Yes| C[Sign In Page]
        B -->|No| D[Sign Up Page]
        C --> E{Enter Credentials / Use Google}
        E -- Email/Pass --> F[Validate Credentials]
        E -- Google --> G[Google Auth Flow]
        F -->|Valid| H[Dashboard]
        F -->|Invalid| I[Error Message on Sign In Page] --> E
        G -->|Success| H
        G -->|Failure| I
        D --> J[Enter Email/Pass or Use Google]
        J -- Email/Pass --> K[Submit Registration]
        J -- Google --> G
        K --> L{Valid Information & Email Available?}
        L -- Yes --> M[Send Verification Email] --> N[Verification Pending Page / Prompt]
        L -- No --> O[Error Message on Sign Up Page] --> J
        N -- User Clicks Link in Email --> P[Verify Email Token]
        P -->|Valid| H
        P -->|Invalid| Q[Error Message / Resend Option]
        C --> R[Forgot Password?]
        R --> S[Request Password Reset Page]
        S -- Enter Email --> T[Send Reset Link] --> U[Reset Email Sent Page / Prompt]
        U -- User Clicks Link in Email --> V[Password Reset Page]
        V -- Enter New Password --> W{Validate New Password}
        W -- Valid --> X[Password Updated] --> C
        W -- Invalid --> Y[Error Message on Reset Page] --> V****Figure 2: Authentication User Flow****
-------------------------------------------------------------------------------------------------------

### 4.2 Deal Creation Flow

      flowchart TD
    A[Dashboard/Deals List] --> B(Click 'Create New Deal')
    B --> C[Deal Creation Form]
    C --> D{"Enter Deal Details:<br/>• Brand/Client (Select/New)<br/>• Deal Name/Title<br/>• Value & Currency<br/>• Scope/Description<br/>• Dates (Start/End)<br/>• Initial Deliverables<br/>• Status (e.g., Negotiation)"}
    D --> E[Validate Form]
    E -->|Valid| F[Save Deal]
    F --> G[Deal Detail Page for New Deal]
    G --> H[Show Success Toast/Notification]
    E -->|Invalid| I[Show In-form Errors]
    I --> C

    classDef startClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef actionClass fill:#e8f5e8,stroke:#388e3c,stroke-width:2px
    classDef formClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef decisionClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef successClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef errorClass fill:#ffebee,stroke:#d32f2f,stroke-width:2px

    class A startClass
    class B actionClass
    class C,E,F formClass
    class D decisionClass
    class G,H successClass
    class I errorClass                    
    V****Figure 3: Deal Creation Flow****
--------------------------------------------------------------------------------------------

### 4.3 Invoice Generation Flow (from a Deal)

    flowchart TD
    A[Deal Detail Page] --> B(Click 'Generate Invoice')
    B --> C[Invoice Creation Form - Pre-filled from Deal]
    C --> D{"Review/Edit Details:<br/>• Invoice Number (Suggest/Editable)<br/>• Issue/Due Dates<br/>• Client Info (from Deal)<br/>• Line Items (from Deal/Deliverables)<br/>• Amount (Calculated/Editable)<br/>• Notes<br/>• Payment Terms (from Settings)"}
    D --> E[Validate Form]
    E -->|Valid| F[Save Invoice as Draft]
    F --> G[Invoice Detail Page - Draft]
    G --> H[Show Success Toast/Notification]
    G --> I("Options:<br/>• Mark as Sent<br/>• Download PDF<br/>• Edit")
    E -->|Invalid| J[Show In-form Errors]
    J --> C

    classDef startClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef actionClass fill:#e8f5e8,stroke:#388e3c,stroke-width:2px
    classDef formClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef decisionClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef successClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef errorClass fill:#ffebee,stroke:#d32f2f,stroke-width:2px
    classDef optionsClass fill:#f1f8e9,stroke:#689f38,stroke-width:2px

    class A startClass
    class B actionClass
    class C,E,F formClass
    class D decisionClass
    class G,H successClass
    class J errorClass
    class I optionsClass

    V****Figure 4: Invoice Generation Flow****
-------------------------------------------------------------------------------------------------

### 4.4 Settings Update Flow (e.g., Profile Update)

    flowchart TD
    A[Dashboard/Navigation] --> B(Click 'Settings')
    B --> C[Settings Page - Select 'Account Profile']
    C --> D[Account Profile Form - Display Current Info]
    D --> E{"User Edits Fields:<br/>• Name<br/>• Business Name<br/>• Profile Picture<br/>• etc."}
    E --> F(Click 'Save Changes')
    F --> G[Validate Form]
    G -->|Valid| H[Update User Profile in Backend]
    H --> I[Show Success Toast/Notification]
    H --> D
    G -->|Invalid| J[Show In-form Errors]
    J --> D

    classDef startClass fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef actionClass fill:#e8f5e8,stroke:#388e3c,stroke-width:2px
    classDef formClass fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef decisionClass fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef processClass fill:#e1f5fe,stroke:#0288d1,stroke-width:2px
    classDef successClass fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef errorClass fill:#ffebee,stroke:#d32f2f,stroke-width:2px

    class A startClass
    class B,F actionClass
    class C,D,G formClass
    class E decisionClass
    class H processClass
    class I successClass
    class J errorClass
    V****Figure 5: Settings Update Flow****
----------------------------------------------------------------------------------------------------------------

### 4.5 Deal Listing & Filtering Flow

## - ****Description****: User navigates to the deals list, views all deals, and applies filters (e.g., by status, date) or sorts the list to find specific deals.

- ****Key Steps****:

  1. Navigate to "Deals" section from primary navigation.

  2. Deals list is displayed with default sort (e.g., most recent).

  3. User interacts with filter controls (dropdowns, date pickers).

  4. User interacts with sort controls.

  5. Deals list updates dynamically based on applied filters/sort.

  6. User can click on a deal to navigate to its Deal Detail View.

     (Mermaid diagram to be added)

### 4.6 Deal Detail View Flow

## - ****Description****: User views comprehensive information about a single deal, including its terms, deliverables, status, and related actions.

- ****Key Steps****:

  1. User clicks on a specific deal from the Deals List (or other entry point).

  2. Deal Detail page loads, displaying all relevant information (client, value, dates, description, deliverables list, status, notes, associated invoices).

  3. User can perform actions like "Edit Deal", "Add Deliverable", "Generate Invoice", "Set Reminder".

     (Mermaid diagram to be added)

### 4.7 Invoice Listing & Filtering Flow

## - ****Description****: Similar to Deal Listing, user navigates to invoices, views all, and applies filters/sorts.

- ****Key Steps****:

  1. Navigate to "Invoices" section.

  2. Invoice list displayed (default sort).

  3. User interacts with filter/sort controls.

  4. List updates.

  5. User can click an invoice to view its Invoice Detail View.

     (Mermaid diagram to be added)

### 4.8 Invoice Detail View Flow

## - ****Description****: User views details of a single invoice and can perform actions like marking as paid or downloading.

- ****Key Steps****:

  1. User clicks on an invoice from the Invoice List.

  2. Invoice Detail page loads (client, items, amount, status, dates, notes).

  3. User can perform actions: "Mark as Paid", "Download PDF", "Send Reminder" (if applicable).

     (Mermaid diagram to be added)

## 5. Wireframes & Mockups

### 5.1 Key Screen Wireframes

## This section will contain links to or embedded low-to-medium fidelity wireframes for all key screens and views identified in the user flows for the MVP. Wireframes will be developed with a mobile-first approach, demonstrating responsive adaptations for tablet and desktop layouts.* ****Key screens to include****:

  - Dashboard (Mobile, Tablet, Desktop)

  - Deal List (Mobile, Tablet, Desktop - including filter/sort interactions)

  - Deal Details (Mobile, Tablet, Desktop)

  - Deal Creation/Editing Form (Mobile, Tablet, Desktop)

  - Invoice List (Mobile, Tablet, Desktop - including filter/sort interactions)

  - Invoice Details (Mobile, Tablet, Desktop)

  - Invoice Creation/Editing Form (Mobile, Tablet, Desktop)

  - Settings Pages (Account, Notifications, Invoice Defaults - Mobile, Tablet, Desktop)

  - Sign In / Sign Up / Password Reset Pages (Mobile, Tablet, Desktop)

* __(Wireframes to be developed and linked here)__

### 5.2 Interactive Prototypes

## Interactive prototypes will be created using a tool like Figma to validate the user experience for key user flows before implementation. These will also demonstrate responsive behavior.* ****Key flows to prototype****:

  1. Onboarding (Sign Up, Email Verification, Initial Login)

  2. Deal creation and deliverable management flow

  3. Invoice generation and status update flow

  4. Settings update flow (e.g., Invoice Defaults)

* __(Prototypes to be developed and linked here)__

## 6. Component Library/Design System Reference

### 6.1 Core Components

## The application will primarily use shadcn/ui as its component library, customized and extended as needed to match the Creator's Deal Hub brand identity. Styling will be done using Tailwind CSS. While conceptual consistency with the mobile app's UI is desired, the web UI will primarily be a fresh build leveraging web-native shadcn/ui patterns and components, rather than a direct port of existing mobile components.Key components include:

#### Navigation Components

## - Header with responsive navigation (e.g., using shadcn/ui Navigation Menu, Dropdown Menu)

- Sidebar navigation (desktop - potentially using shadcn/ui Collapsible or custom layout)

- Bottom navigation bar (mobile - custom or adapted from mobile patterns)

- Breadcrumbs (e.g., shadcn/ui Breadcrumb if available, or custom)

#### Form Components

## (Leveraging shadcn/ui Form, Input, Select, RadioGroup, Checkbox, DatePicker, Textarea)* Text inputs

* Select dropdowns

* Radio buttons

* Checkboxes

* Date pickers

* File uploads (for logos, etc.)

* Form validation indicators (integrated with React Hook Form)

#### Content Components

## (Leveraging shadcn/ui Card, Table, Tabs, Accordion, Dialog, Popover)* Cards

* Tables (for lists of deals/invoices)

* Lists

* Tabs

* Accordions

* Modals/Dialogs

#### Feedback Components

## (Leveraging shadcn/ui Toast, Alert, Progress, Skeleton)* Toast notifications

* Alert banners

* Progress indicators

* Loading states (Skeletons)

### 6.2 Component Variations

## Each component will have consistent variations for:* States: Default, Hover, Focus, Active, Disabled (as provided by shadcn/ui and Tailwind focus/disabled utilities)

* Sizes: Small, Medium, Large (where applicable, using shadcn/ui variants or Tailwind classes)

* Variants: Primary, Secondary, Destructive (e.g., for Buttons)

### 6.3 Micro-interactions and Component States

## - ****Button Press****: Subtle scale or color change.

- ****Input Focus****: Border highlight, possibly a subtle shadow.

- ****Loading States****: Use skeleton loaders for content areas, spinners for buttons or small sections.

- ****Transitions****: Smooth transitions for modal pop-ups, dropdowns, and accordion expansions (leveraging Tailwind/shadcn animation utilities).

- ****Hover States****: Clear visual feedback on hover for all interactive elements (e.g., links, buttons, list items).

### 6.4 Component Documentation

## (To be developed alongside the Frontend Architecture Plan)Each custom component or significant customization of a shadcn/ui component will be documented with:* Usage guidelines

* Props/configuration options

* Accessibility considerations (ARIA roles, keyboard navigation)

* Code examples (Storybook or similar to be considered)

## 7. Branding & Style Guide Reference

### 7.1 Color Palette

## (Based on shadcn/ui theming capabilities, customizable via CSS variables)

#### Primary Colors

## - Primary: `hsl(222.2, 47.4%, 11.2%)` - Dark blue for primary actions and branding

- Primary Foreground: `hsl(210, 40%, 98%)` - Light text on primary backgrounds

#### Secondary Colors

## - Secondary: `hsl(210, 40%, 96.1%)` - Light gray/blue for secondary elements

- Secondary Foreground: `hsl(222.2, 47.4%, 11.2%)` - Dark text on secondary backgrounds

#### Accent Colors

## - Accent: `hsl(210, 40%, 96.1%)` (Can be same as Secondary or a distinct color like a brighter blue/teal)

- Accent Foreground: `hsl(222.2, 47.4%, 11.2%)` - Dark text on accent backgrounds

#### Semantic Colors

## - Success: `hsl(142.1, 70.6%, 45.3%)` (shadcn default green-600)

- Warning: `hsl(38.3, 95.8%, 50.0%)` (shadcn default yellow-500)

- Destructive: `hsl(0, 84.2%, 60.2%)` (shadcn default red-500)

- Info: `hsl(217.2, 91.2%, 59.8%)` (shadcn default blue-500)

#### Neutral Colors

## (shadcn/ui provides a rich set of grays - `slate`, `gray`, `zinc`, `neutral`, `stone`)* Background: `hsl(0, 0%, 100%)` (shadcn default `background`)

* Foreground: `hsl(222.2, 84%, 4.9%)` (shadcn default `foreground`)

* Muted: `hsl(210, 40%, 96.1%)` (shadcn default `muted`)

* Muted Foreground: `hsl(215.4, 16.3%, 46.9%)` (shadcn default `muted-foreground`)

* Border: `hsl(214.3, 31.8%, 91.4%)` (shadcn default `border`)

* Input: `hsl(214.3, 31.8%, 91.4%)` (shadcn default `input`)

* Ring (Focus): `hsl(215.2, 70.6%, 45.3%)` (shadcn default `ring`)

### 7.2 Typography

#### Font Family

## - Primary Font: Manrope (sans-serif) - Ensure this is configured in Tailwind CSS.

#### Font Sizes

## (Tailwind CSS provides a comprehensive scale - `text-xs`, `text-sm`, `text-base`, etc. These will be used.)* xs: 0.75rem (12px)

* sm: 0.875rem (14px)

* base: 1rem (16px)

* lg: 1.125rem (18px)

* xl: 1.25rem (20px)

* 2xl: 1.5rem (24px)

* 3xl: 1.875rem (30px)

* 4xl: 2.25rem (36px)

#### Font Weights

## (Map to Tailwind `font-normal`, `font-medium`, `font-semibold`, `font-bold`)* Regular: 400

* Medium: 500

* Semibold: 600

* Bold: 700

#### Line Heights

## (Use Tailwind `leading-tight`, `leading-normal`, `leading-relaxed`)* Tight: 1.25

* Normal: 1.5

* Relaxed: 1.75

### 7.3 Spacing System

## Based on a 4px grid system, aligned with Tailwind's default spacing scale (e.g., `p-1` = 4px, `p-2` = 8px).* 0: 0px

* 1: 0.25rem (4px)

* 2: 0.5rem (8px)

* 3: 0.75rem (12px)

* 4: 1rem (16px)

* 5: 1.25rem (20px)

* 6: 1.5rem (24px)

* 8: 2rem (32px)

* 10: 2.5rem (40px)

* 12: 3rem (48px)

* 16: 4rem (64px)

### 7.4 Iconography

## The application will use ****Lucide icons**** for consistency and accessibility, as recommended by shadcn/ui.

### 7.5 Shadows & Elevation

## Utilize Tailwind CSS shadow utilities (e.g., `shadow-sm`, `shadow-md`, `shadow-lg`, `shadow-xl`).* Shadow-xs: Subtle shadow for cards and containers

* Shadow-sm: Light shadow for elevated elements

* Shadow-md: Medium shadow for modals and popovers

* Shadow-lg: Heavy shadow for important elements

### 7.6 Border Radius

## Utilize Tailwind CSS border radius utilities (e.g., `rounded-sm`, `rounded-md`, `rounded-lg`).* Radius-sm: 0.125rem (2px)

* Radius-md: 0.375rem (6px)

* Radius-lg: 0.5rem (8px)

* Radius-xl: 0.75rem (12px)

* Radius-full: 9999px (for pills and avatars)

## 8. Accessibility (AX) Requirements

### 8.1 Standards Compliance

## The application will comply with WCAG 2.1 AA standards, ensuring:* Perceivable: Information and UI components must be presentable to users in ways they can perceive.

* Operable: UI components and navigation must be operable.

* Understandable: Information and operation of the UI must be understandable.

* Robust: Content must be robust enough to be interpreted by a wide variety of user agents.

### 8.2 Keyboard Navigation

## - All interactive elements must be keyboard accessible.

- Logical tab order following visual layout.

- Focus indicators must be visible and clear (Tailwind's `focus:ring` utilities will be used).

- Keyboard shortcuts for common actions (to be defined, e.g., "Ctrl+S" for save where appropriate).

### 8.3 Screen Reader Support

## - Proper semantic HTML structure.

- ARIA labels and roles where appropriate, especially for custom components or complex shadcn/ui composites.

- Alternative text for images and icons.

- Descriptive link text.

### 8.4 Color & Contrast

## - Minimum contrast ratio of 4.5:1 for normal text.

- Minimum contrast ratio of 3:1 for large text.

- Color is not the only means of conveying information.

- High contrast mode support (consider system preferences and potential theme toggle).

### 8.5 Motion & Animation

## - Respect user preferences for reduced motion (`prefers-reduced-motion` media query).

- No flashing content that could trigger seizures.

- Animations should be subtle and purposeful (e.g., using Tailwind/shadcn animation utilities).

### 8.6 ARIA Implementation Guidance

## - For custom interactive components not directly from shadcn/ui, ensure appropriate ARIA roles (e.g., `role="button"`, `role="dialog"`), states (e.g., `aria-expanded`, `aria-selected`), and properties (e.g., `aria-labelledby`, `aria-describedby`) are used.

- When extending shadcn/ui components, verify that accessibility is maintained or enhanced.

- Dynamic content updates should use ARIA live regions (`aria-live`, `aria-atomic`, `aria-relevant`) where necessary to inform screen reader users.

- Complex UI patterns (e.g., custom data tables, tab panels if not using shadcn defaults) must follow ARIA authoring practices.

## 9. Responsiveness

### 9.1 Breakpoints

## The application will use Tailwind CSS default breakpoints, which are generally:* `sm`: 640px

* `md`: 768px

* `lg`: 1024px

* `xl`: 1280px

* 2xl: 1536px

  (Design will primarily focus on mobile <640px, tablet 640px-1024px, and desktop >1024px for layout shifts).

### 9.2 Mobile-First Approach

## All interfaces will be designed with a mobile-first approach, ensuring:* Content prioritization for small screens.

* Touch-friendly tap targets (minimum 44x44px).

* Simplified layouts for mobile devices.

* Progressive enhancement for larger screens.

### 9.3 Layout Adaptations

#### Mobile Adaptations

## - Single column layouts primarily.

- Bottom navigation bar or hamburger menu for primary navigation.

- Collapsible sections (Accordions) for dense information.

- Modal dialogs for complex forms or actions.

#### Tablet Adaptations

## - Two-column layouts where appropriate (e.g., master-detail views).

- Sidebar navigation (collapsible or persistent depending on orientation/space).

- Expanded form layouts.

#### Desktop Adaptations

## - Multi-column layouts for optimal use of space.

- Persistent sidebar navigation.

- Advanced data visualization (if applicable for future analytics).

- Enhanced keyboard shortcuts.

### 9.4 Touch vs. Mouse Interactions

## - ****Touch interactions****: Ensure sufficient tap target sizes, support for swipe gestures where intuitive (e.g., carousels, list item actions - post-MVP).

- ****Mouse interactions****: Provide clear hover states for interactive elements; consider right-click context menus for advanced actions (post-MVP).

## 10. Design Considerations for Next.js & Supabase

## - ****Loading States****: Design clear loading indicators (skeletons, spinners) for data fetched via Next.js Server Components, Client Components (using SWR/React Query), or directly from Supabase.

- ****Empty States****: Design informative empty states for lists (deals, invoices) when no data is available.

- ****Error States****: Design user-friendly error messages for API failures (Supabase interactions, Next.js API routes) or validation errors.

- ****Optimistic Updates****: For actions like creating or updating data, consider UI patterns that support optimistic updates to enhance perceived performance (relevant for SWR/React Query usage).

- ****Server vs. Client Components****: While an architectural concern, the choice impacts interactivity. Design components with an understanding of where they might render (server or client) to ensure smooth UX.

## 11. Change Log

## |             |            |                  |                                                                                                                                                                                                                                                          |
| ----------- | ---------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Version** | **Date**   | **Author**       | **Description**                                                                                                                                                                                                                                          |
| 0.1         | 2023-07-10 | Millie (Initial) | Initial draft (as provided by user)                                                                                                                                                                                                                      |
| 1.0         | 2025-06-02 | Millie (BMAD)    | Updated version, date, related doc paths. Elaborated on personas. Added placeholders/descriptions for new user flows. Updated wireframe/mockup sections. Expanded Design System & Accessibility sections. Added note on Next.js/Supabase considerations. |
