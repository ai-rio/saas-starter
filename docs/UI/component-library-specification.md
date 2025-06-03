# Creator's Deal Hub Component Library Specification

## 1. Introduction

### 1.1 Purpose

This document defines the component library specification for the Creator's Deal Hub (CDH) Next.js web application. It outlines the design system, component organization, implementation details, and usage guidelines to ensure consistency, reusability, and maintainability across the application.

### 1.2 Scope

This specification covers:
- Component design philosophy and principles
- Component organization and structure
- Implementation details for shadcn/ui components
- Custom component guidelines
- Theming and styling approach
- Accessibility considerations
- Component documentation standards

### 1.3 Audience

This document is intended for:
- Frontend developers implementing the CDH web application
- Designers working on UI/UX for the application
- QA engineers testing the application
- Project stakeholders reviewing the technical approach

### 1.4 Related Documents

- UX/UI Specification
- Frontend Architecture Plan
- Product Requirements Document (PRD) Version 1.7
- Architecture Document Version 1.2

## 2. Component Design Philosophy

### 2.1 Overall Philosophy

The CDH component library follows these core principles:

1. **Composition Over Inheritance**: Components are designed to be composed together rather than extended through inheritance, promoting flexibility and reusability.

2. **Atomic Design Methodology**: Components are organized following the Atomic Design principles (atoms, molecules, organisms, templates, pages) to create a scalable and maintainable component hierarchy.

3. **Accessibility First**: All components are designed with accessibility in mind from the beginning, ensuring compliance with WCAG 2.1 AA standards.

4. **Mobile-First Responsive Design**: Components are designed to work on mobile devices first, then scale up to larger screens.

5. **Performance Optimization**: Components are optimized for performance, with careful consideration of bundle size, rendering efficiency, and runtime performance.

### 2.2 Design Patterns

#### 2.2.1 Compound Components

Compound components are used to create complex UI elements with multiple related parts. This pattern allows for flexible composition while maintaining semantic relationships between components.

Example: The `Card` component consists of `Card`, `CardHeader`, `CardTitle`, `CardDescription`, `CardContent`, and `CardFooter` subcomponents.

#### 2.2.2 Controlled vs. Uncontrolled Components

Components can be implemented as either controlled (state managed by parent) or uncontrolled (state managed internally) based on use case requirements.

#### 2.2.3 Render Props and Higher-Order Components

These patterns are used sparingly and only when they provide significant benefits over simpler approaches.

## 3. Component Organization

### 3.1 Directory Structure

Components are organized in the following directory structure:

```
/components
  /ui                 # Base UI components from shadcn/ui
  /feature            # Feature-specific components
    /auth             # Authentication-related components
    /deals            # Deal management components
    /invoices         # Invoice management components
    /dashboard        # Dashboard components
  /layout             # Layout components (Header, Sidebar, etc.)
  /shared             # Shared components used across features
```

### 3.2 Naming Conventions

- Component files use PascalCase: `Button.tsx`, `DealCard.tsx`
- Component directories use kebab-case: `deal-form`, `invoice-list`
- Component props interfaces are named with the component name followed by `Props`: `ButtonProps`, `DealCardProps`

## 4. shadcn/ui Implementation

### 4.1 Overview

The CDH web application uses shadcn/ui as its core component library. shadcn/ui provides a collection of accessible, reusable, and customizable React components that are styled using Tailwind CSS.

Key characteristics of shadcn/ui:
- Not installed as a dependency but copied into the project
- Fully customizable components
- Built with Radix UI primitives for accessibility
- Styled with Tailwind CSS
- Supports both light and dark modes

### 4.2 Configuration

