# architecture-diagram

## Purpose

Visualize system components, services, and how they connect.

## Use when

- Showing service topology and how components relate
- Data flow between components or tiers
- Layered systems (frontend → backend → data)
- Deployment architecture for documentation or onboarding

## Do NOT use when

- Time-ordered interactions between actors — use `sequence-diagram`
- Pure layer dependency without cross-connections — use `concept-stack`

## Width budget

120 cols

## Arc

N/A — single artifact

## Layout rules

- Boxes for components; lines for connections; labels on connections (protocol/payload)
- Layered top-to-bottom or left-to-right by tier (frontend → backend → data)
- Group related components inside a shared region with a label
- External systems use double border (`╔═╗`); internal systems use single border (`┌─┐`)
- Connection arrows: `▼` (down), `─▶` (right), `◀─` (left)

## Canonical skeleton — Unicode

```
╔════════════════════════╗
║     External Client    ║   (external)
╚══════════╤═════════════╝
           │  HTTPS
           ▼
┌──────────────────────────────────────────────────────┐
│                    Edge / CDN                        │  (internal)
└────────────────────────┬─────────────────────────────┘
                         │  HTTP
                         ▼
           ┌─────────────────────────┐
           │       API Server        │  (internal)
           └────────┬────────────────┘
                    │  SQL
                    ▼
           ╔════════════════════════╗
           ║       Database         ║   (external)
           ╚════════════════════════╝
```

## Canonical skeleton — ASCII fallback

```
+=========================+
|     External Client     |   (external)
+==========+==============+
           |  HTTPS
           v
+------------------------------------------------------+
|                    Edge / CDN                        |  (internal)
+------------------------+-----------------------------+
                         |  HTTP
                         v
           +-------------------------+
           |       API Server        |  (internal)
           +--------+----------------+
                    |  SQL
                    v
           +=========================+
           |       Database          |   (external)
           +=========================+
```

## Short rendered example

```
SponsorCal Architecture

╔═══════════════════════╗
║       Browser         ║   (external)
╚══════════╤════════════╝
           │  HTTPS
           ▼
┌──────────────────────────────────────────────────────────┐
│                  Vercel Edge / CDN                       │
└────────────────────────────┬─────────────────────────────┘
                             │  HTTP / Next.js routing
                             ▼
              ┌──────────────────────────────┐
              │     Next.js API + App Router  │
              └───────────┬──────────────────┘
                          │
           ┌──────────────┼──────────────┐
           │  Prisma ORM  │              │
           ▼              ▼              ▼
╔═══════════════╗  ┌────────────┐  ╔══════════════╗
║  Neon Postgres ║  │ Vercel Blob│  ║    Stripe    ║
╚═══════════════╝  └────────────┘  ╚══════════════╝
```

## Failure modes

- If components exceed 8 → group into named sub-diagrams and reference each from a top-level overview
- If diagram grows too tall → switch to left-to-right layout
- If width overflows 120 cols → shorten component labels or remove protocol labels from arrows
