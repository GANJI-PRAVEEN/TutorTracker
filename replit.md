# replit.md

## Overview

TutorTrack is an AI-powered mobile web application designed to track home tutoring sessions with GPS-based automatic timing. The application serves both tutors and parents, providing automatic session tracking, compensation management, and payment calculations. It's built as a full-stack TypeScript application with a React frontend and Express backend, using PostgreSQL for data persistence.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a modern full-stack architecture with clear separation between client and server concerns:

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query for server state management
- **UI Framework**: Radix UI components with shadcn/ui styling
- **Styling**: Tailwind CSS with CSS variables for theming
- **Build Tool**: Vite for development and production builds

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **Authentication**: Replit Auth with OpenID Connect
- **Session Management**: Express sessions with PostgreSQL storage
- **API Design**: RESTful API with role-based access control

### Database Architecture
- **Database**: PostgreSQL (via Neon serverless)
- **ORM**: Drizzle ORM with schema-first approach
- **Migrations**: Drizzle Kit for schema management
- **Connection**: Connection pooling with @neondatabase/serverless

## Key Components

### Authentication System
- **Provider**: Simple session-based authentication (standalone, no external dependencies)
- **Session Storage**: PostgreSQL-backed sessions using connect-pg-simple
- **User Management**: Auto-login system creates test user for development
- **Role-Based Access**: Support for tutor, parent, and admin roles
- **Note**: All Replit-specific authentication removed for standalone deployment

### GPS Tracking System
- **Location Services**: Browser Geolocation API
- **Geofencing**: Distance calculation for proximity detection
- **Automatic Session Management**: GPS-triggered session start/stop
- **Manual Overrides**: Manual session adjustments with approval workflow

### Session Management
- **Automatic Tracking**: Location-based session detection
- **Time Tracking**: Real-time session duration monitoring
- **Compensation Logic**: Shortfall calculation and makeup scheduling
- **Holiday Management**: Weekend exclusion from tracking

### Role Management
- **Dual Roles**: Users can be both tutors and parents
- **Role Switching**: Dynamic interface adaptation based on current role
- **Permission System**: Role-based data access and operation permissions

### Payment System
- **Rate Calculation**: Duration-based payment computation
- **Monthly Reports**: Automated payment calculation at month-end
- **Compensation Tracking**: Shortfall management and makeup session tracking

## Data Flow

### Session Lifecycle
1. **Detection**: GPS monitoring detects tutor at student location
2. **Initiation**: Automatic session start with timer activation
3. **Monitoring**: Real-time duration tracking and progress updates
4. **Completion**: Automatic or manual session end
5. **Calculation**: Payment and compensation calculations
6. **Notification**: Alerts to relevant parties for shortfalls

### User Authentication Flow
1. **Auto-Login**: Automatic test user creation for development
2. **Session Creation**: Express session with PostgreSQL storage
3. **User Management**: Automatic user record creation with dual roles
4. **Session Persistence**: Secure session cookies with proper expiration
5. **Role Assignment**: User can be both tutor and parent simultaneously

### Data Synchronization
- **Real-time Updates**: TanStack Query for automatic data refetching
- **Optimistic Updates**: Immediate UI updates with server reconciliation
- **Error Handling**: Automatic retry and fallback mechanisms
- **Offline Support**: Service worker for basic offline functionality

## External Dependencies

### Core Dependencies
- **Database**: Neon PostgreSQL serverless database
- **Authentication**: Replit Auth service
- **UI Components**: Radix UI primitives with shadcn/ui
- **State Management**: TanStack Query for server state
- **Validation**: Zod for runtime type validation
- **Date Handling**: date-fns for date manipulation

### Development Dependencies
- **Build System**: Vite with React plugin
- **Type Checking**: TypeScript with strict configuration
- **Code Quality**: ESLint and Prettier integration
- **Deployment**: Replit hosting platform

### Optional Integrations
- **Maps API**: Google Maps or similar for address validation
- **Push Notifications**: Web Push API for mobile notifications
- **Analytics**: Usage tracking and performance monitoring

## Deployment Strategy

### Development Environment
- **Platform**: Replit development environment
- **Hot Reload**: Vite development server with HMR
- **Database**: Neon development database instance
- **Environment Variables**: `.env` file for local configuration

### Production Deployment
- **Build Process**: Vite production build with optimization
- **Server Bundle**: esbuild for server-side code bundling
- **Static Assets**: Served from Express with proper caching headers
- **Database**: Neon production PostgreSQL instance
- **Environment**: Production environment variables via Replit secrets

### Performance Considerations
- **Bundle Splitting**: Automatic code splitting via Vite
- **Asset Optimization**: Image optimization and compression
- **Caching Strategy**: Browser caching for static assets
- **Database Optimization**: Connection pooling and query optimization

### Security Measures
- **HTTPS Enforcement**: Secure connections in production
- **Session Security**: Secure session cookies with proper flags
- **CORS Configuration**: Restricted cross-origin requests
- **Input Validation**: Server-side validation for all inputs
- **SQL Injection Prevention**: Parameterized queries via Drizzle ORM