+++
tags = ['NovelFoundry', 'AI', 'Build Notes', 'Python', 'SaaS', 'API', 'JavaScript', 'Litestar']
title = 'SARAH UI Redesign'
date = 2025-09-19T20:30:07+01:00
draft = false
+++

## New Site Design

![Sarah Hero](https://pbrazeale.github.io/images/SARAH_hero_page.jpg)
I'm ashamed to admit this took two days, and over two hours was just me figuring out how to get the Hero image to align with the content and fade just right. Eventually I threw in the towel, and chose to handle the alignment question by manually exporting the image to the exact pixel dimension I wanted. I don't think that's the best approach, but it does mean that I'll not waste resources loading an image larger than needed, so there's that.

---

## SARAH V2 Build: Platform Pragmatism Done Right

SARAH V2 leaned hard into simplicity—flat UI up front, typed Python under the hood.

The end result?

A tight, fast dev loop and a deploy pipeline that just works on any Platform as a Service (PaaS). Nothing fancy unless it has to be.

### Core Tech Stack (Built for Speed)

- **Frontend:** I built out a dead-simple HTML/CSS/JS frontend in `frontend\`, powered by a micro `app.js`. In prod, I’ll hook auth and session handling through Supabase JS; for local/dev, I’m dropping in a fallback using API-issued JWTs (JSON Web Tokens). No extra dependencies are needed during development.
- **API:** Used Litestar in `api\src\app.py`. Clean, typed, minimal. Pydantic handled the schema contracts. I tuned CORS (Cross-Origin Resource Sharing) via `CORS_ORIGINS`.
- **Auth:** Went with a dual-path setup. Supabase Auth (Google or email/pass) + JWT verification through JWKS (JSON Web Key Set) will be used in prod. For dev, I used Argon2id to hash passwords and HMAC-signed JWTs for session tokens. Gave me speed during iteration without needing full infra.
- **Data:** Wired storage through Supabase Postgres using a small client wrapper. During dev, artifacts land in a local `working_dir`; swapping to S3 or Supabase Storage in prod will be straightforward.
- **Payments:** Stubbed in Stripe. Checkout and webhook endpoints are basic but live. Entitlement logic is modular and staged for future expansion.
- **Extensibility:** Heavy optional packages like `python-docx` and OpenAI/OpenRouter helpers are lazy-loaded under the `process\...` routes. If a dependency’s missing, the API still boots cleanly. No breakage!

### Deploying on a PaaS (Platform as a Service)

- **Split Deploy Strategy:** 
    - The frontend will deploy as static assets on Vercel.
    - The backend lives in a containerized dyno (Suitable for Railway, Render, or Fly.io).
    - The full app serves from `uvicorn api.src.app:app`.
- **Environment Vars:** 
    - These get injected via the platform:
      - `SUPABASE_URL`
      - `SUPABASE_SERVICE_ROLE_KEY`
      - `JWT_JWKS_URL` (for prod)
      - `JWT_SECRET` (for dev/fallback)
      - `STRIPE_SECRET_KEY`
      - `STRIPE_WEBHOOK_SECRET`
      - `CORS_ORIGINS` for the frontend origin
- **Frontend Config:** I ignored `frontend\config.js` in version control. At deploy, I'll inject it via CI or render it from env vars to keep secrets clean and environment-specific.
- **Webhooks:** Wired `/stripe/webhook` to the public PaaS endpoint. For local testing, I’ll use an ngrok tunnel. Once everything routes through a verified endpoint, I’ll be good to go.
- **Disk Handling:** Used local disk in dev. In prod, the `working_dir` will route to S3 (though Supabase Storage is another option). Either path works without needing refactors.
- **Scaling:** The API is stateless—sessions handled via JWTs—so horizontal scaling is trivial. Any heavier jobs can run in a worker process, following the same routes.

### Dev Workflow (Streamlined for Iteration)

- **One-Command Launch:** Ran everything with `python api\run.py` for the backend, and served the frontend through a basic static server. Low overhead from zero to live.
- **Guardrails First:** Typed models, clean routers, strict env var boundaries. Added a ‘auth/dev-login` route to keep testing frictionless.
- **Security Strategy:** Started with permissive CORS and HMAC JWTs (symmetric). Once deployed, I’ll flip it to JWKS (asymmetric) with locked-down CORS for security.

### Outcomes

The result is a lean, modular, stack. Static UI + typed API, designed for scalability and easy maintenance.

Clean path from dev to PaaS, no overengineering needed.

First SaaS launch scheduled for mid October!
