# comic — full example

**Topic:** Ser vs Estar — the classic "Yo soy 30 años" mistake (A9.1 teaching arc, 4 panels)
**Width budget:** 100 cols
**Mode:** Unicode (default — comic doesn't have an ASCII fallback)

---

```
┌── Panel 1: At the language exchange ───────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                            Carlos                                       │
│   (•‿•) ── "¡Hola! ¿Cuántos años tienes?"                                "¡Hola!" ── [•‿•]      │
│     │                                                                       │                   │
│    ╱│╲                                                                     ╱│╲                  │
│    ╱ ╲                                                                     ╱ ╲                  │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 2: The mistake ────────────────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                            Carlos                                       │
│   (¬_¬)                                                       "Yo soy 30 años." ── [•_•]        │
│     │                                                                       │                   │
│    ╱│╲                                                                     ╱│╲                  │
│    ╱ ╲                                                                     ╱ ╲                  │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 3: The correction ─────────────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                                                                         │
│   (•‿•) ── ╭───────────────────────────────────────────────────╮                                │
│              │ ¡Casi! Para la edad usamos TENER, no SER.        │                               │
│              │ Es: "Tengo 30 años" — literalmente,              │                               │
│              │ "I have 30 years."                               │                               │
│              ╰───────────────────────────────────────────────────╯                              │
│     │                                                                                           │
│    ╱│╲                                          Carlos                                          │
│    ╱ ╲                                          (O_o) ── "Oh."                                  │
│                                                   │                                             │
│                                                  ╱│╲                                            │
│                                                  ╱ ╲                                            │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘

┌── Panel 4: Application ────────────────────────────────────────────────────────────────────────┐
│                                                                                                 │
│   Sofía                                            Carlos                                       │
│   (•◡•) ── "¡Eso es!"                                              "Tengo 30 años." ── [^_^]    │
│     │                                                                       │                   │
│    ╱│╲                                                                     ╱│╲                  │
│    ╱ ╲                                                                     ╱ ╲                  │
│                                                                                                 │
│   ┌── narración ─────────────────────────────────────────────────────────────────────────────┐ │
│   │  Rule: edad (age) uses TENER. SER is for identity ("Soy Carlos"), not duration.           │ │
│   └───────────────────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Why this works

- **A9.1 teaching arc** in exactly 4 panels: Sofía's question sets up the situation, Carlos makes the canonical mistake, Sofía corrects with the rule stated explicitly (boxed bubble for the longer explanation), Carlos applies it correctly. Each panel earns its existence per U1.
- **Face progression** carries the emotion arc: Sofía neutral-happy → skeptical → patient → pleased; Carlos cheerful → confident-wrong → surprised → delighted. Mandatory per comic-specific strict QA item 5.
- **Bracket consistency** holds: Sofía always `(...)`, Carlos always `[...]`. Identity readable at a glance even without name labels (which are present in all panels for clarity).
- **Hybrid bubble grammar** in action: inline `── "..."` for short lines, boxed `╭─...─╮` for the longer correction in Panel 3, and a narration box in Panel 4 for the takeaway rule.
- **A9.1 over A9.2** chosen because the topic has a story shape (encounter → mistake → reveal → apply). A9.2 contrast would compress this into 2 panels but loses the dramatic moment of the mistake landing.

## ASCII variant

Comic does not ship an ASCII fallback. The format relies on Unicode emoticons (`(•‿•)` etc.) and rounded bubble corners (`╭╮╰╯`) that have no clean ASCII equivalents preserving the comic feel. If a user requests plain ASCII output, the skill falls back to `slideshow` per the failure-mode in `comic.md` and the format-fallback map in `qa-checklist.md`.
