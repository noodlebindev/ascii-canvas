# architecture-diagram — full example

**Topic:** SponsorCal architecture (browser → Vercel edge → Next.js API → Prisma → Neon Postgres + Vercel Blob)
**Width budget:** 120 cols
**Mode:** Unicode (default)

---

```
SponsorCal — System Architecture
─────────────────────────────────

╔══════════════════╗
║     Browser      ║   (external)
╚════════╤═════════╝
         │  HTTPS
         ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                          Vercel Edge / CDN                                 │
│   ISR page cache · static assets · Edge Middleware (auth redirect)        │
└────────────────────────────────┬───────────────────────────────────────────┘
                                 │  HTTP / Next.js routing
                                 ▼
             ┌───────────────────────────────────────────┐
             │           Next.js App Router               │
             │  ┌─────────────────────────────────────┐  │
             │  │  App Router pages  (ISR / SSR / RSC) │  │
             │  └─────────────────────────────────────┘  │
             │  ┌─────────────────────────────────────┐  │
             │  │  Route Handlers  (REST API + webhooks)│  │
             │  └─────────────────────────────────────┘  │
             └─────────────┬───────────────────┬─────────┘
                           │  Prisma ORM (SQL)  │
              ┌────────────┘                   └─────────────┐
              ▼                                               ▼
╔══════════════════════════╗                   ╔══════════════════════════╗
║      Neon Postgres        ║                   ║       Vercel Blob        ║
║  (shiny-king / prod DB)   ║                   ║   (signed asset URLs)   ║
╚══════════════════════════╝                   ╚══════════════════════════╝

── Integrations (right-side, external) ──────────────────────────────────────

╔═══════════════════╗  Webhooks ◄── Next.js Route Handler (/api/stripe/webhook)
║   Stripe Connect  ║
║   (payments /     ║  → Creator onboarding, booking checkout, payout triggers
║    payouts)       ║
╚═══════════════════╝

╔═══════════════════╗  SMTP API ──► Next.js Route Handler (/api/email/*)
║     Maileroo      ║
║   (transactional  ║  → Booking confirmations, sponsor access links
║     email)        ║
╚═══════════════════╝

╔═══════════════════╗  REST ──► Next.js middleware / API routes
║  Upstash Redis    ║
║  (rate limiting / ║  → Reservation TTL locks (10 min capacity hold)
║   session cache)  ║
╚═══════════════════╝
```

---

## Why this works

- The main vertical flow (Browser → Edge → App Router → Prisma → DBs) uses single-border boxes for internal components and double-border `╔═╗` for external systems, strictly following the architecture-diagram layout rule — the visual distinction is immediately legible.
- Integrations are pulled to a separate labelled section below the main stack rather than placed at the right margin, which keeps the primary flow narrow and avoids crossing leader lines — a common overflow cause at 120 cols.
- The inner App Router box contains two sub-boxes (pages vs routes) to show the dual-role of Next.js without adding extra layers to the vertical flow.
