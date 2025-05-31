# Next.js 15.3 + Supabase + TypeScript Starter

A modern, production-ready starter template for building full-stack applications with Next.js 15.3, Supabase, TypeScript, and Tailwind CSS v4.

## 🚀 Features

- **Next.js 15.3** with App Router and Server Components
- **Supabase** for authentication and database
- **TypeScript** with strict mode for type safety
- **Tailwind CSS v4** for modern styling
- **shadcn/ui** component library
- **TanStack Query** for client-side data management
- **Vitest** for testing
- **Zod** for schema validation
- Pre-configured development tools (ESLint, Prettier, Husky)

## 📋 Prerequisites

- Node.js 18+ 
- npm/yarn/pnpm
- Supabase CLI (`brew install supabase/tap/supabase`)

## 🛠️ Getting Started

### 1. Clone and Install

```bash
git clone <your-repo-url>
cd my-app
npm install
```

### 2. Set Up Supabase

Start local Supabase development stack:

```bash
npm run db:start
```

This will output your local Supabase credentials. Update `.env.local`:

```env
NEXT_PUBLIC_SUPABASE_URL=http://127.0.0.1:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
```

### 3. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see your app.

## 📁 Project Structure

```
├── app/                    # Next.js App Router
├── components/            
│   ├── ui/                # shadcn/ui components
│   └── features/          # Feature-specific components
├── lib/
│   ├── supabase/         # Supabase client configs
│   └── utils.ts          # Utility functions
├── supabase/
│   ├── migrations/       # Database migrations
│   └── config.toml       # Supabase configuration
└── types/                # TypeScript types
```

## 🔧 Available Scripts

```bash
# Development
npm run dev              # Start dev server with Turbopack
npm run build           # Build for production
npm run start           # Start production server
npm run lint            # Run ESLint

# Database
npm run db:start        # Start local Supabase
npm run db:stop         # Stop local Supabase
npm run db:reset        # Reset database
npm run db:types        # Generate TypeScript types
npm run db:push         # Push migrations to remote

# Testing
npm run test            # Run tests in watch mode
npm run test:ui         # Open Vitest UI
```

## 🏗️ Development Workflow

### Database Changes

1. Create a migration:
```bash
supabase migration new create_posts_table
```

2. Apply locally and regenerate types:
```bash
npm run db:reset
npm run db:types
```

### Adding UI Components

```bash
npx shadcn@latest add button card dialog
```

### Creating Features

1. Use Server Components by default
2. Add `'use client'` only when needed
3. Separate server and client Supabase instances
4. Use Server Actions for mutations

## 🧪 Testing

Write tests for:
- Business logic in utilities and hooks
- Server Actions with mocked Supabase
- Component behavior (not visual appearance)
- Error states and edge cases

```bash
npm run test
```

## 📚 Key Concepts

### Server Components First

```typescript
// ✅ Server Component (default)
export default async function Page() {
  const data = await getServerData()
  return <ClientComponent initialData={data} />
}
```

### Supabase Client Separation

```typescript
// Client-side (browser)
import { createClient } from '@/lib/supabase/client'

// Server-side (Node.js)
import { createClient } from '@/lib/supabase/server'
```

### Type-Safe Database Queries

```typescript
import type { Database } from '@/types/supabase'

type Post = Database['public']['Tables']['posts']['Row']
```

## 🚨 Important Guidelines

1. **Always regenerate types** after schema changes
2. **Use migrations** for all database changes
3. **Enable RLS** on all tables
4. **Validate environment variables** with Zod
5. **Test business logic**, not implementation details

## 📝 Environment Variables

Required environment variables:

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```

## 🤝 Contributing

1. Create feature branch
2. Make changes following the patterns in CLAUDE.md
3. Write/update tests
4. Submit PR

## 📄 License

MIT