# Real Estate Voice Assistant

## Files
- `index.html` — the app. Browser voice demo + Admin panel (Personality / Integrations / Phone tabs).
- `api/vapi-webhook.js` — serverless endpoint that lets a real phone number ring this assistant. Deploys automatically with Vercel from the `api/` folder — no separate hosting.
- `vercel.json` — tells Vercel how to run the serverless function.

## Deploy
1. Change `ADMIN_PASSWORD` in `index.html` (search for it near the top of the `<script>` block).
2. Drag this whole folder into Vercel → Add New → Project → Deploy without Git.
3. Vercel gives you a live link — that's both the browser demo AND the phone webhook endpoint (`https://yourlink.vercel.app/api/vapi-webhook`).

## Browser demo (works immediately, zero setup)
Open the Vercel link in Chrome, allow mic, talk. Leads go to whatever's in Admin → Integrations.

## Real phone number (optional, needs a voice vendor)
Static pages can't answer phone calls — that needs a server. `api/vapi-webhook.js` is that server, already deployed with your site. To connect it:
1. Create an assistant at vapi.ai (or Retell/Bland).
2. Paste the same prompt from Admin → Personality.
3. Set the assistant's Server URL to `https://yourlink.vercel.app/api/vapi-webhook`.
4. Update `LEAD_WEBHOOKS` inside `api/vapi-webhook.js` to match what's in Admin → Integrations (the two don't share storage — browser uses localStorage, the server file uses its own array).

## Known limitations (demo-grade, by design)
- Admin password is client-side JS, visible in page source — fine for a client demo, not real security.
- Personality/webhooks saved in browser localStorage — per-browser, resets on a different device.
- Phone mode needs you to manually mirror webhook URLs into `api/vapi-webhook.js` since it's a separate runtime from the browser page.
