# Frontend Architecture Plan - Creator's Deal Hub

# Version: 1.2Date: June 2, 2025Author: Millie (Design Architect)

## 1. Introduction

### 1.1 Purpose

# This document outlines the frontend architecture plan for the Creator's Deal Hub web application. It serves as a comprehensive guide for the implementation of the frontend components, ensuring a consistent, maintainable, and scalable codebase that aligns with the project requirements and UX/UI specifications.

### 1.2 Scope

# This architecture plan covers the frontend structure, component organization, state management, API interaction, routing strategy, build process, testing approach, and other technical considerations for the Creator's Deal Hub web application.

### 1.3 Audience

# This document is intended for frontend developers, backend developers, technical leads, and other stakeholders involved in the development of the Creator's Deal Hub web application.

### 1.4 Related Documents

# - [Creator's Deal Hub PRD (`web/docs/prd/creator-deal-hub-prd.md`)]

- [Creator's Deal Hub Architecture (`web/docs/architecture/creator-deal-hub-architecture.md`)]

- [UX/UI Specification (`web/docs/UI/ux-ui-specification.md`)]

- [Project Brief (`web/docs/project-brief/project-brief.md`)]

## 2. Overall Frontend Philosophy & Patterns

### 2.1 Architectural Approach

# The Creator's Deal Hub frontend will follow a component-based architecture using Next.js with the App Router pattern. This approach emphasizes:* ****Server Components First****: Leveraging Next.js 13+ server components for improved performance and SEO.

* ****Client Components When Needed****: Using client components for interactive elements that require client-side state.

* ****Modular Design****: Building reusable, self-contained components that can be composed to create complex interfaces.

* ****Progressive Enhancement****: Aiming for core functionality to work without JavaScript where feasible, then enhancing with client-side features.

* ****Mobile-First****: Designing and implementing for mobile devices first, then scaling up to larger screens.

### 2.2 Design Patterns

#### Component Patterns

# - ****Atomic Design (Conceptual)****: Organizing components into atoms, molecules, organisms, templates, and pages as a guiding principle.

- ****Compound Components****: Creating related components that work together to provide complex functionality (e.g., a custom select component).

- ****Render Props/Custom Hooks****: Using render props and custom hooks (e.g., `useAuth`, `useDeals`) to share stateful logic and functionality between components.

- ****Container/Presentational (Implicit with Server/Client Components)****: Server Components often act as containers fetching data, while Client Components handle presentation and interactivity.

#### State Management Patterns

# - ****Server State****: Using SWR (or React Query) for data fetching, caching, and optimistic updates.

- ****Client State****: Using React Context API for global UI state (e.g., theme, auth status) and `useState`/`useReducer` for local component state.

- ****Form State****: Using React Hook Form for complex forms, leveraging its performance and validation capabilities.

### 2.3 Code Organization Principles

# - ****Feature-First****: Organizing code by feature (e.g., `deals`, `invoices`) rather than by technical role (e.g., all components in one folder, all hooks in another).

- ****Co-location****: Keeping related files (component, styles if any, tests, stories) close together within their feature or component directory.

- ****Single Responsibility****: Each component and module should aim to have a single, well-defined responsibility.

- ****DRY (Don't Repeat Yourself)****: Extracting common functionality into reusable components, hooks, and utilities.

- ****Consistent Naming****: Following consistent naming conventions for files, components, functions, and variables.

## 3. Detailed Frontend Directory Structure

    /app                           # Next.js App Router directory
      /(auth)/                     # Authentication routes group (e.g., sign-in, sign-up)
        /sign-in/page.tsx
        /sign-up/page.tsx
        # ... other auth-related pages (e.g., forgot-password)
        actions.ts                 # Server actions for auth (if applicable)
        layout.tsx                 # Layout specific to auth pages
      /(dashboard)/                # Authenticated dashboard routes group
        /deals/                    # Deals management feature
          page.tsx                 # Deals list page
          /create/page.tsx         # Create deal page
          /[id]/page.tsx           # Deal details page
          /[id]/edit/page.tsx      # Edit deal page
          components/              # Components specific to the deals feature
            DealForm.tsx
            DeliverablesSection.tsx
        /invoices/                 # Invoices management feature
          page.tsx                 # Invoices list page
          /create/page.tsx         # Create invoice page (likely contextual from a deal)
          /[id]/page.tsx           # Invoice details page
          /[id]/edit/page.tsx      # Edit invoice page
          components/              # Components specific to the invoices feature
            InvoiceForm.tsx
            LineItemEditor.tsx
        /settings/                 # User settings feature
          page.tsx                 # Main settings page (could be a layout for sub-settings)
          /account/page.tsx
          /notifications/page.tsx
          /branding/page.tsx       # For invoice defaults, logo etc.
          # /team/page.tsx         # Future team management
          components/              # Components specific to settings
        layout.tsx                 # Layout for all dashboard pages (e.g., with sidebar)
        page.tsx                   # Main dashboard overview page
      /api/                        # API routes (Next.js backend handlers)
        /auth/[...nextauth]/route.ts # Example if using NextAuth.js with Supabase adapter
        # ... other API routes for server-side logic interacting with Supabase
      globals.css                  # Global CSS styles
      layout.tsx                   # Root layout for the entire application
      page.tsx                     # Landing page (public)
    /components                    # Shared, reusable components across features
      /layout/                     # Global layout components (Header, Sidebar, Footer, PageWrapper)
        Header.tsx
        Sidebar.tsx
        Footer.tsx
      /ui/                         # Core UI elements, primarily from shadcn/ui
        button.tsx                 # (shadcn/ui Button)
        card.tsx                   # (shadcn/ui Card)
        input.tsx                  # (shadcn/ui Input)
        # ... other shadcn/ui components re-exported or customized
      # /shared-feature-components/ # e.g., UserAvatar.tsx, if used in multiple distinct features
    /hooks                         # Custom React hooks (global or widely shared)
      useAuth.ts                   # (Example, might be part of lib/auth)
      useMediaQuery.ts
      # ... other custom hooks
    /lib                           # Utility functions, Supabase client setup, constants
      utils.ts                     # General utility functions (formatting, etc.)
      supabaseClient.ts            # Supabase client initialization
      constants.ts                 # Application-wide constants
      /auth/                       # Auth-specific utilities (e.g., Supabase Auth helpers)
      /validation/                 # Zod schemas for form validation
    /types                         # TypeScript type definitions
      index.ts                     # Shared/global types
      deals.ts
      invoices.ts
      user.ts
    /public                        # Static assets (images, fonts, icons)
      /images/
      /fonts/
      favicon.ico
      manifest.json                # PWA manifest
      service-worker.js            # PWA service worker
    # ... other root files (next.config.js, tailwind.config.js, etc.)
=====================================================================

## 4. Component Breakdown & Implementation Details

### 4.1 Component Organization

# Components will be organized conceptually following ****Atomic Design**** principles to guide structure and reusability:1) ****Atoms****: Basic UI elements, primarily sourced from `components/ui/` (which are shadcn/ui components).

   - Example: `components/ui/button.tsx`, `components/ui/input.tsx`.

2) ****Molecules****: Simple combinations of atoms forming a distinct unit.

   - Example: A form field combining a `Label` and `Input` atom, or a search bar.

3) ****Organisms****: More complex UI sections composed of molecules and/or atoms, representing distinct parts of an interface.

   - Example: `components/deals/DealCard.tsx`, `components/layout/Header.tsx`.

