# Technical shapes and free-tier stacks for an async music game

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [Which technical shapes fit on free tiers](../10-tech-options.md)

Method: pages were read as raw HTML from each vendor's own site on 2026-11-22. "Page date" is the date the page itself shows (a "last updated" line or a `dateModified` field); "none shown" means the page shows no date. Marked **not verified** where a primary page could not be read. "(inference)" marks my own reasoning, not a source claim.

Sizing assumption used for "first limit that bites": 50 leagues x 10 players = about 500 players, one round per league per week, deadlines clustered on the same weekday evening (inference; the ticket gives no traffic model).

## Answer

- **A PWA is viable and costs nothing in store fees.** The Apple Developer Program is [99 USD per membership year](https://developer.apple.com/programs/whats-included/); Google Play is a [US$25 one-time fee](https://support.google.com/googleplay/android-developer/answer/6112435). Native adds review friction: Apple guideline 4.2 says an app must [elevate "beyond a repackaged website"](https://developer.apple.com/app-store/review/guidelines/), and Google requires new personal accounts to run a [closed test with at least 12 testers for 14 days](https://support.google.com/googleplay/android-developer/answer/14151465) before production.
- **iOS Web Push works only for Home Screen web apps.** [WebKit, iOS 16.4](https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/): a web app "added to the Home Screen" can ask for push permission, and only after a direct user action such as tapping a button. The permission cannot be requested from a plain Safari tab (no source says otherwise; for iOS 26 not verified). Since iOS 26 every site added to the Home Screen [opens as a web app by default](https://webkit.org/blog/16993/news-from-wwdc25-web-technology-coming-in-safari-26-beta/), which helps the install flow. iOS 18.4 added [Declarative Web Push](https://webkit.org/blog/16535/meet-declarative-web-push/), which needs no service worker.
- **Standard Web Push needs no vendor.** It uses VAPID keys and the browser's push service; [Firebase's own FCM web guide](https://firebase.google.com/docs/cloud-messaging/js/client) describes the same VAPID mechanism, and [MDN lists the Push API as Baseline since March 2023](https://developer.mozilla.org/en-US/docs/Web/API/Push_API). You can send it from your own backend for free (inference: the encryption can run in any runtime with WebCrypto).
- **Firebase Spark cannot run the game's clock.** [Cloud Functions are "Not applicable" on Spark](https://firebase.google.com/pricing), and [deploying functions requires Blaze](https://firebase.google.com/docs/functions/get-started); [scheduled functions are billed](https://firebase.google.com/docs/functions/schedule-functions) (Cloud Scheduler: 3 jobs free per Google account). Phase changes and reminders need an external scheduler or a card on file.
- **Supabase Free and Cloudflare Free are the two stacks that fit.** Supabase Free: [50,000 MAU, 500 MB database, 5 GB egress, paused after 1 week of inactivity, 2 active projects](https://supabase.com/pricing). Cloudflare Workers Free: [100,000 requests/day, 10 ms CPU, 5 Cron Triggers per account](https://developers.cloudflare.com/workers/platform/limits/), plus [free, unlimited static asset requests](https://developers.cloudflare.com/workers/platform/pricing/).
- **Vercel Hobby is out.** Its [terms](https://vercel.com/legal/terms) say: "You shall only use the Services under a Hobby plan for your personal or non-commercial use." Fly.io has [no free tier](https://fly.io/docs/about/pricing/) for new organizations. Render Free web services [spin down after 15 minutes and Free Postgres expires 30 days after creation](https://render.com/docs/free).
- **Email is the tightest free resource.** Supabase's built-in mail is [2 messages per hour](https://supabase.com/docs/guides/auth/auth-smtp). Resend Free is [100 emails/day and 3,000/month](https://resend.com/docs/knowledge-base/account-quotas-and-limits). Brevo Free is [up to 300 emails per day](https://www.brevo.com/pricing/). Cloudflare's own email sending to arbitrary recipients [needs Workers Paid](https://developers.cloudflare.com/email-service/platform/pricing/).
- **Sign in with Apple needs the paid program, also on the web.** [Supabase's docs](https://supabase.com/docs/guides/auth/social-login/auth-apple) say an "Apple Developer account" is required, and the web flow needs a Services ID plus a client secret that must be regenerated every 6 months. Email magic links plus Google sign-in avoid this cost.
- **Never free:** an Apple membership (99 USD/year), a domain (`.com` [from $11.81](https://porkbun.com/products/domains), no date shown), SMS (Firebase phone auth is [not available on Spark](https://firebase.google.com/pricing)), and a sending-capable email volume beyond a few hundred per day.

## 1. Form: web/PWA, native, cross-platform

| Form | Cost to ship | Friction | Fit for this game (inference) |
|---|---|---|---|
| Responsive web + PWA | 0 (domain optional) | Users install via browser; iOS needs "Add to Home Screen" for push | Best: no review, instant updates, one codebase |
| Native iOS | [99 USD/year](https://developer.apple.com/programs/whats-included/) | App Review; [4.2 Minimum Functionality](https://developer.apple.com/app-store/review/guidelines/) | Only needed for reliable push or store discovery |
| Native Android | [US$25 once](https://support.google.com/googleplay/android-developer/answer/6112435) | [12 testers x 14 days closed test](https://support.google.com/googleplay/android-developer/answer/14151465) for personal accounts created after 2023-11-13 | Android PWA covers most needs |
| Cross-platform (Expo/React Native, Capacitor, Flutter) | Store fees above; framework prices **not verified** (EAS and similar build services not checked) | Same store review as native | Wraps the same web app; pays off only if push on iOS is a must |

**What a PWA can do on iOS in 2026**
- Home Screen web apps exist since iPhone OS 2.1 and, in iOS 26, [every website added to the Home Screen opens as a web app unless the user turns off "Open as Web App"](https://webkit.org/blog/16993/news-from-wwdc25-web-technology-coming-in-safari-26-beta/) (WebKit, Safari 26 beta post; page date not shown in text).
- Web Push, Notifications API and Badging API arrived in [iOS 16.4 for Home Screen web apps](https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/). Permission must be requested "in response to direct user interaction". Notifications integrate with Focus modes.
- [Declarative Web Push](https://webkit.org/blog/16535/meet-declarative-web-push/) (iOS 18.4, macOS 15.5 beta at time of the post) lets Safari show a notification from a standard JSON payload without running a service worker. The sender must use the declarative JSON format. It is backward compatible with classic Web Push.
- Third-party iOS browsers can also add sites to the Home Screen since 16.4 (same WebKit post). On iOS all of them use WebKit; the web app is still a WebKit web app (see EU below).
- The user must take two steps (Add to Home Screen, then enable notifications). This is the main product risk for reminder reach on iOS (inference).

**EU / DMA.** In February 2024 Apple said iOS 17.4 would remove Home Screen web apps in the EU; on 2024-03-01 it reversed: Apple "will continue to offer the existing Home Screen web apps capability in the EU", built directly on WebKit. Source is secondary, quoting Apple's statement in full: [9to5Mac, 2024-03-01](https://9to5mac.com/2024/03/01/apple-home-screen-web-apps-ios-17-eu/). Apple's current [EU changes page](https://developer.apple.com/support/dma-and-apps-in-the-eu/) no longer mentions web apps, so the primary statement was **not verified** on the live Apple site; the 2026 EU state is not confirmed beyond the 2024 reversal.

**Android.** The Push API is Baseline ([MDN](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)) and installability criteria are described on [web.dev](https://web.dev/learn/pwa/installation) (it notes Safari on macOS does not support installability). Android Chrome install-prompt details and Android push behaviour were not read page by page; **not verified** beyond these two pages.

**Chat-platform app shape.** A Telegram or Discord front end is not a full replacement for the UI; see section 2 for them as notification channels. Telegram Mini Apps and Discord Activities were not researched (outside the listed scope).

## 2. Reminders and notifications

| Channel | Free? | Hard limits | Pauses? | Commercial OK? | Source | Page date |
|---|---|---|---|---|---|---|
| Web Push (VAPID, own backend) | Yes, no vendor | Needs HTTPS, service worker (or Declarative Web Push on iOS 18.4+); iOS only from Home Screen | n/a | No vendor terms apply | [FCM web guide](https://firebase.google.com/docs/cloud-messaging/js/client), [WebKit](https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/) | 2026-11-18 (Firebase page) |
| Firebase Cloud Messaging | "No-cost", no numeric limits listed | Needs a sender: Functions need Blaze, or send from any server with the Admin SDK (inference) | No | Not checked | [Firebase pricing](https://firebase.google.com/pricing) | none shown |
| OneSignal Free | Free plan exists; Web Push line reads "Max 10,000 subscribers per send" | Free-plan web push limits **not verified** (rendered table was ambiguous); Free email: "10,000 sends / month" | Not stated | Not checked | [OneSignal pricing](https://onesignal.com/pricing) | none shown |
| Resend Free | 100/day, 3,000/month (sent and received count) | 3 custom domains; daily quota resets 00:00 UTC; over-quota sends return 429 and are not queued | No | Not checked | [Resend quotas](https://resend.com/docs/knowledge-base/account-quotas-and-limits) | none shown |
| Brevo Free | "up to 300 emails per day" | Account needs approval before sending | No | Not checked | [Brevo pricing](https://www.brevo.com/pricing/) | none shown |
| Postmark Developer | 100 emails/month, "never expires" | Test-level only | No | Not checked | [Postmark pricing](https://postmarkapp.com/pricing) | none shown |
| Amazon SES | No permanent free tier on the page; new AWS accounts get up to $200 credits, free plan lasts 6 months | After that $0.10 per 1,000 emails | Credits expire | Not checked | [SES pricing](https://aws.amazon.com/ses/pricing/) | none shown |
| Mailjet | **Not verified** (page would not load) | | | | | |
| Cloudflare Email Service | Sending to arbitrary recipients needs Workers Paid ($5/month minimum); 3,000/month included then $0.35 per 1,000; inbound Email Routing is free | Free plan can only send to verified addresses of your own account | n/a | n/a | [Cloudflare email pricing](https://developers.cloudflare.com/email-service/platform/pricing/) | 2026-06-09 |
| Telegram Bot API | Free | About 1 message/second per chat, about 30 messages/second bulk; above that needs paid broadcasts (0.1 Stars per message, 100,000 Stars balance required) | No | Not checked | [Telegram bot FAQ](https://core.telegram.org/bots/faq) | none shown |
| Discord webhooks | Free | Rate-limited per route; "If a webhook returns a 404 status you should not attempt to use it again" | No | Not checked | [Discord rate limits](https://discord.com/developers/docs/topics/rate-limits) | none shown |

Notes:
- Telegram users start a bot with a `/start` Start button ([Telegram bot features](https://core.telegram.org/bots/features)); bots cannot be assumed to message users who have never opened them (inference from this flow; the sentence itself was not found). Deep links can connect a Telegram account to a game account (same page).
- A Discord webhook posts to a channel, not to a person. Per-user DMs need a bot account (not researched).
- At about 500 players, a deadline-eve reminder to everyone by email exceeds Resend Free's 100/day (inference). Use push first, email as fallback for a few, or batch across days.
- APNs direct is not an option on a PWA path: iOS Web Push goes through Apple's push service transparently via the standard Web Push protocol. APNs tokens are for native apps and need the paid membership (inference).

## 3. Backend free tiers

Dates are the page date shown on the page, or "none shown".

| Vendor | What is free | Hard limits and gotchas | Pauses idle? | Commercial use | Source | Page date |
|---|---|---|---|---|---|---|
| Supabase Free | Postgres, Auth, Storage, Realtime, Edge Functions, pg_cron | "50,000 monthly active users", "500 MB database size", "1 GB file storage", "5 GB egress", "Limit of 2 active projects", "500,000" Edge Function invocations, Realtime "200" concurrent connections and "2 Million" messages/month | Yes: "paused after 1 week of inactivity"; paused projects do not count toward the 2 | No ban found in the [terms](https://supabase.com/terms) (searched for "commercial"; only "commercially reasonable" appeared) | [pricing](https://supabase.com/pricing), [billing FAQ](https://supabase.com/docs/guides/platform/billing-faq) | none shown |
| Firebase Spark | Firestore, Auth, Hosting, FCM | Firestore 1 GiB, "20K document writes/day", "50K reads/day", "20K deletes/day", 10 GiB/month egress; Auth 50K MAU; Hosting 10 GB storage, 360 MB/day transfer; Functions and Cloud Storage "Not applicable" | No pause stated | Not verified (terms not read) | [pricing](https://firebase.google.com/pricing) | none shown (docs pages 2026-11-18) |
| Cloudflare Workers Free | Workers, static assets, Cron Triggers, KV, D1, Durable Objects (SQLite only), Queues | Workers: 100,000 requests/day, 10 ms CPU per request and per cron, 50 subrequests, 5 Cron Triggers per account, 100 Workers. Static asset requests free and unlimited | No | No ban found in the [Self-Serve Subscription Agreement](https://www.cloudflare.com/terms/) (Last Updated 2025-09-12); service-specific terms not read | [limits](https://developers.cloudflare.com/workers/platform/limits/), [pricing](https://developers.cloudflare.com/workers/platform/pricing/) | 2026-11-19 / 2026-11-18 |
| Cloudflare D1 (Free) | SQLite database | 5 million rows read/day, 100,000 rows written/day, 5 GB total, 10 databases; at the limit queries return errors until 00:00 UTC | No | as above | [D1 pricing](https://developers.cloudflare.com/d1/platform/pricing/) | none read |
| Cloudflare KV (Free) | Key-value | 100,000 reads/day, 1,000 writes/day, 1,000 deletes/day, 1,000 lists/day, 1 GB | No | as above | [KV pricing](https://developers.cloudflare.com/kv/platform/pricing/) | 2026-10-30 |
| Cloudflare Durable Objects (Free) | SQLite-backed only | 100,000 requests/day, 13,000 GB-s/day, 5 million rows read/day, 100,000 rows written/day, 5 GB; failing operations error out; resets 00:00 UTC | No | as above | [DO pricing](https://developers.cloudflare.com/durable-objects/platform/pricing/) | 2026-11-13 |
| Cloudflare Queues (Free) | Yes | 10,000 operations/day, 24 hour retention; about 3 operations per message | No | as above | [Queues pricing](https://developers.cloudflare.com/queues/platform/pricing/) | 2026-10-30 |
| Cloudflare Pages (Free) | Static hosting | 500 builds/month, 20,000 files, 25 MiB per file, 100 custom domains per project | No | as above | [Pages limits](https://developers.cloudflare.com/pages/platform/limits/) | 2026-11-19 |
| Vercel Hobby | Hosting, Functions | 1,000,000 function invocations, 100 GB Fast Data Transfer; over limit you "wait until 30 days have passed" | Projects can be disabled "with or without notice" | **No**: "personal or non-commercial use" only | [Hobby plan](https://vercel.com/docs/plans/hobby), [terms](https://vercel.com/legal/terms) | Fair-use page 2026-11-12 |
| Netlify Free | Hosting, Functions, Blobs, Netlify Database | 300 credits/month, hard limit, no auto recharge. Cost: production deploy 15 credits, bandwidth 20 credits/GB, web requests 2 credits/10k, compute 10 credits/GB-hour. Scheduled function availability on Free **not verified** | Hard stop at the limit | Terms silent; Netlify staff say allowed (secondary: [Netlify forum](https://answers.netlify.com/t/can-we-use-netlify-free-plan-for-commercial-purposes/41545), not opened directly). **Not verified** on a primary page | [pricing](https://www.netlify.com/pricing/), [credit plans](https://docs.netlify.com/manage/accounts-and-billing/billing/billing-for-credit-based-plans/credit-based-pricing-plans/) | none shown |
| Neon Free | Postgres only | 100 projects, "100 CU-hrs monthly per project", "1 GB of storage per project", up to 2 CU; scale to zero "After 5 minutes when inactive"; page also lists Managed Better Auth and 5 GB object storage in Free (reading of table) | Compute suspends, data stays | No ban found in [terms](https://neon.com/terms-of-service) (Last Updated 2026-10-14) | [pricing](https://neon.com/pricing) | none shown |
| Turso Free | SQLite (libSQL) | 100 databases, 5 GB, 500 million rows read, 10 million rows written per month | Not stated | Not checked | [pricing](https://turso.tech/pricing) | none shown |
| Render Free | Web services, static sites, Postgres, Key Value | Web service spins down after 15 min idle, about 1 minute to wake; 750 Free instance hours/month; Free Postgres "expire 30 days after creation"; ephemeral disk; SMTP ports blocked; no one-off jobs | Yes (15 min) | Page says "Do not use them for production applications" | [Render free](https://render.com/docs/free) | none shown |
| Fly.io | No free tier for new orgs | "$1 of credit ... lasts for 7 days"; bills under $5/month are waived; cheapest always-on machine $2.19 per 30 days; card required | n/a | n/a | [Fly pricing](https://fly.io/docs/about/pricing/) | none shown |
| Deno Deploy Free | Hosting, KV, cron | 1M requests/month, 20 GiB egress, 10 hr active CPU, 150 GiB-hr memory, KV 1 GiB, 1,000,000 KV reads, 500,000 KV writes; max 10 cron jobs per revision on free orgs | Idle apps scale to zero (about 20-30 s) | **Not verified** (terms page returned no text) | [pricing](https://deno.com/deploy/pricing), [cron docs](https://docs.deno.com/deploy/reference/cron/) | none shown |
| Appwrite Cloud Free | Auth, DB, Functions, Storage | Reaching a limit freezes the project (read-only console); numeric Free limits **not verified** (pricing page is script-rendered); docs call Free "perfect for personal hobby projects" | Not verified | Not verified | [pricing](https://appwrite.io/pricing), [free plan docs](https://appwrite.io/docs/advanced/platform/free) | none shown |
| Oracle Cloud Always Free + PocketBase | 2 AMD micro VMs (1 GB RAM each) or Arm A1 "2 OCPUs and 12 GB"; 200 GB block volume; "10 TB per month of outbound data" | Needs credit/debit card (no prepaid or virtual); idle instances "may be reclaimed" (7 days with 95th percentile CPU under 20%, network under 20%, A1 memory under 20%); accounts idle 30 days may be suspended; port 25 blocked | Reclaim risk is real for a lightly loaded game (inference) | Free Tier terms not read | [Always Free](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm), [Free Tier](https://www.oracle.com/cloud/free/) | none shown |

PocketBase itself: one executable with an embedded SQLite database and realtime subscriptions ([docs](https://pocketbase.io/docs/)). You run, back up and patch the server yourself (inference). Licence not checked.

Notes:
- Supabase acquired Turso: [Turso's announcement](https://turso.tech/blog/turso-is-joining-supabase) ("Turso ... is being acquired by Supabase"; press coverage puts the announcement on 2026-10-02). Neither side commits to future Turso pricing (secondary summary). Treat Turso Free terms as unstable.
- Neon's pricing page now also bundles Functions and Realtime (Beta), so it is no longer a database-only vendor.

## 4. Scheduled phase transitions

| Option | Free limits | Gotchas | Source | Page date |
|---|---|---|---|---|
| Cloudflare Cron Triggers | 5 per account; 10 ms CPU per cron run | New or changed triggers take up to 15 minutes to propagate; many games can share one trigger that sweeps all due rounds (inference) | [cron docs](https://developers.cloudflare.com/workers/configuration/cron-triggers/), [limits](https://developers.cloudflare.com/workers/platform/limits/) | 2026-11-18 |
| Supabase Cron (pg_cron) | Included in Free plan listings; "from every second to once a year"; recommend no more than 8 concurrent jobs, each under 10 minutes | Project must not be paused (1 week idle) or the clock stops | [Supabase Cron](https://supabase.com/docs/guides/cron) | "Updated Nov 17, 2026" |
| Supabase Edge Functions | 500,000 invocations; CPU 2 s; wall clock 150 s on Free | Outgoing ports 25 and 587 blocked (use an HTTPS email API) | [limits](https://supabase.com/docs/guides/functions/limits) | "Updated Oct 29, 2026" |
| Firebase scheduled functions | Not on Spark. Blaze required; Cloud Scheduler job $0.10/month, 3 jobs free per Google account | Needs a card | [schedule docs](https://firebase.google.com/docs/functions/schedule-functions) | 2026-11-18 |
| Deno cron | Free orgs: max 10 cron jobs per revision | Not verified for commercial terms | [Deno cron](https://docs.deno.com/deploy/reference/cron/) | none shown |
| GitHub Actions `schedule` | Shortest interval once every 5 minutes; can be delayed or dropped at high load (start of every hour); in public repos disabled after 60 days without repository activity | Usable as a free external clock for Firebase Spark; minutes quota for private repos not checked | [GitHub docs](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows) | none shown |
| Vercel Hobby cron | **Not verified** (usage page would not load); Hobby is non-commercial anyway | | | |
| Netlify scheduled functions | Listed as a function type; Free availability **not verified** | | [credit plans](https://docs.netlify.com/manage/accounts-and-billing/billing/billing-for-credit-based-plans/credit-based-pricing-plans/) | none shown |
| Render Free | No cron service among free types (only web, static, Postgres, Key Value) | | [Render free](https://render.com/docs/free) | none shown |

Design note (inference): store each round's deadline as a timestamp and compute the phase on read. Then the cron job is only needed to send reminders and close rounds for players who do not open the app, and one 5-minute sweep is enough.

## 5. Realtime (only for a live "listening night")

| Option | Free limits | Source | Page date |
|---|---|---|---|
| Supabase Realtime | 200 concurrent connections, 100 messages/second, 2 million messages/month, 256 KB max message | [pricing](https://supabase.com/pricing), [Realtime limits](https://supabase.com/docs/guides/realtime/limits) | "Updated Oct 29, 2026" |
| Cloudflare Durable Objects WebSockets | Free plan 100,000 requests/day (incoming WebSocket messages count at a 20:1 ratio for billing), 13,000 GB-s/day; use the WebSocket Hibernation API so idle sockets do not burn duration | [DO pricing](https://developers.cloudflare.com/durable-objects/platform/pricing/) | 2026-11-13 |
| Firebase (Firestore listeners) | Each document read counts against the 50K reads/day Spark quota (inference from the quota list) | [pricing](https://firebase.google.com/pricing) | none shown |
| Ably Free | Docs: "Includes 500 MAUs each month"; the pricing page slider text says "1K monthly active users"; discrepancy not resolved | [Ably packages](https://ably.com/docs/platform/pricing), [pricing](https://ably.com/pricing) | none shown |
| Pusher Sandbox | 200k messages/day, 100 concurrent connections | [Pusher pricing](https://pusher.com/channels/pricing/) | none shown |

A game with a 10-player league and a 1-hour live window sits well under these caps (inference). Realtime is not needed for the core async loop: push plus refetch is enough.

## 6. Auth

| Option | Free | Notes | Source |
|---|---|---|---|
| Supabase Auth | 50,000 MAU; social OAuth providers, anonymous sign-ins, custom SMTP included in Free | Built-in email is "2 messages per hour"; raise it only with custom SMTP (starting limit 30/hour, adjustable). Auth rate limit config default `rate_limit_email_sent: 10` in the example | [pricing](https://supabase.com/pricing), [SMTP](https://supabase.com/docs/guides/auth/auth-smtp), [rate limits](https://supabase.com/docs/guides/auth/rate-limits) |
| Firebase Auth | "No-cost up to 50K MAUs"; SAML/OIDC 50 MAU; phone auth not on Spark | Email link sign-in requires the Email provider and email/password enabled | [pricing](https://firebase.google.com/pricing), [email link](https://firebase.google.com/docs/auth/web/email-link-auth) |
| Clerk Hobby | Free, "50,000 MRU limit per app", custom domain | "Fixed, 7 day session lifetime" on Hobby | [Clerk pricing](https://clerk.com/pricing) |
| Better Auth (self-hosted) | Open source TypeScript framework; plugins incl. passkey | You run it; email still needs a sender | [Better Auth](https://www.better-auth.com/docs/introduction), [passkey plugin](https://www.better-auth.com/docs/plugins/passkey) |
| Auth.js | **Not verified** (not opened) | | |

Details:
- **Sign in with Apple.** Needs an Apple Developer account for the capability; the web flow also needs a Services ID and a signing key, and "Apple requires you to generate a new secret key every 6 months" ([Supabase docs](https://supabase.com/docs/guides/auth/social-login/auth-apple)). Native-only setups skip the rotation. So the web version is not free: 99 USD/year (inference from the account requirement plus [the program fee](https://developer.apple.com/programs/whats-included/)).
- **App Store rule 4.8.** If a native app offers a third-party or social login (Google, for example), it must also offer an equivalent login service with the features listed in [4.8](https://developer.apple.com/app-store/review/guidelines/). Email-only login sidesteps this (inference).
- **Google sign-in.** Offered as a social provider on Supabase Free (pricing page "Social OAuth providers: Included in free") and in Firebase Auth. Console fees not checked.
- **Passkeys.** Available as a Better Auth plugin. Support in Supabase Auth and Firebase Auth was **not verified**.
- **Magic links** depend on the email quota in section 2. At 500 players with sign-in links sent on deadline day, Resend Free's 100/day is the limit (inference).

## 7. Never free

- **Apple Developer Program:** [99 USD per membership year](https://developer.apple.com/programs/whats-included/).
- **Google Play:** [US$25 one time](https://support.google.com/googleplay/android-developer/answer/6112435).
- **Domain:** `.com` ["from $11.81"](https://porkbun.com/products/domains) per Porkbun (price list, no date shown, first-year vs renewal not distinguished). [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/) sells "at cost" with prices "at or below what registries and ICANN charge us".
- **SMS:** not free anywhere checked: Firebase phone auth is not on Spark; Supabase's default is 30 SMS per hour but needs an SMS provider ([rate limits](https://supabase.com/docs/guides/auth/rate-limits)). Provider prices not checked.
- **Email beyond about 100-300/day** and any dedicated sending from Cloudflare (Workers Paid $5/month).
- **Anything that needs a card.** Fly.io, Oracle, Render (for overage protection), Firebase Blaze and AWS require a card. The owner "does not pay for services", so card-on-file stacks carry risk of a surprise bill (inference).

## 8. Reference stacks for 50 leagues x 10 players

### Stack A: Cloudflare-only

- **Parts:** one Worker serving static assets (free, unlimited) and an API; D1 (SQLite) for data; one Cron Trigger every 5 minutes; Web Push sent from the Worker; email via Resend Free; auth with Better Auth on D1 (email magic link plus Google).
- **Free:** everything above. Durable Objects (SQLite-backed) are available if a live mode is added.
- **First limit to bite:** Resend's 100 emails/day on a deadline-heavy day, then the 100,000 Worker requests/day if the client polls (inference: 500 players x 20 visits x 10 calls already hits 100,000). The 10 ms CPU cap per request is a risk for crypto-heavy work such as Web Push encryption or password hashing (inference, not tested). Rows written (100,000/day) and D1 size (5 GB) are not close.
- **Lock-in:** medium. D1 is SQLite and data exports; Worker bindings and Durable Objects are Cloudflare-specific.
- **Commercial use:** no ban found in the Self-Serve Subscription Agreement (2025-09-12). Service-specific terms not read.
- **Cost surprises:** limits stop operations (errors) instead of billing. No card needed for Free.

### Stack B: Supabase + static hosting

- **Parts:** Supabase Postgres, Auth, Realtime, Edge Functions and pg_cron; static PWA on Cloudflare Workers/Pages Free; email through Resend or Brevo via custom SMTP; Web Push sent from an Edge Function.
- **Free:** 50,000 MAU, 500 MB, 5 GB egress, 500,000 Edge Function invocations, 200 realtime connections.
- **First limit to bite:** email (2 per hour built in; with Resend 100/day). Next, the project pause after 1 week of inactivity during off-season or a dormant beta (it stops cron too; recovery steps not checked), and the cap of 2 active free projects. The 500 MB database is ample for about 500 players (inference).
- **Lock-in:** low to medium. It is standard Postgres (the pricing page lists "Dedicated Postgres Database"); Auth, Edge Functions and Realtime APIs are Supabase-specific.
- **Commercial use:** no ban found in the terms.
- **Cost surprises:** none on Free; hitting limits stops service. Note the Turso acquisition adds some roadmap uncertainty only for Turso users.

### Stack C: Firebase (Spark)

- **Parts:** Firestore, Firebase Auth, Hosting, FCM for Web Push.
- **Free:** Firestore 1 GiB with daily quotas, Auth 50K MAU, Hosting, FCM.
- **First limit to bite:** no server code on Spark, so no scheduled phase changes or reminders. Workaround: an external clock (GitHub Actions every 5 minutes, or a Cloudflare Cron Worker) calling the Admin SDK, or Blaze with a card. Then Firestore's 50K reads/day (a results page that reads about 100 documents x 3 visits x 500 players is already 150,000; inference).
- **Lock-in:** high. Firestore's data model and security rules do not port easily (inference).
- **Commercial use:** not verified (terms not read).
- **Cost surprises:** moving to Blaze to get Functions needs a card and usage-based billing.

Verdict (inference): A or B. A gives the strongest "never pays, never pauses" profile; B gives relational data (Postgres), built-in auth and a built-in clock, at the cost of the one-week pause and the 2-project cap. C needs a second system just to tell time.

## Not verified and open questions

- Apple's own current statement on Home Screen web apps in the EU (the Apple EU page no longer mentions them; the 2024 reversal is only confirmed by [9to5Mac](https://9to5mac.com/2024/03/01/apple-home-screen-web-apps-ios-17-eu/)).
- Whether iOS 26 allows Web Push outside a Home Screen web app. No source found says it does.
- Android PWA install and push details beyond MDN/web.dev summaries.
- Mailjet free tier (page would not load). Vercel Hobby cron limits (page would not load). Netlify scheduled functions on Free. Firebase, Deno Deploy, Oracle and Turso commercial-use terms. Netlify's commercial status on a primary page. Appwrite Free numeric limits. OneSignal Free web push limits. Auth.js.
- Passkey support in Supabase Auth and Firebase Auth.
- Cloudflare service-specific terms (Workers, D1, Pages) were not read; only the Self-Serve Subscription Agreement.
- Whether Supabase paused-project data persists indefinitely and how restore works (billing FAQ says paused projects are not charged; retention not read).
- Expo/EAS, Capacitor and Flutter tooling costs were not researched.
- Web Push encryption CPU cost on Workers Free (10 ms) is a guess; test before committing.
- Ably's free tier: docs say 500 MAU, pricing page shows 1K.
- Traffic model: all "first limit" statements assume a rough pattern; a prototype should log real request and row counts.

## Sources

Apple, WebKit, Google, standards
- Apple Developer Program fee: https://developer.apple.com/programs/whats-included/
- Apple App Review Guidelines (4.2, 4.8): https://developer.apple.com/app-store/review/guidelines/
- Apple EU changes page: https://developer.apple.com/support/dma-and-apps-in-the-eu/
- WebKit, Web Push for Home Screen web apps (iOS 16.4): https://webkit.org/blog/13878/web-push-for-web-apps-on-ios-and-ipados/
- WebKit, Safari 26 beta (every site is a web app): https://webkit.org/blog/16993/news-from-wwdc25-web-technology-coming-in-safari-26-beta/
- WebKit, Declarative Web Push: https://webkit.org/blog/16535/meet-declarative-web-push/
- 9to5Mac (secondary), EU reversal: https://9to5mac.com/2024/03/01/apple-home-screen-web-apps-ios-17-eu/
- Google Play registration fee: https://support.google.com/googleplay/android-developer/answer/6112435
- Google Play testing requirement: https://support.google.com/googleplay/android-developer/answer/14151465
- MDN Push API: https://developer.mozilla.org/en-US/docs/Web/API/Push_API
- web.dev installation: https://web.dev/learn/pwa/installation

Backends
- Supabase pricing: https://supabase.com/pricing
- Supabase billing FAQ: https://supabase.com/docs/guides/platform/billing-faq
- Supabase terms: https://supabase.com/terms
- Supabase Cron: https://supabase.com/docs/guides/cron
- Supabase Edge Function limits: https://supabase.com/docs/guides/functions/limits
- Supabase Realtime limits: https://supabase.com/docs/guides/realtime/limits
- Supabase SMTP: https://supabase.com/docs/guides/auth/auth-smtp
- Supabase Auth rate limits: https://supabase.com/docs/guides/auth/rate-limits
- Supabase Sign in with Apple: https://supabase.com/docs/guides/auth/social-login/auth-apple
- Firebase pricing: https://firebase.google.com/pricing
- Firebase Functions get started: https://firebase.google.com/docs/functions/get-started
- Firebase scheduled functions: https://firebase.google.com/docs/functions/schedule-functions
- Firebase FCM web: https://firebase.google.com/docs/cloud-messaging/js/client
- Firebase email link auth: https://firebase.google.com/docs/auth/web/email-link-auth
- Cloudflare Workers limits: https://developers.cloudflare.com/workers/platform/limits/
- Cloudflare Workers pricing: https://developers.cloudflare.com/workers/platform/pricing/
- Cloudflare Cron Triggers: https://developers.cloudflare.com/workers/configuration/cron-triggers/
- Cloudflare D1 pricing: https://developers.cloudflare.com/d1/platform/pricing/
- Cloudflare KV pricing: https://developers.cloudflare.com/kv/platform/pricing/
- Cloudflare Durable Objects pricing: https://developers.cloudflare.com/durable-objects/platform/pricing/
- Cloudflare Queues pricing: https://developers.cloudflare.com/queues/platform/pricing/
- Cloudflare Pages limits: https://developers.cloudflare.com/pages/platform/limits/
- Cloudflare Email Service pricing: https://developers.cloudflare.com/email-service/platform/pricing/
- Cloudflare Self-Serve Subscription Agreement: https://www.cloudflare.com/terms/
- Cloudflare Registrar: https://www.cloudflare.com/products/registrar/
- Vercel Hobby plan: https://vercel.com/docs/plans/hobby
- Vercel terms of service: https://vercel.com/legal/terms
- Vercel fair use: https://vercel.com/docs/limits/fair-use-guidelines
- Netlify pricing: https://www.netlify.com/pricing/
- Netlify credit-based plans: https://docs.netlify.com/manage/accounts-and-billing/billing/billing-for-credit-based-plans/credit-based-pricing-plans/
- Netlify forum (secondary, via search summary): https://answers.netlify.com/t/can-we-use-netlify-free-plan-for-commercial-purposes/41545
- Neon pricing: https://neon.com/pricing
- Neon terms: https://neon.com/terms-of-service
- Turso pricing: https://turso.tech/pricing
- Turso joins Supabase: https://turso.tech/blog/turso-is-joining-supabase
- Render free: https://render.com/docs/free
- Fly.io pricing: https://fly.io/docs/about/pricing/
- Deno Deploy pricing: https://deno.com/deploy/pricing
- Deno cron: https://docs.deno.com/deploy/reference/cron/
- Appwrite pricing: https://appwrite.io/pricing
- Appwrite free plan docs: https://appwrite.io/docs/advanced/platform/free
- Oracle Always Free resources: https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm
- Oracle Cloud Free Tier: https://www.oracle.com/cloud/free/
- PocketBase docs: https://pocketbase.io/docs/
- GitHub Actions events (schedule): https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Email, push, realtime, auth, chat
- Resend pricing: https://resend.com/pricing
- Resend quotas: https://resend.com/docs/knowledge-base/account-quotas-and-limits
- Brevo pricing: https://www.brevo.com/pricing/
- Postmark pricing: https://postmarkapp.com/pricing
- Amazon SES pricing: https://aws.amazon.com/ses/pricing/
- OneSignal pricing: https://onesignal.com/pricing
- Ably pricing: https://ably.com/pricing
- Ably packages docs: https://ably.com/docs/platform/pricing
- Pusher Channels pricing: https://pusher.com/channels/pricing/
- Clerk pricing: https://clerk.com/pricing
- Better Auth: https://www.better-auth.com/docs/introduction
- Better Auth passkey plugin: https://www.better-auth.com/docs/plugins/passkey
- Telegram Bot FAQ: https://core.telegram.org/bots/faq
- Telegram bot features: https://core.telegram.org/bots/features
- Discord rate limits: https://discord.com/developers/docs/topics/rate-limits
- Porkbun domain prices: https://porkbun.com/products/domains
