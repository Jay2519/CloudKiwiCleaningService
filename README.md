# Elite Home Cleaning

Full-stack Next.js application for Elite Home Cleaning & Window Services, including public marketing pages, multi-step booking, customer dashboard, admin dashboard, Stripe billing, notifications, and Prisma/PostgreSQL data layer.

## Tech Stack

- Next.js (App Router) + TypeScript
- Tailwind CSS
- Prisma ORM + PostgreSQL
- NextAuth (Credentials + Google OAuth)
- Stripe (payments + subscriptions + webhooks)
- Resend (email)
- Twilio (SMS)
- Zod + React Hook Form

## Prerequisites

- Node.js 18+
- PostgreSQL (local or hosted)
- Stripe account
- Resend account
- Twilio account

## Installation

```bash
git clone <your-repo-url>
cd elite-home-cleaning
npm install
cp .env.example .env.local
# fill in .env.local
npx prisma migrate dev --name init
npx prisma db seed
npm run dev
```

## Stripe Setup

1. Create Stripe products and recurring prices for:
   - Basic
   - Standard
   - Premium
   - Elite
2. Copy each price ID into:
   - `STRIPE_BASIC_PRICE_ID`
   - `STRIPE_STANDARD_PRICE_ID`
   - `STRIPE_PREMIUM_PRICE_ID`
   - `STRIPE_ELITE_PRICE_ID`
3. Set webhook endpoint:
   - Local: `http://localhost:3000/api/stripe/webhook`
   - Production: `https://<your-domain>/api/stripe/webhook`
4. Start webhook listener locally:

```bash
stripe listen --forward-to localhost:3000/api/stripe/webhook
```

5. Copy the signing secret to `STRIPE_WEBHOOK_SECRET`.

## Deployment (Vercel + Supabase)

1. Create a PostgreSQL project in Supabase.
2. Copy the database connection string into `DATABASE_URL`.
3. Push repository to GitHub.
4. Import project into Vercel.
5. Add all environment variables from `.env.example`.
6. Deploy.
7. Run migrations against production DB:

```bash
npx prisma migrate deploy
```

## Admin Credentials (Seed)

- Email: `admin@elitehomecleaning.com`
- Password: `Admin123!`

## Available Scripts

- `npm run dev` - Start dev server
- `npm run build` - Build production app
- `npm run start` - Start production server
- `npm run lint` - Run lint checks
- `npm run db:push` - Push Prisma schema
- `npm run db:migrate` - Run Prisma dev migrations
- `npm run db:seed` - Seed database
- `npm run db:studio` - Open Prisma Studio
- `npm run db:reset` - Reset database
- `npm run stripe:listen` - Forward Stripe events to local webhook
- `npm run email:preview` - Start React Email preview

## Environment Variables

Use `.env.example` as the source of truth for all required variables:
- Auth/OAuth
- Stripe payments
- Resend + Twilio notifications
- App/business metadata
- Cron security secret

