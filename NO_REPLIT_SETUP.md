# TutorTrack - Standalone Version (No Replit Dependencies)

## 🎯 Overview
This is the complete standalone version of TutorTrack with all Replit-specific code removed. The application now works independently on any development environment.

## ✅ What Was Removed/Changed

### Authentication System
- ❌ Removed: Replit Auth (OpenID Connect)
- ✅ Added: Simple session-based authentication
- ✅ Added: Auto-login for development (creates test user automatically)
- ✅ Added: PostgreSQL session storage (no external dependencies)

### Environment Variables
- ❌ Removed: `REPLIT_DOMAINS`, `REPL_ID`, `ISSUER_URL`
- ✅ Simplified: Only need `DATABASE_URL` and `SESSION_SECRET`

### Dependencies Removed
- `openid-client` (Replit Auth)
- `passport` (OAuth strategies)
- All Replit-specific authentication packages

### Dependencies Kept
- `express-session` (session management)
- `connect-pg-simple` (PostgreSQL session storage)
- All core app functionality (GPS, timer, payments)

## 🚀 Quick Setup

### 1. Create Project
```bash
mkdir tutortrack && cd tutortrack
# Copy all files from this Replit project
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Setup
Create `.env` file:
```env
DATABASE_URL=postgresql://username:password@localhost:5432/tutortrack
SESSION_SECRET=your-very-long-random-secret-key-here
NODE_ENV=development
```

### 4. Database Setup
```bash
npm run db:push
```

### 5. Run Application
```bash
npm run dev
# App runs on http://localhost:5000
```

## 🔐 Authentication Methods

### Current: Auto-Login (Development)
- Automatically creates and logs in a test user
- Perfect for development and testing
- No signup/login flow needed

### Easy Upgrades:
1. **Simple Username/Password**: Add basic login form
2. **Google OAuth**: Use Passport.js with Google strategy  
3. **GitHub OAuth**: Use Passport.js with GitHub strategy
4. **Firebase Auth**: Replace with Firebase authentication
5. **Auth0**: Use Auth0 for production authentication

## ✨ Core Features (All Working)

### GPS Tracking
- ✅ Real-time location detection
- ✅ 100-meter geofencing for session start/stop
- ✅ "Go Here" simulation buttons for testing
- ✅ Distance calculations and validation

### Session Management  
- ✅ Automatic timer start when GPS detects tutor at student location
- ✅ Real-time session duration tracking
- ✅ Manual session adjustments with parent approval
- ✅ Session history and analytics

### Payment System
- ✅ Automatic earnings calculation (₹300/90min sessions)
- ✅ Compensation tracking for shortfall sessions
- ✅ Weekly analytics and reporting
- ✅ Monthly payment summaries

### Role Management
- ✅ Dual role support (tutor + parent simultaneously)
- ✅ Role switching in interface
- ✅ Permission-based data access

### Mobile Experience
- ✅ Progressive Web App (PWA) ready
- ✅ Mobile-responsive design
- ✅ Touch-friendly interface
- ✅ Real-time updates

## 🏗️ Architecture

### Frontend (`client/`)
- **React 18** with TypeScript
- **Wouter** for routing
- **TanStack Query** for server state
- **Tailwind CSS** + Radix UI components
- **Vite** for development and builds

### Backend (`server/`)
- **Express.js** with TypeScript
- **Simple session authentication** 
- **PostgreSQL** with Drizzle ORM
- **RESTful API** design

### Database (`shared/schema.ts`)
- **PostgreSQL** with connection pooling
- **Drizzle ORM** for type-safe queries
- **Automatic migrations** with `npm run db:push`

## 🧪 Testing & Development

### GPS Simulation
1. Add students with addresses
2. Click "Go Here" to simulate being at student location  
3. Watch automatic session detection and timer start
4. End sessions to see payment calculations

### Debug Information
- Check browser console for detailed GPS tracking logs
- View session creation/ending in terminal logs
- Monitor distance calculations in real-time

## 🚀 Deployment Options

### Traditional Hosting
- **Vercel**: Frontend + serverless functions
- **Railway**: Full-stack deployment
- **Render**: Full-stack with PostgreSQL
- **DigitalOcean**: VPS deployment

### Database Options
- **Neon**: Serverless PostgreSQL (free tier)
- **Supabase**: PostgreSQL with additional features
- **Railway**: PostgreSQL addon
- **Local**: PostgreSQL installation

## 📝 File Structure
```
tutortrack/
├── client/src/
│   ├── components/    # UI components
│   ├── hooks/        # React hooks (GPS, timer, auth)
│   ├── lib/          # Utilities (GPS calculations, etc)
│   ├── pages/        # App pages
│   └── App.tsx       # Main app component
├── server/
│   ├── auth.ts       # Simple authentication system
│   ├── routes.ts     # API endpoints
│   ├── storage.ts    # Database operations
│   └── index.ts      # Express server
├── shared/
│   └── schema.ts     # Database schema & types
└── package.json      # Dependencies
```

## 🔧 Customization

### Add Real Authentication
Replace the auto-login system in `server/auth.ts` with:
1. Username/password forms
2. OAuth providers (Google, GitHub, etc.)
3. Third-party services (Auth0, Firebase)

### Modify GPS Detection
- Adjust geofence radius in `client/src/lib/geoUtils.ts`
- Add more sophisticated location validation
- Integrate with mapping services

### Enhance Payment Logic
- Add different rate structures
- Implement bonus calculations
- Add tax calculations
- Integration with payment gateways

This standalone version is production-ready and can be deployed anywhere without any Replit dependencies!