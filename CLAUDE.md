# Mentalis — admin panel

Milliy Sertifikat (MS) imtihoniga tayyorgarlik platformasining **admin paneli**. Telegram bot `@mentaliss_bot` uchun orqa ofis.

## Loyihaning hozirgi holati (6-noyabr 2026)

- **Yoshi:** 2 hafta
- **Foydalanuvchi:** 0 (real, botga yozmagan)
- **Nishon:** qishki MS sikli (dekabr-fevral)
- **Brand:** Mentalis (yagona). "Level Up", "Jumavoy" — eski nomlar, ishlatilmaydi.

## Bu repo — nima?

- **Bitta static** `index.html` (~80 KB, vanilla HTML/CSS/JS)
- GitHub Pages'da hosted
- Backend chaqiradi: `https://gaghsvffdfkxhxniwtmw.supabase.co/functions/v1/levelup-bot/admin`
  (Supabase Edge Function `levelup-bot` — ichki nom, foydalanuvchi ko'rmaydi, almashtirmang)

## Kirish

Faqat `bot_config.admin_ids` ichidagi Telegram ID'lar kira oladi. 2 yo'l:

- **Telegram Mini App:** `/admin` → "Panelni ochish". Server har so'rovda `initData` imzosini tekshiradi.
- **Brauzer:** `/admin` → "Brauzerda ochish". 10 daqiqalik bir martalik havola. Ochilsa, 30 kunlik sessiya yaratiladi (faqat hash saqlanadi).

## Sahifalar

- **Statistika** — foydalanuvchi, javob, streak metrikalar
- **Savollar**
  - Kun savollari (bot kunlik yuboradi) — `bot_questions.pool='daily'`, `qtype='choice'`
  - Pro savollar (web platforma uchun — hali tayyor emas) — `pool='pro'`, `qtype='choice'|'written'`, qiyinlik, rasm
- **Bot matnlari** — har bot xabarini tahrir qilish, versiyalash (`bot_texts` + `bot_text_history`)
- **Sanalar** — imtihon va ro'yxatdan o'tish sanalari (`bot_sessions`)

## Demo rejim

`index.html?demo=1&web=1` — Telegram'siz UI'ni ko'rish, soxta ma'lumot bilan.

## Stack

- **Frontend:** vanilla HTML + CSS + JS (hech qanday framework). Build step yo'q.
- **Backend:** Supabase Edge Function (Deno) — `levelup-bot` (v14+)
- **DB:** Supabase Postgres 17 (ref `gaghsvffdfkxhxniwtmw`, eu-central-1)
- **Rasm storage:** `q-images` private bucket, qisqa muddatli signed URL

## Qo'shiq bazadagi jadvallar (bu panelni boshqaradigan)

- `bot_users` (tg_id PK, role s/t/p, subjects[], streak)
- `bot_questions` (id PK, subject, body, options jsonb, correct, pool, qtype)
- `bot_daily` (tg_id + day PK, question_id, choice, is_correct)
- `bot_sessions` (id PK, exam_label, exam_start, reg_until)
- `bot_texts` (key PK, value, updated_by) + `bot_text_history`
- `admin_sessions` (token_hash PK, kind, tg_id, expires_at)
- `bot_config` (key PK, value) — `admin_ids`, `webhook_secret`, `cron_secret` va h.k.

## Qoidalar (Claude uchun bu repo bilan ishlaganda)

- **Build step qo'shma.** Bu static page. Next.js, React, Vue — kerak emas.
- **Yangi framework qo'shma** agar oson yechim bo'lmasa. Vanilla JS yetadi.
- **`levelup-bot` slugini o'zgartirma** — bu ichki edge function endpoint.
- **Secret'larni repo'ga tushirma** — `.env` yoki Supabase Vault'dan foydalaning.
- **Komment yozma** — nomlar o'zini aytadi.
- **Sahifa 2 formatda ishlaydi:** Telegram WebApp va oddiy brauzer. Har o'zgarishda ikkalasini tekshiring.
- **Admin faqat Zafar** hozir. Multi-admin rol tizimi keyin.

## Birodar hujjatlar

Platforma umumiy konteksti, biznes va yo'l xaritasi uchun:
- Admin paneldan tashqari **web platforma** (mentali.uz) hali qurilmagan — reja bor
- **Landing** — `Level_Up_Qisqa_Landing1.html` prototipi (boshqa yerda) — rebrand va deploy kutmoqda
- **Bot** — Supabase Edge Function `levelup-bot` (boshqa yerda)

## Prioritet — nimaga vaqt sarflash

Bu admin panelni mukammal qilish **1-prioritet emas**. Loyihada 0 foydalanuvchi bor. Prioritetlar:

1. **Birinchi 10 real foydalanuvchini botga olib kirish** (qo'lda, Instagram DM, tanishlar)
2. **Landing'ni deploy qilish** (trafik olish uchun)
3. **Web platforma MVP** (test yechish → natija → Pro sotish)
4. **Admin panel** — Supabase SQL console hozircha yetarli

Shu admin panelga katta refaktor qilishdan oldin — yuqoridagi 1-3 ustuvorligini eslang.