4) ****Templates****: Page-level layouts defining the structure of a page, often using slots for content. These are largely handled by Next.js `layout.tsx` files.

5) ****Pages****: Specific instances of templates, representing full views within the `app/` directory.Feature-specific components (molecules, organisms) will reside within their respective feature folders (e.g., `app/(dashboard)/deals/components/`). Globally shared components will be in the root `components/` directory.

### 4.2 Component Naming Conventions

# - ****PascalCase**** for component files and component names (e.g., `DealCard.tsx`, `function DealCard() {}`).

- ****camelCase**** for utility functions, hooks, and variables.

- ****kebab-case**** for CSS class names (if custom CSS is written outside Tailwind utilities) and non-component file names (e.g., `deal-service.ts`). Primarily for any custom global CSS or very specific, non-utility component styles not covered by Tailwind. Tailwind utility classes will be the primary method for styling directly in JSX.

- ****Descriptive Prefixes/Suffixes****: Use prefixes/suffixes to indicate component type or context where helpful (e.g., `DealForm.tsx`, `useAuth.ts`).

### 4.3 Component Implementation Strategy

#### Server vs. Client Components

# - ****Server Components (Default)****:

  - Used for static content rendering, data fetching directly (e.g., using `async/await` in the component), and SEO-critical parts.

  - Components that do not require browser APIs or interactivity (event handlers, state).

  - Example: A page displaying a list of deals where the initial data fetch happens on the server.

- ****Client Components (With `'use client'` directive)****:

  - Used for interactive UI elements (e.g., forms, buttons with onClick handlers, dropdowns).

  - Components that use React hooks (`useState`, `useEffect`, `useContext`).

  - Components that rely on browser APIs (e.g., `localStorage`, `window`).

  - Example: The `DealForm.tsx` which handles user input and state.

#### Component Template (Example)

    // Component Name: DealCard
    // Location: app/(dashboard)/deals/components/DealCard.tsx (if specific to deals list)
    //        OR components/shared-feature-components/DealCard.tsx (if used more broadly)
    // Description: Displays a summary of a deal with key information and actions.
    // Usage: Used in deal listings and potentially on the dashboard.

    // 'use client'; // Only if interactivity or client-side hooks are needed directly within this card.
                   // Could be a Server Component if actions are passed as props from a Client Component parent.

    import { Card, CardHeader, CardTitle, CardContent, CardFooter } from '@/components/ui/card';
    import { Button } from '@/components/ui/button';
    import { Badge } from '@/components/ui/badge'; // Assuming shadcn/ui Badge
    import { formatCurrency, formatDate } from '@/lib/utils'; // Assumed utility functions
    import type { Deal } from '@/types/deals'; // Assuming a Deal type definition

    interface DealCardProps {
      deal: Deal;
      onViewDetails?: (id: string) => void;
      onEdit?: (id: string) => void;
    }

    export function DealCard({ deal, onViewDetails, onEdit }: DealCardProps) {
      return (
        <Card className="deal-card w-full">
          <CardHeader>
            <div className="flex justify-between items-start">
              <CardTitle>{deal.brand_name}</CardTitle> {/* Using brand_name from PRD data model */}
              <Badge variant={deal.status === 'active' ? 'default' : 'secondary'}>
                {deal.status}
              </Badge>
            </div>
            <p className="text-sm text-muted-foreground">{deal.description.substring(0, 100)}...</p>
          </CardHeader>
          <CardContent>
            <div className="grid grid-cols-2 gap-2 text-sm">
              <div>
                <p className="text-muted-foreground">Value</p>
                <p>{formatCurrency(deal.value / 100, deal.currency)}</p> {/* Assuming value is in cents */}
              </div>
              <div>
                <p className="text-muted-foreground">End Date</p>
                <p>{deal.end_date ? formatDate(new Date(deal.end_date)) : 'N/A'}</p>
              </div>
              {/* Add more relevant summary details here */}
            </div>
          </CardContent>
          <CardFooter className="flex justify-end gap-2">
            {onEdit && (
              <Button variant="outline" size="sm" onClick={() => onEdit(deal.id)}>
                Edit
              </Button>
            )}
            {onViewDetails && (
              <Button size="sm" onClick={() => onViewDetails(deal.id)}>
                View Details
              </Button>
            )}
          </CardFooter>
        </Card>
      );
    }
=====

### 4.4 Key Components Specification (High-Level)

# (Refer to UX/UI Specification Section 6 for detailed component list and design system reference)

#### Authentication Components (`app/(auth)/components/` or `components/auth/`)

# - ****SignInForm****: Client Component using React Hook Form for email/password and Google Sign-In button.

- ****SignUpForm****: Client Component using React Hook Form.

- ****PasswordResetForm****: Client Component.

#### Deal Management Components (`app/(dashboard)/deals/components/`)

# - ****DealList****: Server Component for initial load, potentially with Client Components for filtering/sorting UI.

- ****DealCard****: Likely a Server Component if data is passed down, or Client Component if it has its own interactions.

- ****DealForm****: Client Component using React Hook Form.

- ****DeliverablesList/Item****: Client Components for managing deliverables within a deal.

#### Invoice Management Components (`app/(dashboard)/invoices/components/`)

# - ****InvoiceList****: Similar to DealList.

- ****InvoiceCard****: Similar to DealCard.

- ****InvoiceForm****: Client Component using React Hook Form.

#### Dashboard Components (`app/(dashboard)/components/` or feature-specific)

# - ****ActivityFeed****: Server Component, potentially with client-side updates via SWR.

- ****MetricsCards****: Server Component.

- ****UpcomingDeadlines****: Server Component.

#### Layout Components (`components/layout/`)

# - ****Header****: Client Component for interactive elements like user menu, notifications.

- ****Sidebar****: Can be Server or Client Component depending on dynamic content needs.

