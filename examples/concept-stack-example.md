# concept-stack — full example

**Topic:** Modern web app stack (DB → ORM → API → SSR framework → CDN → User)
**Width budget:** 100 cols
**Mode:** Unicode (default)

---

```
Modern Web App Stack — Layer by Layer
──────────────────────────────────────

┌──────────────────────────────────────────────────────────────────────────────────────────┐
│  Layer 6 — User Outcome                                                                  │
│  role: fast initial loads, dynamic personalised content, seamless navigation             │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│  Layer 5 — CDN / Edge  (Vercel Edge Network)                                             │
│  role: serves cached HTML and static assets from the nearest PoP; runs middleware        │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│  Layer 4 — SSR Framework  (Next.js App Router)                                           │
│  role: renders HTML on the server or at build time; manages routing and React Server     │
│        Components; calls Route Handlers for mutations                                    │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│  Layer 3 — API / HTTP Boundary  (Next.js Route Handlers)                                 │
│  role: exposes typed REST endpoints; validates input; enforces auth; calls ORM           │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│  Layer 2 — ORM  (Prisma)                                                                 │
│  role: translates TypeScript models to SQL; manages migrations; enforces schema types    │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│  Layer 1 — Database  (Neon Postgres)                                                     │
│  role: durable, relational storage; ACID transactions; row-level security                │
└──────────────────────────────────────────────────────────────────────────────────────────┘

Each layer can only be understood fully in terms of the layer below it.
Remove any layer and the one above loses its foundation.
```

---

## Why this works

- Six layers follow the A5 arc exactly (base → supporting layers → top outcome), with the User Outcome at the top to show what the stack is ultimately for — the builder reads top-down as aspiration, bottom-up as dependency.
- Each `role:` line is a complete sentence (not just a noun phrase), which makes the stack usable as onboarding documentation rather than a bare vocabulary list.
- The two-sentence synthesis below the box reinforces the "depends on" semantics that define the concept-stack format — it makes the abstraction explicit rather than leaving it implied.
