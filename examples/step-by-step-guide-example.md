# step-by-step-guide — full example

**Topic:** Set up a new Next.js project on Vercel
**Width budget:** 80 cols
**Mode:** Unicode (default)

---

```
## Goal

Deploy a new Next.js app to a live Vercel preview URL with your
project linked to a Git repository.

                              ▼

### Step 1 — Install the Vercel CLI

Run: npm install -g vercel
Verify: vercel --version prints a version string (e.g. 32.x.x).

                              ▼

### Step 2 — Log in to Vercel

Run: vercel login
Choose your auth method (GitHub, GitLab, or email) when prompted.
Verify: CLI prints "Logged in as <your-email>".

                              ▼

### Step 3 — Scaffold a new Next.js project

Run: npx create-next-app@latest my-app --typescript --app
Verify: my-app/ directory created with app/ folder inside.

                              ▼

### Step 4 — Link the project to Vercel

Run: cd my-app && vercel link
Select your team and accept or enter a project name.
Verify: .vercel/project.json created in the project root.

                              ▼

### Step 5 — Deploy to preview

Run: vercel
Vercel builds, uploads, and prints a preview URL on success.
Verify: Open the printed URL — Next.js default home page loads.

## Outcome

✓ A live preview URL (https://<project>-<hash>.vercel.app) is
  accessible in the browser and returns the Next.js starter page.
```

---

## Why this works

- Five steps map exactly to the minimal command sequence (install → login → scaffold → link → deploy) with no optional detours, keeping the guide usable as a literal copy-paste walkthrough.
- Each step body stays at 1–3 lines: one action line plus one verify line, matching the format's layout rule and preventing the dense-step smell that pushes a guide toward playbook territory.
- The Outcome section gives an observable, URL-level proof of success rather than "it worked" — testers know exactly what to look for.
