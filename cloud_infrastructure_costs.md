# Infinity End-to-End System Costing (Hardware & Cloud)

This document provides a comprehensive breakdown of ALL fundamental expenses required to operate the Infinity SaaS platform, carefully segmented into **Physical Hardware Costs** (per new client deployment) and **Monthly Cloud Infrastructure** (server maintenance).

---

## 1. Hardware & Setup Cost (Per New Client Deployment)

Because the service acts as a complete solution provider, you incur these physical costs every time you sign up a new branch. These are one-time capital expenditures designed to be instantly offset by charging the client an upfront "Registration/Setup Fee".

**Estimated Physical Cost per Branch: `~₱3,500 to ₱5,000`**

- **Bluetooth Wireless Barcode Scanner:** `~₱1,000 to ₱1,500` (Available via wholesale on Shopee/Lazada; ensures the fast scan-driven workflow.)
- **IP Security Camera (CCTV):** `~₱1,500 to ₱2,000` (Smart IP cameras like Tapo C200 or Xiaomi 360 are ideal. This estimate includes the purchase of a 64GB MicroSD card for local backup recording at the store.)
- **Deployment Labor & Transportation:** `~₱1,000 to ₱1,500` (The physical labor constraint of traveling to their store to mount the camera and pair the Bluetooth scanner to their phone.)

*Business Strategy Reminder:* By charging a standard ₱7,500 upfront Registration Fee, you immediately recoup all hardware costs and earn a ~₱3,000 margin on day one before the monthly subscription even begins.

---

## 2. Cloud Infrastructure Overhead (Monthly Fixed Costs)

These are your monthly server bills to run the SaaS infrastructure for an MVP scale of **0 to 100 Active Business Branches** operating all day.

**Estimated Monthly Server Overhead: `~₱1,900 to ₱4,200`**

- **Web Hosting (Vercel/Next.js):** `₱0` (Free Tier) to `₱1,120` (Pro Tier). Hosts your high-tech Landing Page and the Admin Web Dashboard.
- **API Backend compute (NestJS on DigitalOcean App Platform):** `₱800 to ₱1,400`. Handles the core POS math, sync routing, and User Auth.
- **Central Database (Supabase PostgreSQL):** `₱1,400`. The lifeblood of the system. Stores all products, branches, receipts, and offline push queues safely with Row-Level Security.
- **In-Memory Cache (Redis):** `₱100`. Rate limits massive dashboard traffic so your main DB doesn't crash.
- **CCTV Video Routing (WebRTC/TURN server):** `₱300 to ₱1,100`. Required to bypass restrictive store internet routers and relay live video feeds directly to the owner's dashboard anywhere in the world.

---

## 💰 The Total Profit Margin

SaaS businesses thrive because server costs scale practically independently from revenue generation. 

- **Hard Cost to Onboard 1 New Client:** `~₱4,500`
- **Total Overhead to Host 50 Clients (Servers):** `~₱3,500 / month` 
- **Total Revenue from 50 Clients (at ₱1,499/mo):** `₱74,950 / month`

Once you install your first 3 branches, their combined monthly subscription comfortably covers all of your cloud computing bills. The remaining recurring payments act as nearly 95% pure compounding profit.
