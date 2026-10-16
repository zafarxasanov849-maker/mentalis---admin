# Mentalis — admin panel

Telegram Mini App for the Mentalis bot (@mentaliss_bot). Opens from the bot with `/admin`; only Telegram IDs in the
bot's admin list get in (the server checks Telegram's signed `initData` on every request).

Sections: Statistika, Savollar (add/edit, Excel import), Bot matnlari (every bot message, with live preview and
history), Sanalar (exam and registration dates used for the plan and reminders).

- Single static page: `index.html`. Served by GitHub Pages.
- API: Supabase Edge Function `levelup-bot` → `/admin`. No secrets in this repo.
- Layout preview without Telegram: open `index.html?demo=1` (fake data, nothing is saved).