- ****MobileNav****: Client Component.

- ****Footer****: Likely a Server Component.

## 5. State Management In-Depth

### 5.1 State Management Strategy

# The application will use a combination of state management approaches as outlined in the Architecture Document:1) ****Server State****: Data fetched from Supabase (via Next.js API Routes or direct client calls where appropriate).

   - Managed primarily with ****SWR**** (or React Query) for data fetching, caching, revalidation, and optimistic updates.

   - Mutations (Create, Update, Delete) will be handled via calls to Next.js Server Actions or dedicated API routes, with SWR revalidating local cache upon success.

2) ****Client State (UI State)****:

   - ****React Context API****: For global UI state that needs to be shared across different parts of the application (e.g., authentication status/user object, theme preferences, global notifications/toasts).

   - ****`useState` / `useReducer`****: For local component state that doesn't need to be shared.

3) ****Form State****:

   - ****React Hook Form****: Chosen for its performance benefits, extensive validation capabilities (especially when paired with a schema validation library like Zod), and developer-friendly API for complex forms. Validation will be handled by ****Zod****, integrated with React Hook Form, to ensure data integrity and provide clear user feedback.

   - Simple forms might use controlled components with `useState`.

### 5.2 Store Structure (Context Examples)

#### Authentication Context (`lib/auth/AuthContext.tsx` or `contexts/AuthContext.tsx`)

    // /contexts/AuthContext.tsx
    'use client';

    import { createContext, useContext, useState, useEffect, ReactNode } from 'react';
    import { User as SupabaseUser } from '@supabase/supabase-js'; // Assuming Supabase user type
    import { supabase } from '@/lib/supabaseClient'; // Your Supabase client instance
    import type { UserProfile } from '@/types/user'; // Your custom user profile type

    interface AuthContextType {
      user: SupabaseUser | null;
      profile: UserProfile | null; // Additional user profile data from your public.users table
      isLoading: boolean;
      error: Error | null;
      // signIn, signUp, signOut methods would interact with Supabase
      signOut: () => Promise<void>;
    }

    const AuthContext = createContext<AuthContextType | undefined>(undefined);

    export function AuthProvider({ children }: { children: ReactNode }) {
      const [user, setUser] = useState<SupabaseUser | null>(null);
      const [profile, setProfile] = useState<UserProfile | null>(null);
      const [isLoading, setIsLoading] = useState(true);
      const [error, setError] = useState<Error | null>(null);

      useEffect(() => {
        const { data: authListener } = supabase.auth.onAuthStateChange(async (_event, session) => {
          setUser(session?.user ?? null);
          if (session?.user) {
            // Fetch user profile from your 'users' table
            const { data, error: profileError } = await supabase
              .from('users') // Ensure this matches your table name
              .select('*')
              .eq('id', session.user.id)
              .single();
            if (profileError) {
              console.error('Error fetching user profile:', profileError);
              setError(profileError);
            } else {
              setProfile(data as UserProfile);
            }
          } else {
            setProfile(null);
          }
          setIsLoading(false);
        });

        // Initial check
        const checkUser = async () => {
          const { data: { session } } = await supabase.auth.getSession();
          setUser(session?.user ?? null);
          if (session?.user) {
            const { data, error: profileError } = await supabase
              .from('users')
              .select('*')
              .eq('id', session.user.id)
              .single();
            if (profileError) console.error('Error fetching user profile on init:', profileError);
            else setProfile(data as UserProfile);
          }
          setIsLoading(false);
        };
        checkUser();

        return () => {
          authListener?.unsubscribe();
        };
      }, []);

      const signOut = async () => {
        setIsLoading(true);
        const { error: signOutError } = await supabase.auth.signOut();
        if (signOutError) {
          console.error('Error signing out:', signOutError);
          setError(signOutError);
        }
        setUser(null);
        setProfile(null);
        setIsLoading(false);
      };

      const value = { user, profile, isLoading, error, signOut };

      return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
    }

    export const useAuth = () => {
      const context = useContext(AuthContext);
      if (context === undefined) {
        throw new Error('useAuth must be used within an AuthProvider');
      }
      return context;
    };
======

#### SWR Usage for Deals (`hooks/useDeals.ts`)

    // /hooks/useDeals.ts
    import useSWR from 'swr';
    import type { Deal } from '@/types/deals'; // Your Deal type

    // Define a fetcher function that Next.js API routes or direct Supabase calls
    const fetcher = async (url: string): Promise<Deal[]> => {
      const res = await fetch(url);
      if (!res.ok) {
        const error = new Error('An error occurred while fetching the data.');
        // Attach extra info to the error object.
        // error.info = await res.json();
        // error.status = res.status;
        throw error;
      }
      return res.json();
    };

    export function useDeals(filters?: Record<string, any>) { // Add filters type
      // Construct query string from filters
      const queryString = filters ? new URLSearchParams(filters).toString() : '';
      const { data, error, isLoading, mutate } = useSWR<Deal[]>(`/api/deals?${queryString}`, fetcher);

      return {
        deals: data,
        isLoading,
        isError: error,
        mutateDeals: mutate,
      };
    }
=====

### 5.3 Selectors & Derived State

Custom hooks combining SWR/Context with `useMemo` will be used for derived state.    // /hooks/useFilteredDeals.ts (Example)
    import { useMemo } from 'react';
    import { useDeals } from '@/hooks/useDeals'; // Assuming useDeals hook from SWR example
    import type { Deal } from '@/types/deals';

    interface DealFilters {
      status?: string;
      // ... other filter properties
    }

    export function useFilteredDeals(filters: DealFilters) {
      const { deals, isLoading } = useDeals(); // Using the SWR-based hook

      return useMemo(() => {
        if (isLoading || !deals) return [];
        return deals.filter(deal => {
          let matches = true;
          if (filters.status && deal.status !== filters.status) {
            matches = false;
          }
          // Apply other filters
          return matches;
        });
      }, [deals, filters, isLoading]);
    }
=====

### 5.4 Actions/Reducers (for complex client state if needed)

If complex client-side state beyond SWR's scope (e.g., a multi-step UI wizard state not tied to server data) is required, `useReducer` with Context will be employed.    // /contexts/ComplexUIContext.tsx (Illustrative Example)
    'use client';
    import { createContext, useContext, useReducer, ReactNode } from 'react';

    interface State { /* ... */ }
    type Action = { type: 'ACTION_TYPE'; payload?: any };

    const initialState: State = { /* ... */ };

    function uiReducer(state: State, action: Action): State {
      switch (action.type) {
        // ... cases
        default:
          return state;
      }
    }

    interface ComplexUIContextType {
      state: State;
      dispatch: React.Dispatch<Action>;
    }

    const ComplexUIContext = createContext<ComplexUIContextType | undefined>(undefined);

    export function ComplexUIProvider({ children }: { children: ReactNode }) {
      const [state, dispatch] = useReducer(uiReducer, initialState);
      return (
        <ComplexUIContext.Provider value={{ state, dispatch }}>
          {children}
        </ComplexUIContext.Provider>
      );
    }

    export const useComplexUI = () => { /* ... */ };
