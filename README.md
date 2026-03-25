# SmartRupee AI

Production-ready personal finance tracker for Indian users, built with React, TypeScript, Tailwind, and Supabase, with Gemini-powered AI features for receipts and budget forecasting.

Project done by Joshua Haniel J and N Omni Devi.

## Why SmartRupee AI

SmartRupee AI helps users stay on top of day-to-day spending with fast transaction entry, meaningful dashboard insights, and AI assistance that reduces manual effort.

## Core Features

- Secure email/password authentication with Supabase Auth
- Transaction management: create, filter, and export records
- AI receipt scanner: parse receipt images into structured transaction data
- AI budget forecaster: predict category overspend before month end
- Dashboard analytics with pie and trend charts
- Responsive UI for desktop and mobile
- Row-level security policies for per-user data isolation

## Technology Stack

- Frontend: React 18, TypeScript, Vite 5
- Styling: Tailwind CSS, daisyUI, Framer Motion
- Backend: Supabase (PostgreSQL, Auth, Storage, Edge Functions)
- AI: Google Gemini 2.0 Flash via Supabase Edge Functions
- Charts: Recharts
- Forms and validation: React Hook Form, Zod
- Utilities: date-fns, Lucide icons

## Quick Start

### 1) Install dependencies

```powershell
cd d:\Projects\Joshua\Smart-Rupee
npm install
```

### 2) Configure environment variables

```powershell
copy .env.example .env.local
```

Add the following values to `.env.local`:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your_anon_key_here
```

### 3) Set up Supabase schema

Run these SQL files in order from the Supabase SQL Editor:

1. `supabase/schema.sql`
2. `supabase/schema_upgrade_ai.sql`

### 4) Start development server

```powershell
npm run dev
```

App URL: `http://localhost:5173`

## AI Features

### Receipt Scanner

- Upload formats: JPEG, PNG, WebP, HEIC
- Max file size: 10 MB
- Extracts vendor, total amount, date, category, and line items
- Stores receipt images in private Supabase Storage bucket

### Budget Forecast

- Uses recent spending velocity (last 30 days)
- Predicts end-of-month category totals
- Highlights risk levels with actionable guidance

## Security Model

- Supabase RLS enforces strict per-user data access
- Gemini API key is stored in Edge Function secrets
- No client-side exposure of sensitive AI credentials

## Project Structure

```text
Smart-Rupee/
|-- src/
|   |-- components/
|   |-- context/
|   |-- lib/
|   |-- pages/
|   |-- services/
|   |-- App.tsx
|   |-- main.tsx
|   `-- styles.css
|-- functions/
|   `-- gemini-proxy/
|-- supabase/
|   |-- schema.sql
|   `-- schema_upgrade_ai.sql
|-- components/
|   `-- ui/
`-- package.json
```

## Development Commands

```powershell
npm run dev
npm run test
npm run typecheck
npm run build
```

## Deployment

### Frontend (Vercel or Netlify)

1. Push repository to GitHub
2. Connect repository in Vercel or Netlify
3. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`
4. Deploy

### Supabase Edge Function (required for AI)

```powershell
npx supabase login
npx supabase secrets set GEMINI_API_KEY=your_gemini_key --project-ref your-project-ref
npx supabase functions deploy gemini-proxy --project-ref your-project-ref
```

Routes provided by `gemini-proxy`:

- `POST /parse-receipt`
- `POST /forecast-budget`
- `POST /`

## Database Snapshot

Primary tables:

- `transactions`: amount, category, note, date, currency, timestamps
- `budgets`: budget amount per category and period
- `receipts`: receipt file metadata + parsed AI payload

Storage bucket:

- `receipts` (private, user-scoped folder access)

## Credits

- Project done by Joshua Haniel J and N Omni Devi
- UI inspiration: shadcn/ui
- 3D scenes: Spline
- Backend platform: Supabase
- AI model: Google Gemini 2.0 Flash

## License

MIT
