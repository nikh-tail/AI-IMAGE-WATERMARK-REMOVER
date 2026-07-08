# Safelight — Watermark Remover

A small Next.js app: paste an image URL, it calls the Zyla Watermark Remover API
through a server-side route (so your API key never reaches the browser), and shows
a before/after slider with a download link.

## 1. Local setup

```bash
npm install
cp .env.example .env.local
# edit .env.local and paste your real Zyla API key
npm run dev
```

Open http://localhost:3000

## 2. Get a Zyla API key

1. Go to https://zylalabs.com and sign up
2. Subscribe to the "Watermark and Handwriting Remover API" (free tier available)
3. Copy your API key from the dashboard

## 3. Deploy to Vercel

**Option A — via GitHub (recommended)**
1. Push this folder to a new GitHub repo
2. Go to vercel.com → New Project → import that repo
3. In the project's Environment Variables settings, add:
   - `ZYLA_API_KEY` = your key
4. Deploy

**Option B — via Vercel CLI**
```bash
npm i -g vercel
vercel
# follow prompts, then:
vercel env add ZYLA_API_KEY
vercel --prod
```

## Notes

- The image you paste must be a public URL (not a local file) — the API fetches
  it directly.
- The returned `download_url` from Zyla is a temporary signed link — download the
  result if you want to keep it.
- The API key lives only in the serverless function (`pages/api/remove-watermark.js`),
  never sent to the browser.