====================================================

## 6. API Interaction Layer

### 6.1 Client/Service Structure

API interactions will be abstracted into service modules located in `lib/services/` or feature-specific service files. These will typically wrap `fetch` calls to Next.js API Routes or direct Supabase client calls.    // /lib/services/dealService.ts
    import type { Deal, CreateDealPayload, UpdateDealPayload } from '@/types/deals';
    import { supabase } from '@/lib/supabaseClient'; // Assuming direct Supabase client usage for some operations

    // Example using Next.js API Route
    export async function fetchDealsAPI(): Promise<Deal[]> {
      const response = await fetch('/api/deals'); // Assumes an API route at app/api/deals/route.ts
      if (!response.ok) throw new Error('Failed to fetch deals');
      return response.json();
    }

    // Example using Supabase client directly (alternative or complementary)
    export async function fetchDealsSupabase(): Promise<Deal[]> {
      const { data, error } = await supabase.from('deals').select('*');
      if (error) throw error;
      return data || [];
    }

    export async function createDealService(dealData: CreateDealPayload): Promise<Deal> {
      // Could use fetch to POST to /api/deals or direct Supabase call
      const { data, error } = await supabase.from('deals').insert(dealData).select().single();
      if (error) throw error;
      return data;
    }
    // ... other methods for update, delete
===========================================

### 6.2 Data Fetching Strategy

Primary data fetching will use SWR with the service functions.    // In a component or custom hook:
    // import useSWR from 'swr';
    // import { fetchDealsAPI } from '@/lib/services/dealService';
    // const { data: deals, error, isLoading } = useSWR<Deal[]>('/api/deals', fetchDealsAPI);Server Components will fetch data directly using `async/await` with service functions.
===================================================================================================================================================================================

### 6.3 Error Handling

# A custom hook `useApiError` (as shown in the original document) can be used in Client Components to manage and display API errors. Server Components and API routes will handle errors and return appropriate responses/log them.

### 6.4 Request/Response Interceptors

The `fetchWithInterceptor` approach is a good pattern for centralizing fetch logic, especially for adding auth headers and common error handling.    // /lib/apiClient.ts (Refined)
    import { supabase } from './supabaseClient'; // Assuming this is your configured Supabase client
    import Router from 'next/router'; // For client-side navigation

    const getAuthToken = async (): Promise<string | null> => {
      const { data: { session } } = await supabase.auth.getSession();
      return session?.access_token || null;
    };

    async function fetchWithInterceptor(url: string, options: RequestInit = {}) {
      const token = await getAuthToken();
      const headers = new Headers(options.headers || {});
      headers.set('Content-Type', 'application/json');
      if (token) {
        headers.set('Authorization', `Bearer ${token}`);
      }

      try {
        const response = await fetch(url, { ...options, headers });

        if (response.status === 401) {
          // Handle unauthorized: Redirect to sign-in
          // For client-side, use Next.js router. For server-side (API routes), this won't work directly.
          if (typeof window !== 'undefined') {
            Router.push('/sign-in?redirect=' + encodeURIComponent(window.location.pathname));
          }
          // Consider throwing a specific error that components can catch to trigger navigation
          // or that API routes can use to return a 401.
          throw new Error('Unauthorized');
        }

        if (!response.ok) {
          const errorData = await response.json().catch(() => ({ message: `HTTP error! status: ${response.status}` }));
          throw new Error(errorData.message || `API request failed with status ${response.status}`);
        }
        return response;
      } catch (error) {
        console.error('API Error:', url, error);
        throw error; // Re-throw to be caught by SWR or component error handling
      }
    }

    export const apiClient = {
      get: async <T>(url: string): Promise<T> => {
        const response = await fetchWithInterceptor(url);
        return response.json();
      },
      post: async <T>(url: string, data: any): Promise<T> => {
        const response = await fetchWithInterceptor(url, { method: 'POST', body: JSON.stringify(data) });
        return response.json();
      },
      // ... put, delete methods
    };
======

## 7. Routing Strategy

### 7.1 Route Definitions

The application will use Next.js App Router for routing:    /                       # Home/landing page
    /sign-in                # Sign in page
    /sign-up                # Sign up page
    /dashboard              # Main dashboard
    /deals                  # Deals list
    /deals/create           # Create new deal
    /deals/[id]             # Deal details
    /deals/[id]/edit        # Edit deal
    /invoices               # Invoices list
    /invoices/create        # Create new invoice
    /invoices/[id]          # Invoice details
    /invoices/[id]/edit     # Edit invoice
    /settings               # Settings landing
    /settings/account       # Account settings
    /settings/notifications # Notification settings
    /settings/branding      # Branding settings
    /settings/team          # Team management
=============================================

### 7.2 Route Guards & Protection

Route protection will be implemented using Next.js middleware:    // /middleware.ts
    import { NextResponse } from 'next/server';
    import type { NextRequest } from 'next/server';

    // Example using Supabase Auth Helpers for Next.js (recommended)
    // import { createMiddlewareClient } from '@supabase/auth-helpers-nextjs';

    export async function middleware(request: NextRequest) {
      const { pathname } = request.nextUrl;

      // Example with Supabase Auth Helpers:
      // const res = NextResponse.next();
      // const supabase = createMiddlewareClient({ req: request, res });
      // const { data: { session } } = await supabase.auth.getSession();
      // const isAuthenticated = !!session;

      // Placeholder for actual auth check logic:
      const isAuthenticated = request.cookies.has('auth-token'); // Replace with robust session check

      const protectedRoutes = [
        '/dashboard',
        '/deals',
        '/invoices',
        '/settings'
      ];

      const isProtectedRoute = protectedRoutes.some(route =>
        pathname === route || pathname.startsWith(`${route}/`)
      );

      if (isProtectedRoute && !isAuthenticated) {
        const url = new URL('/sign-in', request.url);
        url.searchParams.set('redirect', pathname);
        return NextResponse.redirect(url);
      }

      if ((pathname === '/sign-in' || pathname === '/sign-up') && isAuthenticated) {
        return NextResponse.redirect(new URL('/dashboard', request.url));
      }

      return NextResponse.next();
    }

    export const config = {
      matcher: [
        // Match all request paths except for the ones starting with:
        // - api (API routes)
        // - _next/static (static files)
        // - _next/image (image optimization files)
        // - favicon.ico (favicon file)
        '/((?!api|_next/static|_next/image|favicon.ico).*)',
      ],
    };(Note: The `request.cookies.has('auth-token')` check is a placeholder. It will likely be implemented using ****Supabase Auth Helpers for Next.js**** (e.g., `createClient` from `@supabase/ssr`) to reliably manage session state across server components, client components, and middleware.)
