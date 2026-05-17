# sequence-diagram — full example

**Topic:** SponsorCal Stripe Connect creator onboarding handshake
**Width budget:** 120 cols
**Mode:** Unicode (default)

---

```
SponsorCal — Stripe Connect Creator Onboarding

   [Creator]            [SponsorCal API]               [Stripe]                  [DB]
       │                        │                          │                       │
       │── POST /onboard ──────▶│                          │                       │
       │                        │                          │                       │
       │                        │── Create Connect acct ──▶│                       │
       │                        │   (account type: express) │                       │
       │                        │                          │                       │
       │                        │◀── account_id ───────────│                       │
       │                        │                          │                       │
       │                        │── INSERT creator row ────────────────────────────▶│
       │                        │   (stripeAccountId, status: pending)              │
       │                        │                          │                       │
       │◀── 302 redirect URL ───│                          │                       │
       │    (Stripe onboarding) │                          │                       │
       │                        │                          │                       │
       │── visits onboarding URL ────────────────────────▶│                       │
       │                        │                          │                       │
       │   [Creator completes KYC + bank details on Stripe] │                       │
       │                        │                          │                       │
       │                        │◀── webhook: account.updated ─────────────────────│
       │                        │    (charges_enabled: true) │                       │
       │                        │                          │                       │
       │                        │── UPDATE creator ────────────────────────────────▶│
       │                        │   (status: active)        │                       │
       │                        │                          │                       │
       │◀── 302 /dashboard ─────│                          │                       │
       │                        │                          │                       │
```

---

## Why this works

- Nine messages cover the full handshake from the creator's first POST through KYC completion and webhook acknowledgement — every state transition visible as a labeled arrow so a new engineer can trace the exact flow.
- The four actors are spaced to give message labels room to breathe; the longest arrow (`── webhook: account.updated ───`) spans three lifelines and sits just inside the 120-col budget.
- The inline comment `[Creator completes KYC + bank details on Stripe]` uses the sequence diagram convention of a bracketed note on the lifeline row to represent off-system activity without adding a fifth actor.