The shadcn/ui configuration is defined in `components.json`:

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.js",
    "css": "app/globals.css",
    "baseColor": "zinc",
    "cssVariables": true
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "icon": "lucide"
}
```

### 4.3 Theme Configuration

The theme is configured using CSS variables in `app/globals.css`. The application supports both light and dark modes with distinct color palettes for each.

#### 4.3.1 Color Palette

**Light Mode**
```css
:root {
  --background: 0 0% 100%;
  --foreground: 222.2 84% 4.9%;
  --card: 0 0% 100%;
  --card-foreground: 222.2 84% 4.9%;
  --popover: 0 0% 100%;
  --popover-foreground: 222.2 84% 4.9%;
  --primary: 222.2 47.4% 11.2%;
  --primary-foreground: 210 40% 98%;
  --secondary: 210 40% 96.1%;
  --secondary-foreground: 222.2 47.4% 11.2%;
  --muted: 210 40% 96.1%;
  --muted-foreground: 215.4 16.3% 46.9%;
  --accent: 210 40% 96.1%;
  --accent-foreground: 222.2 47.4% 11.2%;
  --destructive: 0 84.2% 60.2%;
  --destructive-foreground: 210 40% 98%;
  --border: 214.3 31.8% 91.4%;
  --input: 214.3 31.8% 91.4%;
  --ring: 222.2 84% 4.9%;
  --radius: 0.5rem;
}
```

**Dark Mode**
```css
.dark {
  --background: 222.2 84% 4.9%;
  --foreground: 210 40% 98%;
  --card: 222.2 84% 4.9%;
  --card-foreground: 210 40% 98%;
  --popover: 222.2 84% 4.9%;
  --popover-foreground: 210 40% 98%;
  --primary: 210 40% 98%;
  --primary-foreground: 222.2 47.4% 11.2%;
  --secondary: 217.2 32.6% 17.5%;
  --secondary-foreground: 210 40% 98%;
  --muted: 217.2 32.6% 17.5%;
  --muted-foreground: 215 20.2% 65.1%;
  --accent: 217.2 32.6% 17.5%;
  --accent-foreground: 210 40% 98%;
  --destructive: 0 62.8% 30.6%;
  --destructive-foreground: 210 40% 98%;
  --border: 217.2 32.6% 17.5%;
  --input: 217.2 32.6% 17.5%;
  --ring: 212.7 26.8% 83.9%;
}
```

#### 4.3.2 Typography

The application uses the Manrope font family as its primary typeface:

```css
@layer utilities {
  body {
    font-family: "Manrope", Arial, Helvetica, sans-serif;
  }
}
```

#### 4.3.3 Border Radius

The application uses a consistent border radius defined by the `--radius` CSS variable:

```css
--radius: 0.5rem;
--radius-lg: var(--radius);
--radius-md: calc(var(--radius) - 2px);
--radius-sm: calc(var(--radius) - 4px);
```

## 5. Core Components

### 5.1 Button

**Purpose**: Provides an interactive element for user actions.

**Source File**: `/components/ui/button.tsx`

**Props**:
- `variant`: Defines the visual style of the button. Options: `default`, `destructive`, `outline`, `secondary`, `ghost`, `link`.
- `size`: Defines the size of the button. Options: `default`, `sm`, `lg`, `icon`.
- `asChild`: When true, the component will render its child as the root element.

**Usage Example**:
```tsx
<Button variant="default" size="default">
  Click me
</Button>

<Button variant="destructive" size="sm">
  Delete
</Button>

<Button variant="outline" size="lg">
  Cancel
</Button>

<Button variant="ghost" size="icon">
  <Icon />
</Button>
```

### 5.2 Card

**Purpose**: Provides a container for related content.

**Source File**: `/components/ui/card.tsx`

**Subcomponents**:
- `Card`: The main container component.
- `CardHeader`: Container for the card's header content.
- `CardTitle`: The title of the card.
- `CardDescription`: A description or subtitle for the card.
- `CardContent`: The main content area of the card.
- `CardFooter`: Container for the card's footer content.

**Usage Example**:
```tsx
<Card>
  <CardHeader>
    <CardTitle>Card Title</CardTitle>
    <CardDescription>Card Description</CardDescription>
  </CardHeader>
  <CardContent>
    <p>Card Content</p>
  </CardContent>
  <CardFooter>
    <Button>Action</Button>
  </CardFooter>
</Card>
```

### 5.3 Input

**Purpose**: Provides a form input field for user data entry.

**Source File**: `/components/ui/input.tsx`

**Props**:
- Standard HTML input attributes

**Usage Example**:
```tsx
<Input type="text" placeholder="Enter your name" />
<Input type="email" placeholder="Enter your email" />
<Input type="password" placeholder="Enter your password" />
```

### 5.4 Label

**Purpose**: Provides an accessible label for form elements.

**Source File**: `/components/ui/label.tsx`

**Props**:
- Standard HTML label attributes

**Usage Example**:
```tsx
<div className="grid w-full max-w-sm items-center gap-1.5">
  <Label htmlFor="email">Email</Label>
  <Input type="email" id="email" placeholder="Email" />
