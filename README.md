# FMS – Fleet Financial Management System (Netlify package)

## Files
| File | Purpose |
|---|---|
| `index.html` | The whole app (your FMS-app-14.html, renamed so Netlify serves it at `/`) |
| `manifest.webmanifest`, `icon-*.png`, `sw.js` | Installable app (Add to Home Screen) |
| `netlify.toml`, `_redirects`, `robots.txt` | Netlify settings, no-cache for the app shell, hidden from search engines |
| `database.rules.json` | Your Firebase Realtime Database rules (already published by you; kept here as a backup) |
| `relay/fms-whatsapp-relay.js` | OPTIONAL 24/7 WhatsApp sender. Not needed to run the app |

## Deploy on Netlify
1. Go to app.netlify.com > Add new site > **Deploy manually**.
2. Drag the **unzipped folder** (or this zip) onto the drop area.
3. Open the site URL and sign in with your admin email and password (Admin tab).

## Firebase checklist
- Authentication > Sign-in method: **Email/Password** enabled.
- Realtime Database rules = `database.rules.json`.
- Your admin node must exist: `admins/<admin UID>: true` (your admins.json).
- Authentication > Settings > **Authorized domains**: add your Netlify domain (e.g. `yoursite.netlify.app`). Needed only for some Firebase auth flows, but harmless to add.
- The API key in `index.html` is a public web key. Security comes from the rules, so keep them published.

## Known limits (from the app code, not Netlify)
- **Traccar** must be served over **https** and allow your Netlify origin (`web.origin` in traccar.xml), otherwise browsers block it.
- Alerts and Traccar polling run only while FMS is open in a browser. For 24/7 WhatsApp alerts, host `relay/fms-whatsapp-relay.js` on a small server (Render, Railway, a VPS) and choose "My WhatsApp Business relay" in Integrations.
- Email reminders: the app opens your mail program (`mailto:`). Automatic server-sent emails are not included.
- The customer chatbot ("Where is my vehicle?") is not part of this package. The app only exports `customers.json` for it.
- Driver and document files are stored inside the database (max 600 KB each). Fine for small fleets.
- Passwords shorter than 6 characters are padded for Firebase, so 4 digit passwords work but are weak. Tell your users to pick longer ones.

## Update the app later
Replace `index.html`, then in Netlify open Deploys > drag the folder again.
