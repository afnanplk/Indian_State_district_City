# App Kalyanam - Comprehensive Event & Wedding Management Platform

## What is this App For?
App Kalyanam is a complete end-to-end event and wedding management ecosystem designed to streamline the process of booking event spaces (auditoriums/banquet halls) and managing associated services (catering, decoration, photography, stage, and sound). 

It serves multiple types of users:
1. **Clients/Customers**: Can browse available event rooms, check availability, book rooms along with various services, and track their bookings and events.
2. **Superadmins/Platform Owners**: Have a birds-eye view of all bookings, revenue, expenses, and margins. They can assign tasks to team members and approve partner registrations.
3. **Partners (Auditorium Owners / Event Management)**: Third-party vendors who list their services or spaces on the platform.
4. **Team Members/Staff**: Internal staff organized by departments (food, catering, decoration, etc.) who receive assigned tasks for specific bookings and can log expenses.

## Architecture and Technology Stack
The project is built as a monorepo utilizing a modern, scalable tech stack:
- **Frontend**: Flutter (Mobile/Web) utilizing Riverpod for state management and GoRouter for declarative routing.
- **Backend**: Supabase (PostgreSQL) for authentication, database, Row Level Security (RLS), and file storage.

### Directory Structure
The repository is split into four primary components:
- `client_app/`: The customer-facing Flutter application.
- `admin_app/`: The internal Flutter application for admins, partners, and staff.
- `shared/`: A shared Dart package containing common UI widgets, routing logic, and shared state to prevent code duplication between the two apps.
- `supabase/`: Contains the backend configuration, primarily the database schema, RLS policies, and triggers.

---

## What We Have Done Till Now

### 1. Database & Backend Setup (Supabase)
- Designed a comprehensive, relational PostgreSQL schema (`schema.sql`).
- Created tables for:
  - **profiles**: Extending Supabase Auth with custom roles (client, superadmin, auditorium_owner, event_management), departments, and approval statuses.
  - **event_rooms & event_room_images**: To store auditorium details, pricing, capacities, and galleries.
  - **services**: Defining available add-on services (catering, decoration, etc.) with base prices.
  - **bookings & booking_services**: To handle the core transactional flow, capturing room price snapshots and attaching individual tasks/services to team members.
  - **payments & expenses**: To track incoming revenue (Razorpay integration) and internal departmental expenses.
- Created an **admin_billing_view** to automatically calculate revenue, total expenses, and net margin per booking.
- Implemented robust **Row Level Security (RLS) policies** ensuring:
  - Clients only see their own bookings and payments.
  - Team members only see their assigned tasks and logged expenses.
  - Admins have comprehensive access to manage the platform.
- Created a **database trigger** (`handle_new_user`) that automatically inserts a new profile row when a user signs up via Supabase Auth, properly setting default roles and putting partners into a 'pending' approval state.

### 2. Shared Library Setup
- Initialized a `shared` Dart package to act as the core dependency for both apps.
- Centralized the GoRouter configuration logic so both apps can share a consistent routing wrapper while defining their own specific routes.

### 3. Client Application Initialization
- Created the `client_app` Flutter project.
- Configured a warm, event-oriented theme (Gold accent).
- Integrated Supabase initialization using the project URL and Anon Key.
- Set up Riverpod and defined the core GoRoute structure:
  - Public routes: Login, Register.
  - Shell routes with a bottom navigation scaffold: Search, Browse (Home), Events, and Profile.
  - Dynamic routes: Booking Checkout.

### 4. Admin Application Initialization
- Created the `admin_app` Flutter project.
- Configured a corporate, internal-focused theme (Deep Slate).
- Integrated Supabase initialization.
- Set up Riverpod and defined the administrative GoRoute structure:
  - Auth flows including Unauthorized and Pending Approval screens for unverified partners.
  - Admin Dashboard for superadmins to view metrics.
  - Task Assignment routing for specific bookings.
  - A Team Tasks screen for staff members to manage their assigned work.