</div>
```

## 6. Feature-Specific Components

### 6.1 Deal Management Components

#### 6.1.1 DealCard

**Purpose**: Displays a summary of a deal.

**Source File**: `/components/feature/deals/DealCard.tsx`

**Props**:
- `deal`: The deal object containing deal data.
- `onView`: Callback function when the view button is clicked.
- `onEdit`: Callback function when the edit button is clicked.
- `onDelete`: Callback function when the delete button is clicked.

**Internal State**:
- `isMenuOpen`: Boolean state to track if the action menu is open.

**UI Elements**:
- Card component with deal information
- Status badge
- Action menu with view, edit, and delete options

**Usage Example**:
```tsx
<DealCard 
  deal={deal}
  onView={() => router.push(`/deals/${deal.id}`)}
  onEdit={() => router.push(`/deals/${deal.id}/edit`)}
  onDelete={() => handleDeleteDeal(deal.id)}
/>
```

#### 6.1.2 DealForm

**Purpose**: Provides a form for creating and editing deals.

**Source File**: `/components/feature/deals/DealForm.tsx`

**Props**:
- `initialData`: Optional initial deal data for editing.
- `onSubmit`: Callback function when the form is submitted.
- `isLoading`: Boolean indicating if the form is in a loading state.

**Internal State**:
- Form state managed by React Hook Form

**UI Elements**:
- Form inputs for deal details
- Client selection dropdown
- Date pickers for start and end dates
- Submit and cancel buttons

**Usage Example**:
```tsx
<DealForm
  initialData={deal}
  onSubmit={handleSubmit}
  isLoading={isSubmitting}
/>
```

### 6.2 Invoice Management Components

#### 6.2.1 InvoiceCard

**Purpose**: Displays a summary of an invoice.

**Source File**: `/components/feature/invoices/InvoiceCard.tsx`

**Props**:
- `invoice`: The invoice object containing invoice data.
- `onView`: Callback function when the view button is clicked.
- `onEdit`: Callback function when the edit button is clicked.
- `onDelete`: Callback function when the delete button is clicked.

**Internal State**:
- `isMenuOpen`: Boolean state to track if the action menu is open.

**UI Elements**:
- Card component with invoice information
- Payment status badge
- Action menu with view, edit, and delete options

**Usage Example**:
```tsx
<InvoiceCard 
  invoice={invoice}
  onView={() => router.push(`/invoices/${invoice.id}`)}
  onEdit={() => router.push(`/invoices/${invoice.id}/edit`)}
  onDelete={() => handleDeleteInvoice(invoice.id)}
/>
```

#### 6.2.2 InvoiceForm

**Purpose**: Provides a form for creating and editing invoices.

**Source File**: `/components/feature/invoices/InvoiceForm.tsx`

**Props**:
- `initialData`: Optional initial invoice data for editing.
- `onSubmit`: Callback function when the form is submitted.
- `isLoading`: Boolean indicating if the form is in a loading state.

**Internal State**:
- Form state managed by React Hook Form

**UI Elements**:
- Form inputs for invoice details
- Deal selection dropdown
- Line items management
- Submit and cancel buttons

**Usage Example**:
```tsx
<InvoiceForm
  initialData={invoice}
  onSubmit={handleSubmit}
  isLoading={isSubmitting}