=====================================================================================================================================================================================================================================================================================================

### 7.3 Navigation Components

Navigation will be implemented with Next.js `Link` component and custom navigation components:    // /components/layout/Navigation.tsx
    'use client';

    import { usePathname } from 'next/navigation';
    import Link from 'next/link';
    import { Home, Briefcase, FileText, Settings as SettingsIcon } from 'lucide-react'; // Example icons

    interface NavItem {
      label: string;
      href: string;
      icon: React.ReactNode;
    }

    const mainNavItems: NavItem[] = [
      { label: 'Dashboard', href: '/dashboard', icon: <Home size={18} /> },
      { label: 'Deals', href: '/deals', icon: <Briefcase size={18} /> },
      { label: 'Invoices', href: '/invoices', icon: <FileText size={18} /> },
      { label: 'Settings', href: '/settings', icon: <SettingsIcon size={18} /> },
    ];

    export function Navigation() { // Removed items prop, using mainNavItems directly
      const pathname = usePathname();

      return (
        <nav className="space-y-1">
          {mainNavItems.map((item) => {
            const isActive = pathname === item.href || pathname.startsWith(`${item.href}/`);

            return (
              <Link
                key={item.href}
                href={item.href}
                className={`flex items-center px-4 py-2 text-sm font-medium rounded-md ${
                  isActive
                    ? 'bg-primary text-primary-foreground'
                    : 'text-muted-foreground hover:bg-accent hover:text-accent-foreground'
                }`}
              >
                <span className="mr-3">{item.icon}</span>
                {item.label}
              </Link>
            );
          })}
        </nav>
      );
    }
=====

## 8. Build/Bundling/Deployment

### 8.1 Build Configuration

The application will use the Next.js build system. The `next.config.js` (or `next.config.mjs`) file will be configured as needed.    // next.config.js
    /** @type {import('next').NextConfig} */
    const nextConfig = {
      reactStrictMode: true,
      swcMinify: true,
      images: {
        // Add domains for external images if used, e.g., Supabase Storage
        // domains: ['your-supabase-project-id.supabase.co'],
      },
      experimental: {
        serverActions: true, // Enable if using Next.js Server Actions
      },
      env: {
        // Public environment variables (available on client and server)
        NEXT_PUBLIC_SUPABASE_URL: process.env.NEXT_PUBLIC_SUPABASE_URL,
        NEXT_PUBLIC_SUPABASE_ANON_KEY: process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY,
        // NEXT_PUBLIC_API_URL: process.env.NEXT_PUBLIC_API_URL, // If using a separate API base
      },
      // Server-only environment variables are accessed directly via process.env in server-side code
    };

    module.exports = nextConfig;
================================

### 8.2 Environment Configuration

Environment variables will be managed using `.env` files (e.g., `.env.local` for development, Vercel environment variables for deployment).    # .env.example
    NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
    NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key

    # For Server-side Supabase client (if needed, e.g., in API routes or Server Actions)
    SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key
============================================================

### 8.3 Optimization Strategies

# - ****Code Splitting****: Leveraging Next.js automatic code splitting per page and dynamic imports (`next/dynamic`) for components loaded conditionally or below the fold.

- ****Image Optimization****: Utilizing the `next/image` component for responsive images, lazy loading, and optimization (format conversion, resizing).

- ****Font Optimization****: Using `next/font` for optimizing local or Google fonts, enabling automatic self-hosting and reducing layout shifts.

- ****Bundle Analysis****: Periodically using `@next/bundle-analyzer` to inspect JavaScript bundle sizes and identify opportunities for optimization.

- ****Tree Shaking****: Ensuring code is structured to allow for effective tree shaking by the bundler.

- ****Caching****: Implementing appropriate caching strategies at various levels (CDN, Next.js Data Cache for Server Components, SWR/React Query for client-side).

### 8.4 Deployment Pipeline

# - ****CI/CD****: GitHub Actions for continuous integration and deployment.

- ****Environments****:

  - ****Development****: Local development environment.

  - ****Preview****: Vercel automatically creates preview deployments for each pull request.

  - ****Staging****: A dedicated staging environment (e.g., `staging.cdh.app`) deployed from a `develop` or `staging` branch.

  - ****Production****: Live application (e.g., `cdh.app`) deployed from the `main` branch after successful testing and approvals.

- ****Deployment Platform****: Vercel is the primary hosting and deployment platform, leveraging its integration with Next.js.

## 9. Frontend Testing Strategy

### 9.1 Testing Approach

# The application will use a comprehensive testing pyramid approach:* ****Unit Tests****: Focus on individual functions, hooks, and simple UI components in isolation. Aim for high coverage of utility functions and business logic within hooks.

* ****Integration Tests****: Test interactions between several components, or components with their hooks and context providers. Verify that data flows correctly and UI updates as expected.

* ****End-to-End (E2E) Tests****: Test complete user flows through the application, simulating real user scenarios from the browser.

### 9.2 Testing Tools

# - ****Jest****: As the primary test runner.

- ****React Testing Library****: For rendering components and interacting with them in unit and integration tests, promoting tests that resemble how users interact with the application.

- ****Cypress**** (or Playwright): For E2E tests, allowing for browser automation and testing critical user journeys.

- ****MSW (Mock Service Worker)****: For mocking API requests (Supabase calls, Next.js API routes) during testing to ensure reliable and fast tests without external dependencies.

### 9.3 Test Organization

    /__tests__/                # Root test directory (alternative: co-locate tests with components)
      /components/            # Component tests (unit/integration)
        /ui/
          Button.test.tsx
        /deals/
          DealCard.test.tsx
      /hooks/                 # Hook tests
        useDeals.test.ts
      /pages/                 # Page-level integration tests (testing composition of components on a page)
        dealsPage.test.tsx
      /utils/                 # Utility function tests
        formatCurrency.test.ts
    /cypress/                 # Cypress E2E tests
      /e2e/                   # E2E test specs
        auth.cy.ts
        deals.cy.ts
      /fixtures/              # Test data for E2E tests
        user.json
      /support/               # Support files and custom commands for Cypress
        commands.ts
        e2e.ts__(Alternatively, tests can be co-located with the source files, e.g., `MyComponent.test.tsx` next to `MyComponent.tsx`)__
