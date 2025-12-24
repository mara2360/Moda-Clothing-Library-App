# Wishlist App

## Overview

A full-stack wishlist management application that allows users to save and organize items they want to purchase. Users can add items by URL (with automatic metadata scraping), organize them into categories, and track their purchase status. The app features a modern, elegant UI with a warm color palette and smooth animations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state caching and synchronization
- **Styling**: Tailwind CSS with CSS variables for theming
- **UI Components**: shadcn/ui component library (Radix primitives + Tailwind)
- **Animations**: Framer Motion for smooth transitions
- **Forms**: React Hook Form with Zod validation

The frontend follows a component-based architecture with:
- Pages in `client/src/pages/` (Dashboard, Auth, NotFound)
- Reusable components in `client/src/components/`
- Custom hooks in `client/src/hooks/` for data fetching and auth
- Shared UI primitives in `client/src/components/ui/`

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript (ESM modules)
- **Build Tool**: esbuild for server bundling, Vite for client
- **API Design**: RESTful endpoints with Zod schema validation

Key server files:
- `server/index.ts` - Express app setup and middleware
- `server/routes.ts` - API route definitions
- `server/storage.ts` - Database access layer
- `server/db.ts` - Database connection pool

### Data Storage
- **Database**: PostgreSQL
- **ORM**: Drizzle ORM with drizzle-zod for schema validation
- **Schema Location**: `shared/schema.ts` (shared between client/server)
- **Migrations**: `migrations/` directory via drizzle-kit

Database tables:
- `users` - User accounts (Replit Auth)
- `sessions` - Session storage for authentication
- `categories` - User-defined item categories
- `items` - Wishlist items with URL, title, image, price, etc.

### Authentication
- **Provider**: Replit Auth (OpenID Connect)
- **Session Storage**: PostgreSQL via connect-pg-simple
- **Implementation**: Passport.js with custom OIDC strategy
- Located in `server/replit_integrations/auth/`

### Key Features
1. **URL Metadata Scraping**: Server-side scraping using Cheerio to extract title, image, and price from product URLs
2. **Category Management**: Users can create categories to organize items
3. **Purchase Tracking**: Items can be marked as bought/unbought
4. **Responsive Design**: Mobile-first with sidebar navigation

## External Dependencies

### Third-Party Services
- **Replit Auth**: OpenID Connect authentication via Replit
- **PostgreSQL**: Database (provisioned via Replit)

### Key NPM Packages
- `drizzle-orm` / `drizzle-kit` - Database ORM and migrations
- `express` / `express-session` - Web server and session handling
- `passport` / `openid-client` - Authentication
- `cheerio` - HTML parsing for metadata scraping
- `@tanstack/react-query` - Client-side data fetching
- `zod` - Schema validation (shared between client/server)
- `framer-motion` - Animations
- Radix UI primitives - Accessible component foundations

### Environment Variables Required
- `DATABASE_URL` - PostgreSQL connection string
- `SESSION_SECRET` - Session encryption key
- `ISSUER_URL` - Replit OIDC issuer (defaults to https://replit.com/oidc)
- `REPL_ID` - Replit environment identifier