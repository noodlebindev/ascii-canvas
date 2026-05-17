# sequence-diagram

## Purpose

Show time-ordered messages between named actors.

## Use when

- API call flows: what happens when a user does X
- Auth handshakes and OAuth flows
- Protocol interactions where ordering and direction matter
- Debugging "who calls who" questions

## Do NOT use when

- Static topology without time ordering — use `architecture-diagram`
- No time ordering — use `flowchart`

## Width budget

120 cols

## Arc

N/A — single artifact

## Layout rules

- Actor boxes `[Actor]` at the top, each with a vertical lifeline (`│`) below
- Messages flow as labeled horizontal arrows between lifelines, time descending
- Each arrow labeled with the message name; use `─▶` for request, `◀─` for response
- Activations (boxes on lifeline during processing) optional — omit for clarity in simple flows

## Canonical skeleton — Unicode

```
    [Client]              [API]               [DB]
        │                   │                   │
        │── POST /login ────▶│                   │
        │                   │── SELECT user ────▶│
        │                   │                   │
        │                   │◀── user record ───│
        │                   │                   │
        │◀── 200 + token ───│                   │
        │                   │                   │
```

## Canonical skeleton — ASCII fallback

```
    [Client]              [API]               [DB]
        |                   |                   |
        |-- POST /login ---->|                   |
        |                   |-- SELECT user ---->|
        |                   |                   |
        |                   |<-- user record ----|
        |                   |                   |
        |<-- 200 + token ----|                   |
        |                   |                   |
```

## Short rendered example

```
SponsorCal — Stripe Connect Onboarding

  [Creator]        [SponsorCal API]        [Stripe]         [DB]
      │                    │                   │               │
      │── POST /onboard ──▶│                   │               │
      │                    │── create account ▶│               │
      │                    │                   │               │
      │                    │◀── account id ────│               │
      │                    │                   │               │
      │                    │── INSERT creator ─────────────────▶│
      │                    │                   │               │
      │◀── redirect URL ───│                   │               │
      │                    │                   │               │
      │────────────── visits Stripe Connect ──▶│               │
      │                    │                   │               │
      │                    │◀── webhook: account.updated ──────│
      │                    │                   │               │
      │                    │── UPDATE creator ─────────────────▶│
      │                    │                   │               │
```

## Failure modes

- If actors exceed 4 → split into sub-flow diagrams linked by label
- If messages exceed 12 → split into named phases (Phase 1: Auth, Phase 2: Payment)
- If width overflows 120 cols → shorten actor and message labels
