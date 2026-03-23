# Locus Budget Broker

A Telegram agent that keeps teams from overspending on pay-per-use APIs. It quotes the Locus wrapped Email Reputation call, enforces spend policies (allowance + reserve), asks for explicit approval, pays via the Locus wallet (`0xdf17…cdaf`), and logs every action.

## Features
- `/check email@example.com` → plan + approval prompt
- Balance check + reserve buffer before every paid call
- Locus wrapped API invocation (`/api/wrapped/abstract-email-reputation/check`)
- JSONL audit log with intent, wallet, cost, and summaries
- Architecture/safety brief, proof bundle, submission pack

## Quickstart
```bash
cp .env.example .env
# Fill TELEGRAM_BOT_TOKEN + LOCUS_API_KEY (+ optional AUDIT_LOG_PATH)
npm install
npm run dev
```
Then, in Telegram, send `/check someone@example.com` and tap **Approve**.

## Demo Website
## 24/7 Bot Hosting
**Render worker (one-click):** connect this repo, keep `render.yaml`, and Render will spin a Node worker with `npm run dev`. Set `TELEGRAM_BOT_TOKEN` + `LOCUS_API_KEY` in the Render dashboard.

**Self-hosted PM2:**
``
cp .env.example .env  # fill secrets
npm install
npx pm2 start npm --name locus-broker -- run dev
pm2 save && pm2 startup
``
This keeps the bot alive through reboots on any VPS.

A lightweight static landing page lives under `website/`. Deploy it to Vercel/Netlify or test locally with `npx serve website`. It summarizes the agent, key features, and links to the Telegram bot before visitors hop into chat.

## Repo Layout
- `src/index.ts` — Telegraf bot + Locus client
- `docs/` — architecture plan, proof bundle, submission copy, skill references
- `data/locus-audit-log.jsonl` — append-only audit log
- `assets/` — SVG/JPG hero + logo

## Proof Checklist
- Wallet: `0xdf17b4c0394ef7f231e1db629018a1189ff9cdaf` on Base (funded via gift code `b8484ca4-f2d6-45f8-bf7f-fdb0ef6ec79b` → tx `0x8fbf…95dfb`).
- Wrapped API spend recorded (balance 10 → 9.994 USDC) with JSON log + Telegram transcript.
- Docs ready for Synthesis submission: `docs/locus-submission.md` (story), `docs/locus-proof.md` (evidence).
