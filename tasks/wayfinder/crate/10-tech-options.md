---
id: 10
title: Which technical shapes fit on free tiers
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

What are the viable technical shapes (web/PWA, native, cross-platform) and free-tier stacks (backend, scheduled jobs, notifications, auth, realtime) for an asynchronous, turn-based social music game built and run by one person without paying for services?

_Context:_ Feeds the product-form decision and, later, the stack.

## Resolution

Resolved 2026-11-22 by crate-overnight #1 (research) and crate-session-2 (closing review). Findings: [research/tech-options.md](research/tech-options.md). Checked against its brief by the main session.

**Answer, in brief:**
- **PWA first:** no store fees (Apple 99 USD a year, Google 25 USD once) and no review friction; iOS Web Push works only once the web app is added to the Home Screen.
- **Web Push needs no vendor** (VAPID).
- **Free stacks that fit:** Supabase Free (50,000 MAU, 500 MB, pauses after a week idle) and Cloudflare Workers Free (100,000 requests a day, 5 cron triggers).
- **Out:** Firebase Spark (no scheduled functions), Vercel Hobby (non-commercial only), Fly.io (no free tier), Render Free (sleeps; database expires in 30 days).
- **Tightest free resource is email:** Resend 100 a day, Brevo 300 a day.
- **Avoid Sign in with Apple** (needs the paid programme); email magic links plus Google sign-in are free.
- **Never free:** Apple membership, a domain (about 12 USD a year), SMS.

**Still open:** Web Push on iOS 26 outside Home Screen apps; Cloudflare service terms; Netlify and Mailjet free tiers.
