# Sin City Udaipur — Gate Scanner

QR entry-pass scanner for **Sin City Udaipur** (Kairo × Firangi Nights).
Community partner: Hustling Together · Venue partner: Goya Hills

## What it does

- Staff opens the page, enters the gate PIN, and scans each guest's pass QR with the phone camera.
- **ENTRY ALLOWED** (green) on the first scan of a pass; **ALREADY USED** (red) on every scan after that, with the time of the first entry; **NOT A VALID PASS** for anything else.
- Check-ins are stored server-side, so several phones can scan at the same gate and a pass still only works once.
- If the network drops, the app keeps working offline and syncs queued check-ins as soon as it is back.
- A guest opening their own QR only sees their pass details — it is never marked used from the guest's phone.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app — self-contained, hostable on any static host |
| `server.js` | Minimal Node server for platforms that run a process |
| `package.json` | `npm start` runs the server |

## Backend

One-time-scan logic runs in a Supabase Edge Function (`gate`) backed by the
`sincity_passes` table. The API takes `status`, `auth`, `list`, `checkin`,
`sync` and `reset` actions as JSON POSTs.

## Deploy

Static hosts (Netlify, Vercel, Cloudflare Pages): upload `index.html`.
Process hosts (Railway, Render, Fly): `npm start`.
