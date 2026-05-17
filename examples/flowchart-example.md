# flowchart — full example

**Topic:** User signup with email verification + magic link fallback
**Width budget:** 100 cols
**Mode:** Unicode (default)

---

```
User Signup — Email Verification + Magic Link Fallback
───────────────────────────────────────────────────────

┌────────────────────────────────────────┐
│                 START                  │
└─────────────────────┬──────────────────┘
                      │
                      ▼
┌────────────────────────────────────────┐
│          Enter email address           │
└─────────────────────┬──────────────────┘
                      │
                      ▼
┌────────────────────────────────────────┐
│       Send verification email         │
└─────────────────────┬──────────────────┘
                      │
                      ▼
               ◆────────────◆
              ╱  Link clicked ╲
             ◆                 ◆
            ╱                   ╲
       Yes ▼                     ▼ No (timeout 15 min)
┌──────────────────┐      ┌──────────────────────────┐
│  Verify token    │      │   Send magic link email  │
└────────┬─────────┘      └─────────────┬────────────┘
         │                              │
         ▼                              ▼
  ◆────────────◆               ◆─────────────────◆
 ╱ Token valid? ╲             ╱  Magic link used?  ╲
◆                ◆           ◆                      ◆
╱                 ╲          ╱                        ╲
▼ Yes          No ▼     Yes ▼                      No ▼
┌──────────┐  ┌────────────────┐         ┌──────────────────────┐
│ Account  │  │  Show "token   │         │  Prompt re-enter     │
│  active  │  │  expired" msg  │         │  email (loop back)   │
└────┬─────┘  └───────┬────────┘         └──────────┬───────────┘
     │                │                             │
     │                ▼                             │
     │     ┌──────────────────────────┐             │
     │     │  Re-enter email address  │◄────────────┘
     │     └──────────────┬───────────┘
     │                    │ (loops to "Send verification email")
     │                    │
     │                    ▼
     │       ┌────────────────────────────────────────┐
     │       │       Send verification email          │  ◄── loop
     │       └────────────────────────────────────────┘
     │
     ▼
┌────────────────────────────────────────┐
│          Redirect to dashboard         │
└─────────────────────┬──────────────────┘
                      │
                      ▼
┌────────────────────────────────────────┐
│                  END                   │
└────────────────────────────────────────┘
```

---

## Why this works

- Three decision diamonds cover the full branching space: link clicked, token valid, and magic link used — each with a clearly labeled Yes/No path so the happy path is traceable top-to-bottom.
- The loop-back for "re-enter email" is drawn as a right-side leader to the "Send verification email" box rather than crossing the main flow, keeping the diagram readable within 100 cols.
- Boxes were kept to 40 inner chars so that both branches at the second level fit side-by-side without exceeding budget; label text was shortened ("Show 'token expired' msg") rather than widened.

## ASCII variant (if structurally different from Unicode)

```
User Signup -- Email Verification + Magic Link Fallback
--------------------------------------------------------

+----------------------------------------+
|                 START                  |
+---------------------+------------------+
                      |
                      v
+----------------------------------------+
|          Enter email address           |
+---------------------+------------------+
                      |
                      v
+----------------------------------------+
|       Send verification email         |
+---------------------+------------------+
                      |
                      v
              <  Link clicked? >
             /                   \
          Yes                    No (timeout)
           v                       v
+------------------+      +--------------------------+
|  Verify token    |      |   Send magic link email  |
+--------+---------+      +-------------+------------+
         |                              |
         v                              v
   < Token valid? >            < Magic link used? >
  /               \           /                    \
Yes              No         Yes                    No
 v                v           v                      v
+----------+ +----------+  +----------+   +--------------------+
| Account  | | Token    |  | Account  |   | Re-enter email     |
|  active  | | expired  |  |  active  |   | (loops back)       |
+----+-----+ +----------+  +----+-----+   +---------+----------+
     |                          |                   |
     |                          +----> Send verif. email <------+
     v
+----------------------------------------+
|         Redirect to dashboard          |
+---------------------+------------------+
                      |
                      v
+----------------------------------------+
|                  END                   |
+----------------------------------------+
```
