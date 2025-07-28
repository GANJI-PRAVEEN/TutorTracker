# TutorTrack - Local Development Setup Guide

## Overview
TutorTrack is an AI-powered Progressive Web App for tracking home tutoring sessions with GPS-based automatic timing, payment calculations, and compensation management.

## Prerequisites
- Node.js 18+ and npm
- PostgreSQL database (local or cloud like Neon)
- Code editor (VS Code recommended)

## Quick Setup Steps

### 1. Create Project Structure
```bash
mkdir tutortrack
cd tutortrack
npm init -y
```

### 2. Install Dependencies
```bash
# Core dependencies
npm install express typescript tsx drizzle-orm drizzle-kit @neondatabase/serverless
npm install react react-dom wouter @tanstack/react-query zod drizzle-zod
npm install @radix-ui/react-slot @radix-ui/react-toast @radix-ui/react-dialog
npm install class-variance-authority clsx tailwind-merge lucide-react
npm install framer-motion date-fns

# Development dependencies
npm install -D vite @vitejs/plugin-react tailwindcss postcss autoprefixer
npm install -D @types/node @types/react @types/react-dom @types/express
npm install -D @tailwindcss/typography @tailwindcss/vite

# Authentication (if using Replit Auth)
npm install passport express-session connect-pg-simple openid-client
npm install -D @types/passport @types/express-session
```

### 3. Project Structure
Create these folders and files:
```
tutortrack/
├── client/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── pages/
│   │   ├── App.tsx
│   │   ├── index.css
│   │   └── main.tsx
│   └── index.html
├── server/
│   ├── db.ts
│   ├── index.ts
│   ├── routes.ts
│   ├── storage.ts
│   └── vite.ts
├── shared/
│   └── schema.ts
├── package.json
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── drizzle.config.ts
```

### 4. Environment Variables
Create `.env` file:
```env
DATABASE_URL=postgresql://username:password@localhost:5432/tutortrack
SESSION_SECRET=your-secret-key-here
NODE_ENV=development
```

### 5. Database Setup
```bash
# Push schema to database
npm run db:push

# Or if using migrations
npm run db:generate
npm run db:migrate
```

### 6. Development Commands
Add to package.json scripts:
```json
{
  "scripts": {
    "dev": "tsx server/index.ts",
    "build": "vite build",
    "db:push": "drizzle-kit push",
    "db:generate": "drizzle-kit generate",
    "db:migrate": "drizzle-kit migrate"
  }
}
```

### 7. Run Development Server
```bash
npm run dev
```

## Key Features
- 🎯 GPS-based automatic session detection
- ⏱️ Real-time session timer
- 💰 Automatic payment calculations
- 📊 Compensation tracking for shortfalls
- 👥 Dual role support (tutor/parent)
- 📱 Progressive Web App (mobile-friendly)

## Authentication Options

### Option A: Simple Local Auth
Remove Replit Auth dependencies and implement basic local authentication.

### Option B: Alternative OAuth
Replace Replit Auth with Google, GitHub, or other OAuth providers.

### Option C: Keep Replit Auth
Contact Replit support for external integration options.

## Database Schema
The app uses PostgreSQL with these main tables:
- `users` - User accounts with role support
- `students` - Student profiles with GPS coordinates
- `tutoring_sessions` - Session tracking with timing
- `compensations` - Shortfall tracking
- `notifications` - User notifications
- `sessions` - Express session storage

## GPS Simulation
For testing without actual GPS:
- Use the built-in location simulator
- Click "Go Here" buttons to simulate being at student locations
- Distance-based session detection (100m threshold)

## Troubleshooting

### Common Issues:
1. **Database Connection**: Verify DATABASE_URL is correct
2. **Missing GPS Coordinates**: Run geocoding to populate student locations
3. **Timer Not Starting**: Check active session detection logic
4. **Build Errors**: Ensure all TypeScript types are properly imported

### Debug Mode:
Enable detailed logging by checking browser console for:
- GPS detection logs
- Session creation/ending
- Distance calculations
- Timer state changes

## Deployment Options
- Vercel/Netlify for frontend
- Railway/Render for backend
- Neon/Supabase for database
- Or deploy as full-stack on single platform

## Support
Check the browser console for detailed debugging information. The app includes comprehensive logging for GPS detection, session management, and timer functionality.