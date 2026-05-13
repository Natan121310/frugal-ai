# Frugal AI

A chat interface that auto-optimizes every prompt before sending to Claude — same answers, fewer tokens, lower cost.

## Deploy to Vercel in 3 steps

### Step 1 — Get your Anthropic API key
1. Go to https://console.anthropic.com
2. Click **API Keys** → **Create Key**
3. Copy it somewhere safe

### Step 2 — Deploy to Vercel
**Option A: GitHub (recommended)**
1. Push this folder to a GitHub repo
2. Go to https://vercel.com → **New Project** → import your repo
3. Click **Deploy** (no build settings needed)

**Option B: Vercel CLI**
```bash
npm i -g vercel
cd frugal-ai
vercel
```

### Step 3 — Add your API key as an environment variable
1. In your Vercel project dashboard → **Settings** → **Environment Variables**
2. Add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** your key from Step 1
3. Click **Save**, then go to **Deployments** → **Redeploy**

That's it. Your app is live at `your-project.vercel.app`.

---

## Project structure

```
frugal-ai/
├── api/
│   └── chat.js        ← serverless proxy (hides your API key)
├── public/
│   └── index.html     ← the full frontend
├── vercel.json        ← routing config
└── package.json
```

## How it works

Every message goes through a 2-step pipeline:
1. **Optimize** — a fast Haiku call strips filler and compresses your message
2. **Answer** — the lean prompt goes to Claude, which answers it

The proxy (`/api/chat.js`) sits between the browser and Anthropic's API so your key is never exposed to the client.

## Customization

- **Change the model**: edit `MODEL` in `public/index.html` (line ~3 of the script)
- **Adjust max tokens**: change `maxTokens` in the `callProxy` calls
- **Use a different optimizer model**: edit the `callProxy` call in `think-opt` step