========================================================================================================================================

### 9.4 Testing Examples

#### Component Test (React Testing Library & Jest)

    // /components/ui/Button.test.tsx
    import { render, screen, fireEvent } from '@testing-library/react';
    import { Button } from '@/components/ui/button'; // Assuming Button is a shadcn/ui component

    describe('Button', () => {
      it('renders correctly with children', () => {
        render(<Button>Click me</Button>);
        expect(screen.getByRole('button', { name: /click me/i })).toBeInTheDocument();
      });

      it('calls onClick handler when clicked', () => {
        const handleClick = jest.fn();
        render(<Button onClick={handleClick}>Click me</Button>);
        fireEvent.click(screen.getByRole('button', { name: /click me/i }));
        expect(handleClick).toHaveBeenCalledTimes(1);
      });

      it('is disabled when the disabled prop is true', () => {
        render(<Button disabled>Click me</Button>);
        expect(screen.getByRole('button', { name: /click me/i })).toBeDisabled();
      });
    });
=======

#### Hook Test (React Testing Library & Jest)

    // /hooks/useAuth.test.ts (Simplified example, assuming useAuth is more complex)
    import { renderHook, act } from '@testing-library/react';
    // Mock Supabase client if useAuth directly interacts with it
    // jest.mock('@/lib/supabaseClient');
    // import { useAuth } from '@/hooks/useAuth';

    // Example for a simpler hook, actual useAuth would need more involved mocking
    const useCounter = () => {
      const [count, setCount] = React.useState(0);
      const increment = () => setCount(c => c + 1);
      return { count, increment };
    }

    describe('useCounter (example hook)', () => {
      it('should increment count', () => {
        const { result } = renderHook(() => useCounter());
        expect(result.current.count).toBe(0);
        act(() => {
          result.current.increment();
        });
        expect(result.current.count).toBe(1);
      });
    });
=======

## 10. Accessibility Implementation Details

### 10.1 Accessibility Standards

# The application will strive to comply with ****WCAG 2.1 AA**** standards:* ****Perceivable****: Information and UI components must be presentable to users in ways they can perceive.

* ****Operable****: UI components and navigation must be operable.

* ****Understandable****: Information and operation of the UI must be understandable.

* ****Robust****: Content must be robust enough to be interpreted reliably by a wide variety of user agents, including assistive technologies.

### 10.2 Implementation Approach

#### Semantic HTML

Use appropriate HTML5 elements to convey structure and meaning.    <article aria-labelledby="deal-title">
      <h2 id="deal-title">Deal Title</h2>
      <p>Deal description</p>
      <footer>
        <p>Status: <time dateTime="2023-07-15">July 15, 2023</time></p>
      </footer>
    </article>
==============

#### ARIA Attributes

Leverage ARIA attributes where semantic HTML is insufficient, especially for custom components or dynamic content updates. shadcn/ui components generally have good ARIA support.    // Example of ARIA attributes for a custom modal
    <div role="dialog" aria-modal="true" aria-labelledby="dialogTitle">
      <h2 id="dialogTitle">Dialog Title</h2>
      {/* ...modal content... */}
      <button aria-label="Close dialog" onClick={handleClose}>&times;</button>
    </div>
==========

#### Keyboard Navigation

# - Ensure all interactive elements are focusable and operable via keyboard.

- Maintain a logical tab order.

- Provide clear visual focus indicators (Tailwind CSS `focus:ring` utilities will be used).

#### Accessibility Testing

# - ****Automated Testing****: Integrate tools like `axe-core` with Jest/React Testing Library (`@axe-core/react`).

- ****Manual Testing****: Regularly test with screen readers (NVDA, VoiceOver, JAWS) and keyboard-only navigation.

- ****Contrast Checking****: Use tools to ensure color contrast meets WCAG AA requirements.

## 11. Performance Considerations

### 11.1 Performance Metrics

# Target Core Web Vitals:* ****Largest Contentful Paint (LCP)****: < 2.5 seconds

* ****First Input Delay (FID)**** / ****Interaction to Next Paint (INP)****: < 100ms (FID) / < 200ms (INP 'good')

* ****Cumulative Layout Shift (CLS)****: < 0.1

### 11.2 Optimization Techniques

#### Image Optimization

    // Using Next.js Image component
    import Image from 'next/image';

    export function OptimizedImage({ src, alt }: { src: string; alt: string }) {
      return (
        <Image
          src={src}
          alt={alt}
          width={500} // Example, set appropriately
          height={300} // Example, set appropriately
          // placeholder="blur" // If using blurDataURL
          // blurDataURL="data:image/..."
          priority={false} // Set to true for LCP images
        />
      );
    }
=====

#### Code Splitting (Dynamic Imports)

    // Using dynamic imports for components not needed on initial load
    import dynamic from 'next/dynamic';

    const HeavyComponent = dynamic(() => import('@/components/HeavyComponent'), {
      loading: () => <p>Loading component...</p>,
      ssr: false, // If the component is client-side only
    });
=======

#### Memoization

    import React, { memo, useMemo } from 'react';

    interface Item { id: string; value: number; }
    interface ExpensiveComponentProps { data: Item[] }

    // Assume processItem is a computationally intensive function
    const processItem = (item: Item) => ({ ...item, processedValue: item.value * 2 });

    const ExpensiveInternalComponent = memo(function ExpensiveInternalComponent({ data }: ExpensiveComponentProps) {
      // Simulate expensive rendering
      console.log('Rendering ExpensiveInternalComponent');
      return (
        <ul>
          {data.map(item => <li key={item.id}>{item.id}: {item.processedValue}</li>)}
        </ul>
      );
    });

    export function ParentComponent({ items }: { items: Item[] }) {
      const processedItems = useMemo(() => {
        return items.map(item => processItem(item));
      }, [items]); // Only recompute if items array reference changes

      return <ExpensiveInternalComponent data={processedItems} />;
    }
=====

### 11.3 Lazy Loading

# For off-screen images and components, native browser lazy loading (`loading="lazy"` for `<img>`) or Intersection Observer API can be used, often handled by `next/image` or dynamic imports.

## 12. Internationalization/Localization Strategy

### 12.1 I18n Implementation

