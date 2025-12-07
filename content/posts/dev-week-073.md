+++
tags = ['Developer Log', 'AI', 'NovelFoundry']
title = 'Developer Week 073'
date = 2025-12-07T10:14:27+01:00
draft = false
+++

## NovelFoundry

### Frontend

Figured out how to setup GitHub actions to automatically deploy from my repo to the frontend sever, and wrote up an article for anyone else who'd like to do it too: [GitHub Actions Auto Deploy via FTPS to Namecheap (cPanel)](https://pbrazeale.github.io/posts/github-actions-ftps-deploy/) a huge thank you to [Sam Kirkland](https://github.com/SamKirkland/FTP-Deploy-Action) who made the code I'm using to make all this happen within GitHub.

Created an automatic sitemap.xml generator, and tied it into the GitHub Actions to automatically build and deploy when the stie is updated.

Separated the frontend into two servers. The marketing website and the application.

Implemented the basics of CI/CD via GitHub Actions for the application layer. Update both the application and main website to notify me via email whenever the build fails with notes.

### Backend

Setup the initial backend sever with a hostinger VPS. Went with Ubuntu 24.04 LTS and then installed [[Dokploy]] and setup an A record to access Dokploy with a domain name rather than an ip address. Enabled HTTPS and updated my password.

Huge shoutout to [Dreams of Code](https://youtu.be/ELkPcuO5ebo) for bringing this option to my attention, and a brilliant tutorial.

Dokploy not only makes managing and deploying my Docker apps easy. In short it converts my VPS into a self-hosted PaaS. It's also replacing the original design around NGINX by managing Traefik. Traefik is now my edge reverse proxy + TLS terminator + load balancer all in one easy to use platform.

#### Application Layer

Moved the actual application to the backend on Dokploy and spin up instances with docker. Dokploy handles the CI/CD when PRs are merged into main on GitHub; rather clean design, and the setup was easy enough.

NGINX is back to handle the web traffic within the container.

### Database

Designed the schemas and setup all the tables on Supabase. Created the rules for RLS (row level security), and integrated profile. Stage one of authentication is done.

##### NOTE:

> When testing JWT be sure to select "Disable cache" and reload when testing updates.

## Books

[The NGINX Handbook by Farhan Hasin Chowdhury](https://www.freecodecamp.org/news/the-nginx-handbook/) **DONE** (5/5)
