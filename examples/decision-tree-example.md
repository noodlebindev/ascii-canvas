# decision-tree — full example

**Topic:** Should I use Next.js Server Actions or API Routes?
**Width budget:** 100 cols
**Mode:** Unicode (default)

---

```
Should I use Server Actions or API Routes in Next.js?

                        ◆─────────────────────────────────────────◆
                       ╱  Is the call mutation-bound to a form?     ╲
                      ◆                                              ◆
                     ╱                                                ╲
                Yes ▼                                                  ▼ No
       ◆──────────────────────────◆                    ◆─────────────────────────────◆
      ╱  Need a streaming response? ╲                 ╱  External consumers need REST? ╲
     ◆                               ◆               ◆                                  ◆
    ╱                                 ╲             ╱                                    ╲
Yes ▼                              No ▼        Yes ▼                                 No ▼
┌──────────────────┐    ┌──────────────────────┐    ┌──────────────────┐    ┌──────────────────────┐
│  [API Route]     │    │  [Server Action]     │    │  [API Route]     │    │  [Server Action]     │
│                  │    │                      │    │                  │    │                      │
│  Use Route       │    │  Bind directly to    │    │  Expose stable   │    │  Call from Server    │
│  Handler with    │    │  the form's action   │    │  REST endpoint   │    │  Component or        │
│  streaming       │    │  prop; no endpoint   │    │  for 3rd-party   │    │  client handler;     │
│  response        │    │  needed              │    │  consumers       │    │  simpler, typesafe   │
└──────────────────┘    └──────────────────────┘    └──────────────────┘    └──────────────────────┘
```

---

## Why this works

- Two decision levels cover the key architectural forks: form-binding (Server Action vs API Route) and within the Server Action branch, streaming (which forces a Route Handler anyway). This produces four clean outcome leaves with no ambiguous mid-tree states.
- The outcome boxes carry explanatory sub-lines rather than just labels — the richer content shows why each path was chosen, not just what it is.
- Layout stays within 100 cols by using 18-char-wide outcome boxes and keeping question diamonds tight; the widest line is the root question row at ~88 chars.

## ASCII variant (if structurally different from Unicode)

```
Should I use Server Actions or API Routes in Next.js?

                     <> Is the call mutation-bound to a form? <>
                    /                                           \
                 Yes                                            No
                  /                                              \
  <> Need streaming response? <>          <> External consumers need REST? <>
 /                              \        /                                   \
Yes                             No     Yes                                   No
v                                v      v                                     v
+------------------+  +--------------------+  +------------------+  +--------------------+
| [API Route]      |  | [Server Action]    |  | [API Route]      |  | [Server Action]    |
|                  |  |                    |  |                  |  |                    |
| Route Handler    |  | Bind to form       |  | Expose stable    |  | Call from Server   |
| with streaming   |  | action prop;       |  | REST endpoint    |  | Component; simpler |
| response         |  | no endpoint needed |  | for 3rd-parties  |  | and typesafe       |
+------------------+  +--------------------+  +------------------+  +--------------------+
```