The application will use `next-intl` for internationalization, allowing for easy management of translations and locale-specific content.* ****Message Files****: Translations will be stored in JSON files per locale (e.g., `/messages/en.json`, `/messages/es.json`).    // /messages/en.json
    {
      "common": {
        "welcome": "Welcome to Creator's Deal Hub",
        "signIn": "Sign In",
        "signUp": "Sign Up"
      },
      "deals": {
        "title": "Deals",
        "create": "Create Deal",
        "status": {
          "draft": "Draft",
          "active": "Active",
          "completed": "Completed"
        }
      }
    }* ****Provider Setup****: The `NextIntlClientProvider` will be used in the root layout to make messages available throughout the application.    // /app/[locale]/layout.tsx
    import { NextIntlClientProvider } from 'next-intl';
    import { getMessages } from 'next-intl/server';

    export default async function LocaleLayout({
      children,
      params: { locale }
    }: {
      children: React.ReactNode;
      params: { locale: string };
    }) {
      const messages = await getMessages();

      return (
        <html lang={locale}>
          <body>
            <NextIntlClientProvider locale={locale} messages={messages}>
              {children}
            </NextIntlClientProvider>
          </body>
        </html>
      );
    }* ****Usage in Components****: The `useTranslations` hook will be used to access translated strings.    // Usage in components
    'use client';
    import { useTranslations } from 'next-intl';

    export function DealStatus({ status }: { status: 'draft' | 'active' | 'completed' }) {
      const t = useTranslations('deals.status');
      return <span>{t(status)}</span>;
    }
=====

### 12.2 Date & Number Formatting

`next-intl` also provides hooks for formatting dates, numbers, and currencies according to the active locale.    // Date formatting
    import { useFormatter } from 'next-intl';

    export function FormattedDate({ date }: { date: Date }) {
      const format = useFormatter();
      return (
        <time dateTime={date.toISOString()}>
          {format.dateTime(date, { dateStyle: 'medium' })}
        </time>
      );
    }

    // Number formatting
    export function FormattedCurrency({ amount, currency = 'USD' }: { amount: number; currency?: string }) {
      const format = useFormatter();
      return (
        <span>
          {format.number(amount / 100, { // Assuming amount is in cents
            style: 'currency',
            currency
          })}
        </span>
      );
    }
=====

### 12.3 RTL Support

The application will support Right-to-Left (RTL) languages.* The `dir` attribute on the `<html>` tag will be set based on the locale.

* Tailwind CSS's logical properties (e.g., `ms-2` for `margin-start` instead of `ml-2`) will be used to ensure layouts adapt correctly for RTL.    // /app/[locale]/layout.tsx (RTL part)
    const rtlLocales = ['ar', 'he']; // Example RTL locales
    // ...
    const isRtl = rtlLocales.includes(locale);

    return (
      <html lang={locale} dir={isRtl ? 'rtl' : 'ltr'}>
        {/* ... */}
      </html>
    );
======

## 13. Feature Flag Management

### 13.1 Feature Flag Implementation

A simple feature flag mechanism will be implemented, potentially fetching flags from an API or environment variables, with a client-side utility to check if a feature is enabled. For MVP, this might be a simple object, expandable later.    // /lib/featureFlags.ts
    export type FeatureFlag = 'teamManagement' | 'advancedInvoicing' | 'analyticsDashboard';

    interface FeatureFlagsConfig {
      [key: string]: boolean;
    }

    // Default flags, could be overridden by environment variables or a remote config
    const featureFlagsConfig: FeatureFlagsConfig = {
      teamManagement: process.env.NEXT_PUBLIC_FF_TEAM_MANAGEMENT === 'true' || false,
      advancedInvoicing: process.env.NEXT_PUBLIC_FF_ADVANCED_INVOICING === 'true' || false,
      analyticsDashboard: process.env.NEXT_PUBLIC_FF_ANALYTICS_DASHBOARD === 'true' || false,
    };

    export function isFeatureEnabled(feature: FeatureFlag): boolean {
      return featureFlagsConfig[feature] === true;
    }

    // Example of how flags might be initialized or fetched in a real app
    // export async function loadFeatureFlags(): Promise<FeatureFlagsConfig> {
    //   // Fetch from a remote service or use environment variables
    //   return { ...defaultFlags, ...fetchedFlags };
    // }
========

### 13.2 Feature Flag Usage

Components will conditionally render features based on these flags.    // Usage in a component
    'use client';
    import { isFeatureEnabled } from '@/lib/featureFlags';

    export function DashboardFeatures() {
      const analyticsEnabled = isFeatureEnabled('analyticsDashboard');

      return (
        <div>
          <h2>Dashboard</h2>
          {analyticsEnabled && (
            <section>
              <h3>Analytics Overview</h3>
              {/* Analytics content */}
            </section>
          )}
          {/* Other dashboard content */}
        </div>
      );
    }
=====

## 14. Frontend Security Considerations

### 14.1 XSS Prevention

- ****React's Built-in Escaping****: React automatically escapes content rendered in JSX, which mitigates most XSS risks from dynamic data.

- ****`dangerouslySetInnerHTML`****: Avoid its use. If absolutely necessary (e.g., rendering sanitized HTML from a trusted CMS), ensure the HTML is rigorously sanitized using a library like DOMPurify on the client-side before rendering.

- ****Content Security Policy (CSP)****: Implement a strict CSP via `next.config.js` headers to control which resources (scripts, styles, images, etc.) can be loaded, reducing the impact of any potential XSS.

      // next.config.js
      const securityHeaders = [
        {
          key: 'Content-Security-Policy',
          value: "default-src 'self'; script-src 'self' 'unsafe-eval' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data: your-cdn.com; font-src 'self'; connect-src 'self' your-api.supabase.co; frame-src 'self';"
          // Adjust 'unsafe-eval' and 'unsafe-inline' as much as possible.
          // 'unsafe-eval' might be needed by some client-side libraries or for performance in specific cases.
          // 'unsafe-inline' for styles might be needed if not using a strict CSP-compatible styling solution.
          // Add Supabase URLs to connect-src if using direct client-side SDK calls.
        }
        // ... other security headers like X-Content-Type-Options, X-Frame-Options, etc.
      ]
      module.exports = {
        async headers() {
          return [
            {
              source: '/:path*',
              headers: securityHeaders,
            },
          ]
        },
        // ... other nextConfig
      }

- ****Input Sanitization****: While React escapes output, always validate and sanitize user input on the server-side (API routes, Server Actions) before storing or processing it, especially if it might be reflected back to any client.
==========================================================================================================================================================================================================================================

### 14.2 CSRF Protection

