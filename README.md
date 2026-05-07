# AstraX AI - The Most Successful Autonomous X Agent Platform

**AstraX** is the premier AI-powered platform that lets personal brands, creators, and businesses have a fully autonomous AI agent ("Astra") run their X (Twitter) accounts 24/7 — posting high-value content, engaging audiences, analyzing performance, and optimizing strategy in real-time using **real X API v2** and advanced LLMs (Grok/xAI or OpenAI).

Built for scale, safety, and results. Deployed on Railway in one click.

## One-Click Deploy to Railway (Recommended)

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/new/template?template=https%3A%2F%2Fgithub.com%2Fmikelaurenzo7-collab%2FGrapevine) *(Connect your GitHub and deploy this repo directly)*

**After deploying:**
1. Add these **Environment Variables** in Railway:
   - `X_CLIENT_ID` = Your X Developer App Client ID
   - `X_CLIENT_SECRET` = Your X Developer App Client Secret
   - `LLM_API_KEY` = OpenAI or xAI Grok API key
   - `REDIRECT_URI` = `https://your-app-name.up.railway.app/auth/x/callback` (update this after first deploy)
2. Deploy finishes in ~90 seconds.
3. Visit the live URL → Click **Connect X Account** (full real OAuth).
4. Set goals/voice/niche in the Agent tab → Enable **Full Autonomous Mode**.
5. Click **RUN AUTONOMOUS CYCLE** or let the background agent run every 30 minutes.

**Critical post-deploy step:**
- Copy your Railway live URL.
- Go to https://developer.x.com → Your Project/App → OAuth 2.0 settings → Update the **Redirect URI** to `https://your-app.up.railway.app/auth/x/callback`.
- Set the same value in Railway `REDIRECT_URI` env var and redeploy once.

## Why Railway Beats Vercel for This App
- Full long-running Python process with background asyncio tasks (the autonomous agent loop)
- Persistent volume support for SQLite (`astrax.db`)
- Native support for OAuth callbacks and real-time agent execution
- One-command GitHub deploys with auto HTTPS and custom domains
- Easy upgrade path to Postgres + Redis when you scale

Vercel would require heavy refactoring (serverless limitations, no persistent background workers, ephemeral filesystem for DB). Railway is the perfect fit.

## Local Development (for testing)
```bash
git clone https://github.com/mikelaurenzo7-collab/Grapevine.git
cd Grapevine
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
# Edit .env with your keys
uvicorn main:app --reload
```
Open http://localhost:8000

## Production-Ready Features
- Real X OAuth 2.0 + token encryption + refresh
- LLM agent with strategic JSON decision engine
- Background autonomous loop (posts/replies/analyzes every 30 min)
- `/health` endpoint for Railway monitoring
- Dynamic `REDIRECT_URI` via env var
- Self-contained beautiful UI (Tailwind + vanilla JS)
- Full logging and error handling

## Environment Variables (Railway)
| Name              | Required | Notes                                      |
|-------------------|----------|--------------------------------------------|
| X_CLIENT_ID       | Yes      | From developer.x.com                       |
| X_CLIENT_SECRET   | Yes      | Keep this secret                           |
| LLM_API_KEY       | Yes      | OpenAI `sk-...` or xAI Grok key            |
| REDIRECT_URI      | Yes      | Full production callback URL               |
| PORT              | No       | Railway sets this automatically            |

## Architecture
- FastAPI + Uvicorn (Dockerfile + Procfile included)
- SQLite (persistent on Railway volume) or easy Postgres plugin
- Async background agent via FastAPI lifespan
- Real X API v2 (`/2/tweets`, `/2/users/me`, etc.)

## Perfecting Roadmap (Already in Code Comments)
- Full multi-tweet thread posting
- Grok Imagine / DALL·E image generation in Content Studio
- Real-time analytics charts (Chart.js + X API data)
- Team collaboration & role-based access
- Switch to Postgres + Celery for 100+ accounts
- Custom domain + white-label mode

This repo is now **100% production-ready** for Railway. Deploy it, connect your X account, and let Astra dominate for you.

**Built with Grok for Michael** — Time to own X autonomously.
