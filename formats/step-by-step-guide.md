# step-by-step-guide

## Purpose

Simple linear walkthrough — goal, steps, outcome. Lighter than `playbook` (no prerequisites, success criteria, or failure modes block).

## Use when

- A simple sequential process with no branching
- A user asks "walk me through X" or "how do I do X?"
- A one-off how-to task where failure recovery is trivial
- 4–7 steps that form a straight line from start to done

## Do NOT use when

- The process needs prerequisites, success criteria, and failure modes — use `playbook`
- Steps have branching logic or conditionals — use `flowchart`
- Pure decision-making without execution steps — use `decision-tree`

## Width budget

80 cols

## Arc

A8 — Step-by-step-guide arc (4–7 steps): goal → steps → outcome

## Layout rules

- `## Goal` section at top with a single sentence stating the end state
- Numbered steps as `### Step N — <verb-phrase>` headings
- Each step body: 1–3 lines max (action + optional verify line)
- Steps separated by a centered `▼` marker on its own line
- `## Outcome` section at end with a `✓` verification line (Unicode) or `[x]` (ASCII fallback)
- No boxes or table borders required — plain indented text is sufficient

## Canonical skeleton — Unicode

```
## Goal

<One sentence describing the end state when all steps are complete.>

                              ▼

### Step 1 — <Verb phrase>

<Action line: what to do.>
<Optional verify: how to confirm it worked.>

                              ▼

### Step 2 — <Verb phrase>

<Action line: what to do.>
<Optional verify: how to confirm it worked.>

                              ▼

### Step 3 — <Verb phrase>

<Action line: what to do.>
<Optional verify: how to confirm it worked.>

## Outcome

✓ <Verification statement — observable proof the goal is achieved.>
```

## Canonical skeleton — ASCII fallback

```
## Goal

<One sentence describing the end state when all steps are complete.>

                              v

### Step 1 -- <Verb phrase>

<Action line: what to do.>
<Optional verify: how to confirm it worked.>

                              v

### Step 2 -- <Verb phrase>

<Action line: what to do.>
<Optional verify: how to confirm it worked.>

                              v

### Step 3 -- <Verb phrase>

<Action line: what to do.>
<Optional verify: how to confirm it worked.>

## Outcome

[x] <Verification statement — observable proof the goal is achieved.>
```

## Short rendered example

Set up a Vercel project for a Next.js app:

```
## Goal

Deploy a Next.js app to Vercel with environment variables configured.

                              ▼

### Step 1 — Install Vercel CLI

Run: npm install -g vercel
Verify: vercel --version prints a version number.

                              ▼

### Step 2 — Link the project

Run: vercel link in your project root.
Choose your team and project name when prompted.

                              ▼

### Step 3 — Set environment variables

Run: vercel env add <NAME> for each required variable.
Verify: vercel env ls shows all variables listed.

                              ▼

### Step 4 — Deploy

Run: vercel --prod to deploy to production.
The CLI prints a live URL on success.

## Outcome

✓ Live URL is accessible in a browser and returns HTTP 200.
```

## Failure modes

- If steps exceed 7 → switch to `playbook` (the extra complexity warrants prerequisites and success criteria)
- If any step has conditional logic (if X then Y else Z) → switch to `flowchart`
- If the guide is referenced repeatedly and failures need documented recovery → upgrade to `playbook`
