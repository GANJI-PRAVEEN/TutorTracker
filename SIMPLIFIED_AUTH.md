# Simplified Authentication Setup

Since Replit Auth is specific to Replit, here's how to set up simple local authentication:

## Option 1: Remove Authentication (Simplest)
Remove all auth-related code and run the app locally without user authentication.

### Changes needed:
1. Remove `isAuthenticated` middleware from routes
2. Use a hardcoded user ID for development
3. Remove auth-related imports and dependencies

## Option 2: Simple Local Auth
Implement basic username/password authentication:

### Install additional dependencies:
```bash
npm install bcryptjs jsonwebtoken
npm install -D @types/bcryptjs @types/jsonwebtoken
```

### Create simple auth middleware:
```typescript
// server/auth.ts
import jwt from 'jsonwebtoken';
import bcrypt from 'bcryptjs';

const JWT_SECRET = process.env.JWT_SECRET || 'your-secret-key';

export const hashPassword = async (password: string) => {
  return await bcrypt.hash(password, 10);
};

export const comparePassword = async (password: string, hash: string) => {
  return await bcrypt.compare(password, hash);
};

export const generateToken = (userId: string) => {
  return jwt.sign({ userId }, JWT_SECRET, { expiresIn: '7d' });
};

export const verifyToken = (token: string) => {
  try {
    return jwt.verify(token, JWT_SECRET) as { userId: string };
  } catch {
    return null;
  }
};
```

## Option 3: Use Alternative OAuth
Replace with Google, GitHub, or other OAuth providers using Passport.js strategies.

## Recommendation for Quick Setup
Use Option 1 (no auth) for local development, then add proper authentication later when you're ready to deploy.

### Quick No-Auth Setup:
1. Replace `isAuthenticated` with a function that returns a test user
2. Set a default user ID in your routes
3. Comment out auth-related frontend code

This will let you focus on the core GPS tracking and timer functionality first.