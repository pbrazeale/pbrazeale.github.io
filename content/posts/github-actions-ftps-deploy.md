+++
tags = ['NovelFoundry', 'CI/CD', 'Learning', 'Articles']
title = 'GitHub Actions Auto Deploy via FTPS to Namecheap (cPanel)'
date = 2025-12-02T11:14:27+01:00
draft = false
+++

## Overview

This guide sets up **automatic deployments** from GitHub → Namecheap shared hosting (cPanel) using **FTPS**.

Here’s the flow you’re building (and why it’s nice):

1. **You work on a feature branch** and open a Pull Request (PR) into `main`.
2. **PR is approved and merged** into `main`.
3. The merge triggers a **GitHub Actions workflow** that:
   - checks out your repo,
   - installs dependencies,
   - runs your build (example: `npm run build`) to produce `dist/`,
   - syncs `dist/` to your server via **FTPS** using SamKirkland’s deploy action.

If you enable **branch protection** for `main` (require PRs + approvals), then “merge PR to main” becomes the only way code reaches production (which prevents accidental deploys from random pushes).

[GitHub Branch Protection docs](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)

[GitHub Actions docs](https://docs.github.com/actions)

---

## What you’ll need

- A Namecheap shared hosting plan with **cPanel** access
- FTP/FTPS credentials (ideally a dedicated deploy user)
- A repo that builds into a static output folder (commonly `dist/` or `build/`)
- A GitHub Actions workflow file at `.github/workflows/deploy-to-namecheap.yml`

---

## 1) Get your Namecheap / cPanel FTP details

You’ll deploy over FTPS from GitHub → your cPanel account.

1. Log in to **Namecheap** → **Hosting List** → **Manage** on your hosting → open **cPanel**.
2. In cPanel, go to **FTP Accounts**:
   - Either use the **main account** credentials, or (recommended) create a **dedicated deploy user**.
   - If you create a deploy user, limit it to the directory you actually deploy to (more secure; less “oops I overwrote everything”).

### 1.1 What values to capture

You’ll store these as GitHub Secrets in the next step:

- **FTP host / server**
  - Often your domain (`example.com`) or a server hostname from Namecheap’s welcome email.
- **FTP username**
  - Use the exact value shown in cPanel.
- **FTP password**
  - Set or reset it in cPanel if needed.
- **Port**
  - FTP is commonly `21`.
  - **FTPS “Explicit”** is often also `21` (you connect on 21, then upgrade to TLS).
  - Some hosts also support **FTPS “Implicit”** (commonly `990`), but many shared hosts default to explicit FTPS.
- **Target directory (server path)**
  - This is the folder your website actually serves from:
    - Primary domain root is usually: `public_html/`
    - Subdomain is often: `public_html/subdomain/`
  - Confirm the exact folder in **cPanel → File Manager**.

> Important: `server-dir` is the #1 place first-time deploys go wrong.  
> If you deploy to the wrong folder, your workflow will be “green” but your site won’t change.

---

## 2) Add your FTP credentials as GitHub Actions Secrets

Never hard-code credentials in your workflow; use **encrypted secrets** instead: [GitHub Actions Secrets](https://docs.github.com/actions/security-guides/using-secrets-in-github-actions)

In your GitHub repo:

1. Go to **Settings → Secrets and variables → Actions → New repository secret**
2. Create secrets like this (names are suggestions; the workflow below assumes these exact names):

- `FTP_SERVER` → `example.com`
- `FTP_USERNAME` → `deploy@example.com` (or whatever cPanel gives you)
- `FTP_PASSWORD` → your FTP password
- `FTP_PORT` → `21` (or your FTPS port)
- `FTP_SERVER_DIR` → `/` (or `/subdomain/`)

---

## 3) The deploy action we’ll use (SamKirkland/FTP-Deploy-Action)

We’ll use [SamKirkland/FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action), which syncs a local folder to your server over FTP/FTPS and only uploads changes.

Why this matters:

- It’s faster than “delete everything and re-upload.”
- It’s simple enough for shared hosting.
- It supports FTPS (what you want for encrypted credentials + content in transit).

---

## 4) Create the GitHub Actions workflow

Create this file in your repo:

> `.github/workflows/deploy-to-namecheap.yml`

This workflow triggers when a PR into `main` is **closed** and **merged** (not merely pushed). It also supports manual runs via the Actions UI.

```yaml
name: Deploy to Frontend Server

on:
  pull_request:
    types: [closed]
    branches: [ main ]

  workflow_dispatch:

jobs:
  build-and-deploy:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Use Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '22'

      - name: Install dependencies
        run: npm install

      - name: Build project
        run: npm run build

      - name: Deploy via FTPS
        uses: SamKirkland/FTP-Deploy-Action@v4.3.6
        with:
          server: ${{ secrets.FTP_SERVER }}
          username: ${{ secrets.FTP_USERNAME }}
          password: ${{ secrets.FTP_PASSWORD }}
          port: ${{ secrets.FTP_PORT }}
          protocol: ftps
          local-dir: dist/
          server-dir: ${{ secrets.FTP_SERVER_DIR }}
          log-level: standard
```

### 4.1 If your build output is NOT `dist/`

Some frameworks build to different folders:

- Create React App often uses `build/`
- Vite often uses `dist/`
- Next.js is not a static `dist/` by default (unless you export static output)

If your output folder differs, update:

- `local-dir: dist/` → `local-dir: build/` (or whatever your tool generates)

---

## 5) (Optional) Enable branch protection on `main`

This is the “no cowboy deployments” step.

In GitHub:

1. Repo **Settings → Branches**
2. Add a branch protection rule for `main`
3. Common settings:
   - Require a pull request before merging
   - Require approvals (1+)
   - Require status checks to pass (optional, but great once you add tests)

This ensures deployments happen through reviewable PRs instead of random pushes.

#### NOTE:

This requires extra steps if you're using a private repo and are not setup as an organization.

> Your rulesets won't be enforced on this private repository until you move to GitHub Team organization account

---

## 6) Test the pipeline end-to-end

Before trusting this with real users, do a quick smoke test.

### 6.1 Create a test PR

1. Make a small visible change (tweak text, add a badge, change a background color).
2. Commit it to a feature branch like: `feat/test-deploy`
3. Open a PR into `main`
4. Approve and **merge** the PR

### 6.2 Inspect the workflow run

1. Go to the repo’s **Actions** tab.
2. Click the **Deploy to Frontend Server** run created by your merge.
3. Check for:
   - `Checkout repository` succeeded.
   - `Install dependencies` and `Build project` succeeded.
   - `Deploy via FTP` logs showing uploaded / deleted files.

If something fails:

- Click into the failed step and read the log output.
- Fix the issue (wrong path, missing secret, etc.), commit, and repeat the PR process.

---

## 7) Verify the deployment on Namecheap

Once the workflow run is green:

1. Open your site: `https://yourdomain.com` (or the subdomain)
2. Confirm your test change is visible

If you don’t see it:

- Hard refresh: **Ctrl+Shift+R** (Windows) / **Cmd+Shift+R** (Mac)
- Try an incognito/private window
- If you use caching (Cloudflare / cPanel caching), purge the cache

### 7.1 If your site is in a subdirectory

Example: you want the app at `https://example.com/app/`

Then your server folder might be:

- `public_html/app/`

Make sure `FTP_SERVER_DIR` matches the real folder (and that the folder exists).
