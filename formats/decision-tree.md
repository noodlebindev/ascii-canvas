# decision-tree

## Purpose

Strict yes/no branching to outcomes — each node is a question, each leaf is an outcome.

## Use when

- Classification or decision logic (should I use X or Y?)
- Troubleshooting flows where each answer eliminates paths
- Routing logic — matching input to one of several outcomes
- "Help me decide" requests with two conditions per fork

## Do NOT use when

- Mixed steps and branches in same flow — use `flowchart`
- More than 2 branches per node — use `flowchart`

## Width budget

100 cols

## Arc

N/A — single artifact

## Layout rules

- Root question at top
- Yes/No labels on every branch
- Outcomes (leaves) wrapped as `[Outcome name]` in a box
- Tree depth ≤ 4
- Diamonds `◆` mark decision nodes; rectangular boxes mark outcomes

## Canonical skeleton — Unicode

```
                     ◆─────────────────────────◆
                    ╱  Root question?            ╲
                   ◆                              ◆
                  ╱                                ╲
             Yes ▼                                  ▼ No
    ◆────────────────────◆                ┌──────────────────┐
   ╱  Follow-up?          ╲               │   [Outcome C]    │
  ◆                        ◆              └──────────────────┘
 ╱                          ╲
▼ Yes                    No ▼
┌──────────────┐    ┌──────────────┐
│ [Outcome A]  │    │ [Outcome B]  │
└──────────────┘    └──────────────┘
```

## Canonical skeleton — ASCII fallback

```
                     <>  Root question?  <>
                    /                      \
               Yes /                        \ No
     <> Follow-up? <>               +------------------+
    /                \              |   [Outcome C]    |
   /                  \             +------------------+
  v Yes            No v
+--------------+    +--------------+
| [Outcome A]  |    | [Outcome B]  |
+--------------+    +--------------+
```

## Short rendered example

```
Should I use Server Actions or API Routes in Next.js?

                     ◆───────────────────────────────◆
                    ╱  Is the trigger a form submit?   ╲
                   ◆                                    ◆
                  ╱                                      ╲
             Yes ▼                                        ▼ No
    ◆──────────────────────◆                ┌─────────────────────────┐
   ╱ Needs optimistic UI?   ╲               │ [Use an API Route]      │
  ◆                          ◆              └─────────────────────────┘
 ╱                            ╲
▼ Yes                      No ▼
┌────────────────────┐    ┌────────────────────────┐
│ [Server Action +   │    │ [Server Action alone]  │
│  useOptimistic]    │    └────────────────────────┘
└────────────────────┘
```

## Failure modes

- If tree depth exceeds 4 → split into chained trees linked by name reference
- If any node has more than 2 branches → switch to `flowchart`
- If tree width overflows 100 cols → shorten question labels or increase depth instead of width
