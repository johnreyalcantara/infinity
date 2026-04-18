# Infinity Cloud Infrastructure & Cost Estimates (MVP Scale)

This document provides a breakdown of the estimated monthly server and cloud overhead required to run the Infinity SaaS backend for an MVP scale of **0 to 100 Active Business Branches** operating 12 hours a day.

---

## The Profit Margin Reality
SaaS business models are incredibly profitable because infrastructure scales at a fraction of revenue. 
With **just 2 regular customers** paying `₱1,500/month` (~$26 USD), you will completely generate enough revenue to pay the entire monthly server bill for your first 50 customers.

---

## 1. Web Hosting & Front-End 
**Estimated Cost: $0 - $20 / month**
- **Technology:** Vercel (Next.js) or Netlify.
- The Admin Dashboard and Landing Pages are statically optimized. 
- You safely run on Vercel's **Free Tier** until you breach heavy traffic, at which point Vercel Pro is a flat `$20/month`.

## 2. API Backend Compute (The Monolith)
**Estimated Cost: $14 - $25 / month**
- **Technology:** Render.com, DigitalOcean App Platform, or AWS Fargate.
- The NestJS backend handles authorization, syncing outboxes, and routing requests. A standard lightweight instance (1GB RAM, 1 CPU) easily handles the background transactions of 100 concurrent stores because syncing is asynchronous and lightweight.

## 3. Core Database (PostgreSQL)
**Estimated Cost: $15 - $25 / month**
- **Technology:** Supabase Pro or DigitalOcean Managed Postgres.
- Essential. This stores all tenants, products, tracking, and logs. It uses Row-Level Security (RLS). You cannot cut corners here; use a managed service that handles automated daily backups so you never lose your clients' sales data.

## 4. In-Memory Cache (Redis)
**Estimated Cost: $0 - $5 / month**
- **Technology:** Upstash (Serverless Redis).
- Caches JWT sessions, rate limits, and buffers massive dashboard traffic. Upstash charges per command request. For 100 stores, usage typically falls well within the free tier or mere single-digit dollars.

## 5. CCTV Video Routing (TURN Servers)
**Estimated Cost: $5 - $20 / month**
- **Technology:** WebRTC Peer-to-Peer (Twilio Network / Metered TURN).
- **Architecture Trick to save money**: Video streaming uses massive bandwidth. Do **not** process video through your NestJS backend. Ensure the browser tries to connect to the store's IP Camera via Direct WebRTC (P2P). This costs $0. 
- Only if the store's internet router restricts P2P, a TURN relay server is used to bounce the video data. Typical Twilio metered rates for small bursts of CCTV checking (owners don't watch 24/7, they only peek at the dashboard) stays under $20.

---

## 💰 Total Estimated Monthly Cloud Overhead: ~$34 to $75 USD 
**Converted:** `~₱1,900 to ₱4,200` per month.

### Financial Summary
- **Monthly Revenue at 50 Branches:** `₱74,950`
- **Monthly Server Costs:** `~₱3,500`
- **Gross Software Margin:** `~95.3%`