- ****Next.js API Routes/Server Actions****:

  - For traditional API routes handling state-changing operations (POST, PUT, DELETE), implement CSRF protection. One common method is the Double Submit Cookie pattern:

    1. On user login or page load that includes a form, generate a CSRF token on the server, store it in an HttpOnly, SameSite=Lax/Strict cookie, and also send it to the client (e.g., in a meta tag or initial page data).

    2. For subsequent state-changing requests, the client includes this token in a custom HTTP header (e.g., `X-CSRF-Token`).

    3. The server validates that the token in the header matches the one associated with the user's session (or the one in the cookie if using stateless CSRF tokens).

  - Next.js Server Actions have built-in CSRF protection mechanisms when used correctly (typically for form submissions). Ensure these are understood and leveraged.

  - Supabase client libraries handle auth tokens securely, which also helps mitigate CSRF for direct Supabase operations if properly configured with RLS.

- ****SameSite Cookies****: Use `SameSite=Lax` or `SameSite=Strict` for session cookies to provide a baseline level of CSRF protection. Supabase Auth Helpers often configure this.    // Example: Custom header for CSRF token in a fetch call
    // Assume getCsrfToken() retrieves the token from a meta tag or JavaScript variable
    async function submitFormWithCsrf(formData: FormData) {
      const getCsrfToken = (): string | null => {
        if (typeof document !== 'undefined') {
          return document.querySelector('meta[name="csrf-token"]')?.getAttribute('content');
        }
        return null;
      };
      const csrfToken = getCsrfToken();

      const response = await fetch('/api/submit-data', { // Your API endpoint
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'X-CSRF-Token': csrfToken || '', // Custom header
        },
        body: JSON.stringify(Object.fromEntries(formData)),
      });
      return response.json();
    }
=====

### 14.3 Secure Data Storage (Client-Side)

- ****`localStorage` / `sessionStorage`****:

  - Avoid storing sensitive information like JWTs, API keys, or unencrypted PII in `localStorage` as it's vulnerable to XSS attacks. `sessionStorage` is slightly better as it's cleared when the tab closes but still susceptible to XSS within that session.

  - Supabase client library typically manages auth tokens securely, often using `localStorage` but with its own mechanisms. Rely on the library's secure defaults.

  - If storing user preferences or non-sensitive UI state, `localStorage` can be used, but be mindful of XSS.

- ****HttpOnly Cookies****: For session tokens or CSRF tokens managed by the server, use `HttpOnly` cookies to prevent JavaScript access. This is a server-side configuration.

- ****Encryption****: For any client-side storage of potentially sensitive application data (beyond what Supabase handles), consider encrypting it first, though robust client-side encryption is complex. The primary defense is not to store sensitive data on the client if avoidable.    // Example: Secure storage utility (conceptual, for non-sensitive data)
    // For sensitive data, rely on Supabase's secure token handling.
    const appStorage = {
      setItem(key: string, value: string): void {
        try {
          // For non-sensitive UI preferences or cached data
          if (typeof window !== 'undefined') {
            localStorage.setItem(key, value);
          }
        } catch (error) {
          console.error('Error storing data in localStorage:', error);
        }
      },
      getItem(key: string): string | null {
        try {
          if (typeof window !== 'undefined') {
            return localStorage.getItem(key);
          }
          return null;
        } catch (error) {
          console.error('Error retrieving data from localStorage:', error);
          return null;
        }
      },
      removeItem(key: string): void {
        try {
          if (typeof window !== 'undefined') {
            localStorage.removeItem(key);
          }
        } catch (error) {
          console.error('Error removing data from localStorage:', error);
        }
      }
    };
======

## 15. Browser Support

### 15.1 Supported Browsers

# The application will aim to support the latest two major versions of the following browsers:* Chrome

* Firefox

* Safari

* Edge

* iOS Safari

* Android ChromeSupport for older browsers or Internet Explorer is not a primary goal for the MVP.

### 15.2 Polyfill Strategy

Next.js automatically provides polyfills for many modern JavaScript features for older browser compatibility.* ****Core-js****: Next.js includes core-js polyfills based on browser targets.

* ****Fetch API****: `whatwg-fetch` is polyfilled by Next.js for client-side.

* Custom Polyfills: If specific, non-standard APIs are used or support for very old browsers is unexpectedly required, polyfills will be added selectively. The example webpack modification in next.config.js for stream-browserify and crypto-browserify is noted.

  (Note: Verify necessity of these specific polyfills during development. Next.js and modern browsers handle many features natively. Only add polyfills if a specific, unsupported browser API is used by a critical library.)    // Example in next.config.js if specific fallbacks are needed:
    // const nextConfig = {
    //   webpack: (config, { isServer, dev }) => {
    //     if (!isServer && !dev) { // Only for client-side production bundles
    //       config.resolve.fallback = {
    //         ...config.resolve.fallback,
    //         // Example: stream: require.resolve('stream-browserify'),
    //         // Example: crypto: require.resolve('crypto-browserify'),
    //       };
    //     }
    //     return config;
    //   },
    // };
=========

### 15.3 Feature Detection

Where necessary, feature detection will be used to provide fallbacks or alternative experiences for browsers that do not support certain modern APIs.    // Feature detection utility example
    export const browserFeatures = {
      hasWebPSupport: (): boolean => {
        if (typeof document === 'undefined') return false; // Server-side check
        const elem = document.createElement('canvas');
        if (elem.toDataURL && elem.toDataURL('image/webp').indexOf('data:image/webp') === 0) {
          return true; // WebP is supported
        }
        return false;
      },
      hasIntersectionObserver: (): boolean => {
        return typeof IntersectionObserver !== 'undefined';
      },
      hasLocalStorage: (): boolean => {
        try {
          if (typeof localStorage !== 'undefined') {
            localStorage.setItem('__feature_test__', 'test');
            localStorage.removeItem('__feature_test__');
            return true;
          }
          return false;
        } catch (e) {
          return false;
        }
      },
    };

    // Usage in a component:
    // if (browserFeatures.hasWebPSupport()) { /* Use WebP */ }
===============================================================

## 16. Change Log

# |             |            |                  |                                                                                                                                                                                                       |
| ----------- | ---------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Version** | **Date**   | **Author**       | **Description**                                                                                                                                                                                       |
| 0.1         | 2023-07-10 | Millie (Initial) | Initial draft (as provided by user)                                                                                                                                                                   |
| 1.0         | 2025-06-02 | Millie (BMAD)    | Updated meta, paths, added Atomic Design examples, clarified CSS naming, RHF rationale + Zod, refined 401 redirect, noted Supabase Auth Helpers for middleware, and added polyfill verification note. |
| 1.1         | 2025-06-02 | Millie (BMAD)    | Expanded Section 14 (Frontend Security Considerations) with detailed content for XSS, CSRF, and Secure Data Storage. Updated version number.                                                          |
| 1.2         | 2025-06-02 | Millie (BMAD)    | Expanded Sections 12, 13, and 15 to include full details, removing "(As defined in the original document)" placeholders. Updated version number.                                                      |

##
