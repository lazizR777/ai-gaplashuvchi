# 🔮 Jonli 3D fon · AI

3D animatsiyali jonli fon (shader nebula, zarrali shar, galaktika) va AI bilan ovozli muloqot.
AI foydalanuvchi qaysi tilda yozsa, o‘sha tilda javob beradi.

## Tarkib
```
public/index.html        — butun frontend (3D, UI, o‘yin elementlari)
lib/claude.js            — Claude API'ga so‘rov (kalit faqat serverda)
api/chat.js              — Vercel funksiyasi  (POST /api/chat)
netlify/functions/chat.js— Netlify funksiyasi
server.js                — lokal server (npm start)
```

## 1) Lokal ishga tushirish (Node 20.6+)
```bash
cp .env.example .env      # ichiga ANTHROPIC_API_KEY yozing
npm start                 # http://localhost:3000
```
API kalitni https://console.anthropic.com dan oling.

## 2) Deploy
**Vercel (tavsiya):** GitHub'ga yuklang → vercel.com → *Add New Project* → repo'ni tanlang →
*Environment Variables* ga `ANTHROPIC_API_KEY` qo‘shing → *Deploy*.

**Netlify:** repo'ni ulang → *Site settings → Environment variables* ga `ANTHROPIC_API_KEY` qo‘shing → Deploy.
(`netlify.toml` tayyor.)

**GitHub Pages:** faqat statik fayllarni ushlaydi, server funksiyasi yo‘q. Shunda backend'ni Vercel'ga
qo‘yib, `public/index.html` ichida asosiy `<script>` dan oldin quyidagini qo‘shing:
```html
<script>window.JF_API='https://SIZNING-LOYIHA.vercel.app/api/chat'</script>
```
va Vercel'da `ALLOWED_ORIGIN=https://FOYDALANUVCHI.github.io` o‘rnating.

## Muhim eslatmalar
- **API kalitni hech qachon `index.html` ga yozmang** — faqat environment variable sifatida.
- Har bir AI javobi API hisobingizdan pul yechadi. Himoya: bir IP uchun daqiqada 15 so‘rov
  (`RATE_LIMIT_PER_MIN`), javob 500 tokenga cheklangan. Bu oddiy himoya; jiddiy trafikda
  Vercel/Netlify rate-limit yoki Upstash kabi xizmat qo‘shing.
- Model: standart `claude-haiku-5-5` (tez va arzon). Kuchliroq javob uchun `ANTHROPIC_MODEL=claude-sonnet-5-5`.
- Ovoz brauzerning o‘z ovozlaridan tanlanadi (sifat qurilmaga bog‘liq). O‘zbekcha ovoz ko‘p qurilmada yo‘q —
  shunda turkcha ovoz ishlatiladi.
- Mikrofon (gapirib yozish) Chrome/Edge/Safari da ishlaydi va **HTTPS** talab qiladi.
- Xotira, daraja va vazifalar foydalanuvchi brauzerida (localStorage) saqlanadi.
- three.js CDN'dan yuklanadi (cdnjs). Oflayn kerak bo‘lsa, faylni `public/` ga yuklab, `<script src>` ni almashtiring.
# ai-gaplashuvchi
