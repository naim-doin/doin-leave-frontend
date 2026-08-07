# Doin Leave Portal — Frontend

A single static HTML file that talks to the backend API (see the
`doin-leave-backend` folder) — real email/password login, forced
password reset on first sign-in, and every view (dashboard, apply,
requests, team directory, calendar, holidays) backed by live data
instead of browser storage.

## Running it locally

You don't need a build step — it's one HTML file. Two ways to run it:

1. **Just open it.** Double-click `index.html`, or serve the folder with
   any static file server:
   ```bash
   npx serve .
   ```
2. On first load, it asks for your API's base URL (e.g.
   `http://localhost:4000/api` for local backend testing, or your Render
   URL once deployed). It remembers this per-browser, so you only enter
   it once.

Make sure the backend (`doin-leave-backend`) is running and seeded
first — see its own README.

## Deploying for free

Any static hosting works — this is just HTML/CSS/JS, no build step:

- **Render** — "New → Static Site", point it at this folder in your repo.
- **Netlify** — drag-and-drop the folder, or connect the repo.
- **GitHub Pages** — enable Pages on the repo, point it at this folder.

All are free for a static file this small. Once deployed, visit the URL,
enter your backend's API URL when prompted, and you're in.

### Important: CORS

Once both are deployed, go back to your backend's environment variables
on Render and set `CORS_ORIGIN` to your frontend's exact URL (e.g.
`https://doin-leave.netlify.app`). Without this, the browser will block
the frontend from calling the API.

## What's different from the old demo file

The previous `leave-portal.html` stored everything in browser memory (or
Claude artifact storage) and let you "pretend" to be any role via a
dropdown. This version:

- Requires a real email + password, checked server-side
- Forces a password change on first login
- Can't be tricked into acting as someone else — every action is
  checked against your actual account on the server
- Shows a company-wide "who's on leave" calendar without exposing other
  employees' leave reasons or full request details (a small
  privacy-aware API endpoint backs this)

## Known rough edges

- No "forgot password" self-service flow yet — matches the backend's
  current limitation, see its README.
- The temporary password shown when HR creates a new employee is
  displayed once in a toast notification — there's no email delivery
  wired up, so HR needs to relay it manually through a secure channel.
- No dark/light theme toggle — it's fixed to Doin's black-and-gold brand.