/>
```

## 7. Layout Components

### 7.1 Header

**Purpose**: Provides the main application header with navigation and user menu.

**Source File**: `/components/layout/Header.tsx`

**Props**:
- `user`: The current user object.

**UI Elements**:
- Logo
- Navigation links
- User menu dropdown
- Theme toggle

### 7.2 Sidebar

**Purpose**: Provides navigation sidebar for desktop view.

**Source File**: `/components/layout/Sidebar.tsx`

**Props**:
- `items`: Navigation items to display.
- `collapsed`: Boolean indicating if the sidebar is collapsed.
- `onToggleCollapse`: Callback function to toggle sidebar collapse state.

**UI Elements**:
- Navigation links with icons
- Collapse toggle button

### 7.3 MobileNav

**Purpose**: Provides bottom navigation for mobile view.

**Source File**: `/components/layout/MobileNav.tsx`

**Props**:
- `items`: Navigation items to display.

**UI Elements**:
- Navigation links with icons in a bottom bar

## 8. Component Implementation Guidelines

### 8.1 Server vs. Client Components

Components should be implemented as Server Components by default, with the `'use client'` directive added only when necessary for client-side interactivity.

**Server Components**:
- Static UI components
- Components that fetch data
- Components that don't need interactivity

**Client Components**:
- Components that use React hooks
- Components that use browser-only APIs
- Components that handle user events
- Components that use effects or state

### 8.2 Props Interface Guidelines

- Use TypeScript interfaces to define component props
- Extend HTML element props when appropriate
- Use descriptive names for props
- Document props with JSDoc comments

Example:
```tsx
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  /**
   * The visual style of the button
   * @default "default"
   */
  variant?: "default" | "destructive" | "outline" | "secondary" | "ghost" | "link";
  
  /**
   * The size of the button
   * @default "default"
   */
  size?: "default" | "sm" | "lg" | "icon";
  
  /**
   * When true, the component will render its child as the root element
   * @default false
   */
  asChild?: boolean;
}
```

### 8.3 Styling Guidelines

- Use Tailwind CSS for styling
- Use the `cn` utility function for conditional class names
- Follow the project's color palette and design tokens
- Use CSS variables for theme values

Example:
```tsx
const buttonVariants = cva(
  "inline-flex items-center justify-center whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive: "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline: "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
        secondary: "bg-secondary text-secondary-foreground hover:bg-secondary/80",
        ghost: "hover:bg-accent hover:text-accent-foreground",
        link: "text-primary underline-offset-4 hover:underline",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 rounded-md px-3",
        lg: "h-11 rounded-md px-8",
        icon: "h-10 w-10",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  }
);
```

## 9. Accessibility Guidelines

### 9.1 General Principles

- All components must be keyboard navigable
- All interactive elements must have appropriate ARIA attributes
- Color contrast must meet WCAG 2.1 AA standards
- Focus states must be visible
- Screen reader announcements must be appropriate

### 9.2 Component-Specific Guidelines

**Buttons**:
- Use the `button` element for clickable actions
- Provide descriptive text or aria-label

**Forms**:
- Associate labels with form controls
- Provide error messages that are announced to screen readers
- Group related form controls with fieldset and legend

**Modals**:
- Trap focus within the modal when open
- Return focus to the triggering element when closed
- Use appropriate ARIA roles and attributes

## 10. Component Documentation Standards

### 10.1 Documentation Format

Each component should be documented with:

1. **Purpose**: A brief description of the component's purpose.
2. **Props**: A table of the component's props, their types, default values, and descriptions.
3. **Examples**: Code examples showing common usage patterns.
4. **Accessibility**: Any specific accessibility considerations.
5. **Notes**: Any additional information or caveats.

### 10.2 Example Documentation

```markdown
# Button

A button component that follows the shadcn/ui design system.

## Props

| Name     | Type                                                                   | Default     | Description                                           |
| -------- | ---------------------------------------------------------------------- | ----------- | ----------------------------------------------------- |
| variant  | "default" \| "destructive" \| "outline" \| "secondary" \| "ghost" \| "link" | "default"   | The visual style of the button                       |
| size     | "default" \| "sm" \| "lg" \| "icon"                                    | "default"   | The size of the button                               |
| asChild  | boolean                                                                | false       | When true, renders the child as the root element      |

## Examples

```tsx
<Button variant="default">Default Button</Button>
<Button variant="destructive">Destructive Button</Button>
<Button variant="outline">Outline Button</Button>
```

## Accessibility

- The button is keyboard accessible and can be activated with the Enter or Space keys.
- When used with an icon only, ensure to provide an aria-label for screen readers.
```

## 11. Change Log

| Version | Date       | Author | Description                                |
| ------- | ---------- | ------ | ------------------------------------------ |
| 1.0     | 2023-06-15 | Millie | Initial component library specification    |