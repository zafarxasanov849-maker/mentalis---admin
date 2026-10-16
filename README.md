# Mentalis — admin panel

Admin panel for the Mentalis bot (@mentaliss_bot). Two ways in, both from `/admin` in the bot:

- **Inside Telegram** — “Panelni ochish” opens it as a Mini App; the server checks Telegram's signed `initData` on every request.
- **In a normal browser (Chrome)** — “Brauzerda ochish” is a one-time link (10 minutes). Opening it creates a browser session
  kept for 30 days; “Chiqish” in the top bar ends it on this browser or on all browsers. The server stores only hashes.

Only Telegram IDs in the bot's admin list get in.

Sections: Statistika, Savollar (Kun savollari for the bot, Pro savollar for the platform: variant or written answer,
difficulty, image; add/edit and Excel import), Bot matnlari (every bot message, with live preview and history),
Sanalar (exam and registration dates used for the plan and reminders).

- Single static page: `index.html`. Served by GitHub Pages.
- API: Supabase Edge Function `levelup-bot` → `/admin`. Question images live in the private `q-images` bucket and are shown
  through short-lived signed links. No secrets in this repo.
- Layout preview without Telegram: open `index.html?demo=1` (add `&web=1` for the browser account menu; fake data, nothing is saved).
