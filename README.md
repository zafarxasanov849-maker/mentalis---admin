# Mentalis — admin panel

Milliy Sertifikat (MS) imtihoniga tayyorgarlik platformasining admin paneli. Telegram bot [`@mentaliss_bot`](https://t.me/mentaliss_bot) uchun orqa ofis.

## Kirish

Faqat bot `admin_ids` ro'yxatidagi Telegram ID'lar kira oladi. Ikki yo'l, ikkalasi ham bot ichidagi `/admin` buyrug'idan:

- **Telegram Mini App** — "Panelni ochish" tugmasi panelni Mini App sifatida ochadi. Server har so'rovda Telegram'ning imzolangan `initData`sini tekshiradi.
- **Oddiy brauzer (Chrome)** — "Brauzerda ochish" bir martalik havola (10 daqiqa ishlaydi). Ochilsa, 30 kunlik brauzer sessiyasi yaratiladi. Yuqori paneldagi "Chiqish" tugmasi joriy yoki barcha brauzerlarda sessiyani yopadi. Server faqat token hashlarini saqlaydi.

## Sahifalar

- **Statistika** — asosiy metrikalar
- **Savollar**
  - Kun savollari (bot kunlik yuboradi)
  - Pro savollar (web platforma uchun — variant yoki yozma javob, qiyinlik, rasm; qo'shish/tahrir + Excel import)
- **Bot matnlari** — har bot xabarini live preview va versiya tarixi bilan tahrir
- **Sanalar** — rejalashtirish va eslatmalar uchun imtihon va ro'yxat sanalari

## Texnik

- **Sahifa:** bitta static `index.html`
- **Hosting:** GitHub Pages
- **API:** Supabase Edge Function `levelup-bot` → `/admin`
- **Savol rasmlari:** `q-images` private bucket, qisqa muddatli signed URL
- **Repo'da hech qanday secret yo'q**

## Demo rejim (Telegram'siz)

Dizaynni ko'rish uchun:

- `index.html?demo=1` — faqat soxta ma'lumot bilan UI
- `index.html?demo=1&web=1` — brauzer akkaunt menyusi bilan

Demo rejimida hech narsa saqlanmaydi.
