# BASECRUDE

This repository is a Next.js App Router project tracking real‑time commodity prices on the BASE network. It includes an integrated **CRUDE** chat assistant powered by the OpenAI API.

## Features

- $OIL and $GOLD price widgets
- Live X (formerly Twitter) feed and quick links
- Floating chat widget in the lower right corner with cute avatar
- Serverless backend (Next route handler at `app/api/chat/route.ts`) hides API keys
- CRUDE persona: witty global markets AI (no financial advice)
- Special response for "CA" or "$OIL" questions, returning the contract address and link.

## Setup

1. **Install dependencies**

   ```bash
   npm install
   # or yarn
   ```

2. **Environment variables**

   Create a `.env.local` (or set in Vercel dashboard) with:

   ```env
   OPENAI_API_KEY=sk-...   # keep this secret
   DEFAULT_MODEL=gpt-5-mini
   VERCEL_API_KEY=...     # if you need to perform Vercel operations programmatically
   ```

   > Do not commit `.env*` files. They are ignored by `.gitignore`.

3. **Run locally**

   ```bash
   npm run dev
   ```

   The chat widget will call `/api/chat` which proxies requests to OpenAI using the key from `process.env.OPENAI_API_KEY`.

4. **Deploy to Vercel**

   - `vercel` CLI or GitHub integration automatically detect the project.
   - If your repository has this app in a subfolder, set **Project Settings → Root Directory** to `BASECRUDE`.
   - Add the same environment variables in the Vercel dashboard (Settings → Environment Variables).
   - The `app/api/chat/route.ts` route handler will be deployed as a serverless function.

## Vercel deployment checklist

- **Root Directory:** `BASECRUDE`
- **Framework Preset:** `Next.js`
- **Install Command:** `npm install`
- **Build Command:** `npm run build`
- **Required env vars:** `OPENAI_API_KEY`
- **Recommended env vars:** `DEFAULT_MODEL=gpt-5-mini`
- **Apply env vars to:** Production, Preview, Development
- **After changes:** click **Redeploy** on latest deployment

If Vercel shows `Couldn't find any pages or app directory`, the Root Directory is pointing to the wrong folder.

## Quick deploy

```bash
npm install && npm run build && vercel --prod --yes
```

5. **Usage**

   Click the circular icon in the bottom-right to open the CRUDE chat window. Ask any markets‑related questions; CRUDE will respond under 280 characters with a smart, meme‑aware tone. Avoid giving investment advice.

   If you ask **"what's your CA"** or mention **`$OIL`**, CRUDE returns the hard‑coded contract address and link.

## Customization

- Change the avatar by placing your transparent-background character PNG at `public/llm-icon.png` and adjusting the `<img>` size in `ChatWidget.tsx` (currently `w-12 h-12`).

- **OpenAI API key**: create an environment variable named `OPENAI_API_KEY` with your secret (e.g. `sk-…`). On Vercel add it via the dashboard under *Settings → Environment Variables*; locally use a `.env` file or your shell. This keeps the key private and out of the repo.
- Adjust the system prompt in `app/api/chat/route.ts` to tweak CRUDE's personality.

## Notes

- The OpenAI key is intentionally kept server‑side to avoid leaks.
- The front-end only communicates with our own `/api/chat` endpoint, never directly with OpenAI.

> **Disclaimer:** CRUDE is a fun demonstration and never provides financial advice. Always do your own research.
