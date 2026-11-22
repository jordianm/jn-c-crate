# Can the game live inside group chats?

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [Whether the game can live inside group chats](../11-group-channels.md)

## Answer

- **Discord is the only channel where the whole game can run inside the chat, with no fees to start.** Activities (web apps in an iframe) were opened to all developers on 2024-09-26 and run on desktop, mobile and web ([Discord blog](https://discord.com/blog/build-where-the-world-plays), [mobile guide](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/mobile.mdx)). A plain bot with slash commands is the cheaper route; two open-source bots already play Music League that way ([music-leek](https://github.com/snsutton/music-leek), [musicleague-bot](https://github.com/eeSquared/musicleague-bot)).
- **Telegram is the best free fit after Discord.** The Bot API is free. Mini Apps open from a link in any chat and know which chat they were opened from, so a group can share one game instance ([Mini Apps](https://core.telegram.org/bots/webapps)). A bot can post in the group, but can only DM users who allowed it ([Bot Developer Terms](https://telegram.org/tos/bot-developers)). Digital goods must be sold in Telegram Stars ([Stars](https://core.telegram.org/bots/payments-stars)).
- **WhatsApp cannot host the game, and reminders there cost money.** The Cloud API charges per delivered message since 2025-07-01. The Spain rate card (effective 2026-10-01) lists marketing 0.0585 EUR, utility 0.0166 EUR per message ([pricing](https://developers.facebook.com/docs/whatsapp/pricing)). The Groups API needs an Official Business Account and allows at most 8 participants ([Groups API](https://developers.facebook.com/docs/whatsapp/cloud-api/groups)). That rules it out for most leagues.
- **The free WhatsApp path is the share link.** `https://wa.me/?text=<encoded text>` opens a contact picker with the text pre-filled; the user still taps send ([click to chat](https://faq.whatsapp.com/5913398998672934), content via search summary, not verified directly). The preview card comes from Open Graph tags on your own page.
- **Slack is a notification channel, not a game surface, for small groups.** Free workspaces are limited to 10 apps ([Slack pricing](https://slack.com/pricing)). Cut Club's Slack integration only posts reminders and results; submitting and voting stay in Cut Club ([Cut Club help](https://www.playcutclub.com/help/slack-integration)).
- **iMessage has no group-friendly option.** iMessage apps and App Clips require an iOS app and Apple's developer program ([Messages](https://developer.apple.com/documentation/messages), [App Clips](https://developer.apple.com/documentation/appclip)). They do not reach Android members. A web link with good preview tags works everywhere.
- **Monetisation inside Discord is open to a Spain-based developer, with limits.** Premium Apps pays out through Stripe to developers in the US, EU and UK only, after the first $100 ([Enabling Monetization](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/monetization/enabling-monetization.mdx)). The owner does not pay for services, so this is a cost-free option to keep open, not a plan.
- **Playing music inside these chats is the unresolved piece.** Discord Activities load external content only through URL mappings ([networking](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/networking.mdx)). Whether YouTube or Spotify players work inside an Activity is **not verified**. Spotify and YouTube API rules are already in [01-market-music-league.md](../../../../research/01-market-music-league.md), section 5.
- **Inference:** for a Spain-based group the realistic combination is a web app with a strong share link (WhatsApp, iMessage, Telegram, Discord all preview it), plus an optional Discord or Telegram bot for groups that live there. Reminders should come from the app itself (push, email), with a "nudge on WhatsApp" button that the human taps.

## Discord

### Activities (Embedded App SDK)

- **What they are:** "Activities are web apps hosted in an iframe that use the Embedded App SDK to communicate with Discord clients" ([overview](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/overview.mdx)). They run on "desktop, mobile and web" ([how they work](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/how-activities-work.mdx)).
- **Launching:** from the App Launcher through an Entry Point command ("Launch" is created by default), or by answering an interaction with callback type `LAUNCH_ACTIVITY` (type 12). They can start in channels or DMs ([platform page](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/platform/activities.mdx), [how they work](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/how-activities-work.mdx)).
- **Availability:** "we are officially opening Discord Activities to all developers" (2024-09-26). Discovery needs verification "directly within our Developer Portal" and an opt-in ([Discord blog](https://discord.com/blog/build-where-the-world-plays)). Enabling Activities is one checkbox in the developer portal ([building guide](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/building-an-activity.mdx)).
- **Platforms:** web/desktop by default; iOS and Android are switched on in the portal ([mobile guide](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/mobile.mdx)).
- **Sandbox:** all traffic goes through the Discord proxy on `discordsays.com`. External URLs must be mapped in the portal, or the request fails with `blocked:csp` ([networking](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/networking.mdx)).
- **Invites and growth:** the SDK has `openInviteDialog` and `shareLink`. Links look like `https://discord.com/activities/<ID>?referrer_id=...&custom_id=...`, and the docs mention "turn-based deep-links" in "it's your turn" DMs ([SDK](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/developer-tools/embedded-app-sdk.mdx), [growth guide](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/growth-and-referrals.mdx)).
- **Fit (inference):** an Activity is a live session. A week-long league with a private vote still needs a backend and a bot for reminders. The Activity would be the "voting screen", not the whole game.

### Bots

- **Slash commands and components:** the two open-source bots use `/submit-song` and `/vote` (Music Leek) or `/submit` and emoji reactions (musicleague-bot) ([music-leek README](https://raw.githubusercontent.com/snsutton/music-leek/main/README.md), [musicleague-bot README](https://raw.githubusercontent.com/eeSquared/musicleague-bot/main/README.md)).
- **DMs for reminders:** bots can open a DM with `POST /users/@me/channels`. The docs warn: "You should not use this endpoint to DM everyone in a server about something. DMs should generally be initiated by a user action. If you open a significant amount of DMs too quickly, your bot may be rate limited or blocked" ([User resource](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/resources/user.mdx)). The Developer Policy forbids contacting users without explicit permission, per a search summary of the policy (the page itself returned HTTP 403, so this is **not verified** against the primary text) ([policy](https://support-dev.discord.com/hc/en-us/articles/8563934450327-Discord-Developer-Policy)). Practical design: remind in the league channel, and DM only players who opted in.
- **Scheduled events:** a guild can have at most 100 events in `SCHEDULED` or `ACTIVE` status. Name 1-100 characters, description 1-1000 ([Guild Scheduled Event](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/resources/guild-scheduled-event.mdx)). They suit a "voting closes" marker.
- **Rate limits:** "All bots can make up to 50 requests per second" globally, plus per-route limits. Interaction endpoints are not bound by the global limit. More than 10,000 invalid requests (401/403/429) in 10 minutes gets an IP temporarily banned ([rate limits](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/topics/rate-limits.mdx)). Normal league traffic is far below this.
- **Verification:** the application docs show separate intents for bots "in 100 or more servers" ([Application](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/resources/application.mdx)). A search summary says verification is required to grow past 100 servers and needs Stripe identity checks. The support article returned HTTP 403, so this is **not verified** at primary level ([support article](https://support-dev.discord.com/hc/en-us/articles/23926564536471-How-Do-I-Get-My-App-Verified)).
- **Threads:** not checked (see open questions).

### Monetisation (Premium Apps)

- Applies to bots and Activities. Subscriptions (user or guild) and one-time purchases (durable or consumable) ([overview](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/monetization/overview.mdx)).
- Eligibility: verified app, team owner at least 18, 2FA, Terms and Privacy links, payouts set up. "Once your app has made its first $100 it will become eligible for payout." Payouts run through Stripe. "Premium Apps is not currently available outside of these regions" (US, EU, UK) ([Enabling Monetization](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/monetization/enabling-monetization.mdx)).
- Revenue share: a search summary gives 85% to the developer on the first $1M, after processing fees. **Not verified**: the support pages that state it were blocked (HTTP 403) ([payouts](https://support-dev.discord.com/hc/en-us/articles/17299902720919-Premium-Apps-Payout)).

### Music inside Discord

- No primary text found that forbids or allows audio inside an Activity. **Not verified:** whether a YouTube iframe, Spotify embed or `<audio>` element plays inside the sandbox. Test with a throwaway Activity in a later prototype ticket.
- Link-based play is the safe route: submissions are links, and people open them in their own player. Music Leek takes Spotify links and can build a Spotify playlist ([README](https://raw.githubusercontent.com/snsutton/music-leek/main/README.md)). Spotify's Development Mode limits (5 users) would hit a hosted bot ([01-market](../../../../research/01-market-music-league.md), section 5).

### Existing music-league bots

| Bot | What it does | State (GitHub API, 2026-11-22) |
|---|---|---|
| [Music Leek](https://github.com/snsutton/music-leek) | Leagues, themed rounds, theme suggestions, `/submit-song` modal, 10-point vote budget over up to 5 songs, DM deadline reminders, automatic tallies, season leaderboard, Spotify playlist export. Self-hosted: you create your own bot token and run it (README suggests Railway). | Last push 2026-11-18, MIT, 1 star |
| [musicleague-bot](https://github.com/eeSquared/musicleague-bot) | Rounds with timed submit and vote phases, emoji-reaction voting (up to 3 votes), leaderboard. Self-hosted, Python. | Last push 2025-10-15, MIT, 0 stars |

Both are self-hosted, so no group can add them with one click. A hosted, invite-by-link bot is the gap (inference). A search of top.gg tags found no hosted Music League-style bot ([top.gg](https://top.gg/tag/songs), search summary).

## Telegram

- **Bot API:** free. "By default, bots are able to message their users at no cost" ([FAQ](https://core.telegram.org/bots/faq)). Current version at access date: Bot API 10.4, 2026-11-09 ([changelog](https://core.telegram.org/bots/api-changelog)).
- **Limits:** one message per second per chat; "In a group, bots are not be able to send more than 20 messages per minute"; about 30 messages per second for bulk. Paid broadcasts (0.1 Stars per message over the free rate) need 100,000 Stars and 100,000 monthly users, so they are irrelevant here ([FAQ](https://core.telegram.org/bots/faq)).
- **DMs:** the Terms refer to broadcasting "to users who have granted permission to contact them" and forbid spamming "with unsolicited messages" ([Bot Developer Terms](https://telegram.org/tos/bot-developers)). A Mini App can ask the user for permission to send messages with `requestWriteAccess` ([Mini Apps](https://core.telegram.org/bots/webapps)). A group reminder (post in the group, mention the late player) needs no permission.
- **Group privacy mode:** bots in groups run in privacy mode by default and see only commands and replies relevant to them ([features](https://core.telegram.org/bots/features)). Slash commands and buttons are enough for this game.
- **Mini Apps:** JavaScript web apps inside Telegram. A direct link `https://t.me/<bot>?startapp=<param>` opens the app in the current chat, with `chat_type` and `chat_instance` so it can "keep track of the current chat context... multiplayer games and similar apps". A Mini App opened this way "can't read messages or send new ones on behalf of the user" ([Mini Apps](https://core.telegram.org/bots/webapps)). Sharing out of a Mini App uses `shareMessage` or `switchInlineQuery` (same page).
- **Older games platform:** HTML5 games sent as bot messages, with per-chat high-score tables; examples are @gamebot and @gamee ([Gaming Platform](https://core.telegram.org/bots/games)).
- **Payments:** "all transactions must be carried out in Telegram Stars, with currency tag XTR"; otherwise Telegram "cannot display your bot or mini-app to mobile users". Bots must answer `/terms` and `/support` ([Stars](https://core.telegram.org/bots/payments-stars)). Stars can be redeemed through Fragment, may be unavailable in some countries, and credit after up to 21 days ([Bot Developer Terms](https://telegram.org/tos/bot-developers), sections 6.2.4-6.2.5). Stars earned expire after 3 years (same page). Whether Spain is covered for rewards is **not verified**.
- **Hosting:** you host the Mini App yourself over HTTPS. No Telegram review was found for a bot or Mini App to go live (**not verified** as a negative).

## WhatsApp

### Business Platform (Cloud API)

- **Pricing model:** "Effective July 1, 2025 – Meta charges on a per-message basis" for delivered messages. Categories: marketing, utility, authentication, service, Meta Business Agent. The pricing page shows no last-updated date; the latest effective date on it is 2026-10-01 ([pricing](https://developers.facebook.com/docs/whatsapp/pricing), read through a page-summary tool because the page renders client-side).
- **Service window:** a 24-hour window opens when the user messages the business. The page says the first 1,000 service messages per number per month are free and charged from the 1,001st starting 2026-10-01. Utility replies inside the window changed from free to `regular` pricing on 2026-10-01 (same page; summary-tool reading, treat as **not verified** until checked on the live page).
- **Click-to-WhatsApp ad window:** up to 7 days free ("The FEP window may remain open for up to 7 days"), but this requires paying for ads ([pricing](https://developers.facebook.com/docs/whatsapp/pricing)).
- **Spain rate card, EUR, effective 2026-10-01** (read directly from the "EUR list rates" file linked on the pricing page):

| Market | Marketing | Utility | Authentication | Service |
|---|---|---|---|---|
| Spain | 0.0585 | 0.0166 | 0.0166 | 0.0166 |
| Italy | 0.0658 | 0.0248 | 0.0248 | 0.0248 |
| Rest of Western Europe | 0.0490 | 0.0142 | 0.0142 | 0.0142 |

- **Worked example (inference):** a league of 10 players with 2 deadline reminders per week is 20 template messages a week. At the utility rate that is about 0.33 EUR a week; at the marketing rate about 1.17 EUR a week. Meta decides the category, and a reminder that nudges people to play could be classed as marketing. Business verification, a dedicated phone number and a Meta billing account are also needed (not detailed in the sources read).
- **Opt-in and policy:** "You may only contact people on WhatsApp if... you have received opt-in permission from the recipient". Real-money gambling and "games of chance/skill" promotions have extra rules; a free music game with no prize in money is outside them ([Business Messaging Policy](https://whatsappbusiness.com/policy), last updated 2026-09-23).
- **Messaging limits (tiers of 250 / 2,000 / 10,000 unique users per 24 h):** only third-party summaries found. **Not verified** ([search results](https://chatarmin.com/en/blog/whats-app-messaging-limits)). Small leagues are well below any tier.
- **Groups API:** "now open to all businesses with an Official Business Account (OBA)". "Max group participants: 8", up to 10,000 groups per business number, one Cloud API business per group. Join is by invite link only. Text, media and templates work; interactive messages (buttons) and calling do not. Pricing is per message, with no group-specific rate listed ([Groups API](https://developers.facebook.com/docs/whatsapp/cloud-api/groups), summary-tool reading). Conclusion: a business number cannot sit in an existing 30-person group, and OBA status is not available to a hobby project (OBA requirements not retrieved, **not verified**).
- **Unofficial bots:** WhatsApp's Terms prohibit "bulk messaging, auto-messaging, auto-dialing" and unauthorized or automated access ([Terms](https://www.whatsapp.com/legal/terms-of-service), effective 2021-01-04). Libraries that automate a personal account break these terms (inference), and I do not recommend them.

### Free path: share links

- `https://wa.me/<number>?text=<urlencoded>` opens a chat with pre-filled text. `https://wa.me/?text=<urlencoded>` opens a contact picker. The user must tap send ([click to chat](https://faq.whatsapp.com/5913398998672934); the FAQ page is client-rendered, so the details come from search summaries and are **not verified** against the page text). `whatsapp://send?text=` is the app-scheme equivalent (same caveat).
- A group invite link (`chat.whatsapp.com/...`) can be shared by the app so players can join a league group. The game would not run in it.

### Channels and Communities

- Third-party summaries: Channels are one-way (followers react and vote in polls); Communities group several groups under an announcement group. Limits vary by source. **Not verified** against WhatsApp's own pages ([comparison](https://www.guidingtech.com/whatsapp-channel-vs-community-vs-groups/)). Neither gives a bot a way to post or collect votes without the Business Platform.

## Slack

- **Free workspaces:** "Up to 10 apps", 90 days of searchable message history ([Slack pricing](https://slack.com/pricing)).
- **Distribution:** an app lives in one workspace by default. "Activate Public Distribution" gives an Add to Slack button and URL (unlisted). Apps "intended for commercial distribution should be submitted and approved for listing in the Slack Marketplace" ([distribution](https://docs.slack.dev/distribution)). Marketplace review checks guidelines and security ([guidelines](https://docs.slack.dev/slack-marketplace/slack-marketplace-app-guidelines-and-requirements)).
- **Limits:** "apps may post no more than one message per second per channel". Web API methods are limited per method, per workspace, per app, in four tiers ([rate limits](https://docs.slack.dev/apis/web-api/rate-limits)). Enough for league traffic.
- **Cut Club's integration:** "notifications only". It posts theme drops, submission reminders, voting reminders and results to a channel. "Players can't submit or vote from Slack." Connecting needs a workspace admin or app-install permission. Players not in Slack get email. Help page updated 2026-04-09 ([Cut Club help](https://www.playcutclub.com/help/slack-integration)). It belongs to the paid Season Pass ($9.99 per season) per the pricing page ([Cut Club pricing](https://www.playcutclub.com/help/understanding-pricing), search summary).
- **Fit (inference):** Slack suits work teams. Friend groups in Spain rarely use it, so it is a low priority.

## iMessage, Apple and Android

- **iMessage apps:** built with the Messages framework, as standalone apps or extensions. They can present "a custom user interface inside the Messages app" and "update interactive messages (for example, to create games or collaborative apps)" ([Messages](https://developer.apple.com/documentation/messages)). They ship through the App Store. They exist only on Apple devices (inference from the framework being iOS/macOS; the page does not discuss Android).
- **App Clips:** "a lightweight version of your app". They need a full app. Binary size limits are 10-25 MB depending on iOS version, or up to 100 MB from iOS 17 if only digital invocations are supported ([App Clips](https://developer.apple.com/documentation/appclip), [size rules](https://developer.apple.com/documentation/appclip/choosing-the-right-functionality-for-your-app-clip)). A link in a message can launch one (inference from "invocations").
- **Cost:** the Apple Developer Program fee was not retrieved (**not verified**).
- **Android:** apps hand content to other apps through the Android Sharesheet and `ACTION_SEND` intents ([Android docs](https://developer.android.com/training/sharing/send)). A web page can only start that sheet through the browser's own share function (not checked).
- **Fit (inference):** the rich preview of a plain link in Messages is the only low-effort iMessage touchpoint (next section).

## Invite links that look good when shared

All channels fetch your page and read meta tags from the HTML your server sends. None runs JavaScript, so a single-page app must render the tags on the server.

| Channel | Reads | Image | Source |
|---|---|---|---|
| Open Graph base | `og:title`, `og:type`, `og:image`, `og:url` required; `og:description` optional | n/a | [ogp.me](https://ogp.me) |
| Discord | `og:title`, `og:description`, `og:site_name`, `og:image` (+ `:width`/`:height`), `theme-color`, `twitter:card` for layout; oEmbed (JSON) as fallback | PNG, GIF, JPG, WebP, AVIF; declare width and height; example 1200x630; `twitter:card=summary_large_image` gives large image; fetch must finish in 10 s, max 5 redirects; "Link previews are subject to change" | [Link Previews](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/link-previews/overview.mdx) |
| iMessage | `og:image`, `og:title` (no site name in it), `og:site_name`, `apple-touch-icon` fallback | at least 900 px wide; under 150 px may be ignored or shown as an icon; avoid text in the image; no meta redirects, no JavaScript | [TN3156](https://developer.apple.com/documentation/technotes/tn3156-create-rich-previews-for-messages) |
| WhatsApp | `og:title`, `og:description`, `og:image` (third-party sources) | no official doc found; guides say 1200x630 JPG under about 300 KB; HTTPS absolute URL; cache per URL (**not verified**) | [OpenGraph+ guide](https://opengraphplus.com/consumers/whatsapp/images), secondary |
| Telegram | `og:title`, `og:description`, `og:image`, falling back to twitter tags (third-party); Instant View is a separate template system | at least 200x200, ideal 1.91:1; refresh with @webpagebot (**not verified**) | [OpenGraph+ guide](https://opengraphplus.com/consumers/telegram/tags), secondary |
| Meta (Facebook, shared crawler family) | `og:image` | minimum 200x200; 1200x630 recommended; 600x315 floor for a large card; 1.91:1; max 8 MB | [Meta sharing docs](https://developers.facebook.com/docs/sharing/webmasters/images) |

**Practical recipe (inference):** one 1200x630 JPG under 300 KB, absolute HTTPS URL, with `og:title`, `og:description`, `og:image`, `og:image:width`, `og:image:height`, `og:site_name`, `twitter:card=summary_large_image` and `theme-color`, rendered server-side. Changing the image later needs a new URL (add `?v=2`) because previews are cached.

## Bottom line

Effort is an inference on a scale S (days), M (weeks), L (months) for one developer, assuming a web backend already exists.

| Channel | Can the game run inside it? | Can it send reminders there? | Cost | Main restriction | Effort (inference) |
|---|---|---|---|---|---|
| Discord Activity | Yes, as a web app in an iframe (desktop, mobile, web) | Via a bot in the channel; DMs only for opted-in users | Free to build; Premium Apps payouts only for US/EU/UK developers | Sandbox URL mappings; music playback inside it unverified; verification past 100 servers (secondary) | M |
| Discord bot only | Partly: commands, buttons, embeds; voting by modal or reactions | Yes: channel posts, DMs with care, scheduled events | Free; hosting is yours | Developer Policy on DMs; self-hosted precedent only | S to M |
| Telegram bot + Mini App | Yes: Mini App from a group link, shared by `chat_instance` | Yes: group posts (20 per minute) and DMs after permission | Free; digital goods in Stars only | Mini App cannot read or post chat messages; user must allow DMs | M |
| WhatsApp Cloud API | No; groups capped at 8 and OBA only | Yes, 1:1 templates with opt-in | Per message: Spain utility 0.0166 EUR, marketing 0.0585 EUR | Paid, business verification, opt-in, no group posting for ordinary groups | L |
| WhatsApp free links | No | No; the user taps a pre-filled share or nudge link | Free | Human must press send; preview depends on your tags | S |
| Slack app | Partly (modals, buttons) | Yes, channel posts at 1 message per second | Free; 10-app cap on free workspaces | Workspace admin must install; Marketplace review for commercial listing | M |
| iMessage app / App Clip | iMessage app yes (Apple only); App Clip as an entry point | No | Apple developer fee (not verified) | iOS only, needs a native app | L |
| Plain web link (all chats) | Yes, in the browser | Only through the app's own push or email | Free | Needs a good preview image and server-side tags | S |

**Most promising combination for a Spain-based group (inference).** The group chat is most likely WhatsApp, where the game cannot live and a free bot cannot post. So the base is a web app (or PWA) whose invite link previews well in WhatsApp, iMessage, Telegram and Discord, plus reminders sent by the app itself (web push, email) and a "nudge on WhatsApp" button that opens a pre-filled `wa.me` message for a human to send. Add a Discord bot or Telegram bot as an optional integration for groups that already live there. Of the two, Telegram offers the more complete free route (Mini App plus group posts), and Discord has the proven precedent (Music Leek). Neither should be the only form, because it would exclude WhatsApp-only groups.

## Not verified and open questions

1. **Discord support-center pages** (`support-dev.discord.com`, `support.discord.com`) and the Developer Policy returned HTTP 403 or a bot check. The 85/15 revenue share, the 100-server verification threshold and the DM rules come from search summaries (secondary).
2. **Audio and embeds inside a Discord Activity** (YouTube iframe, Spotify embed, `<audio>`): no primary source found. Needs a small test.
3. **Discord threads** for league discussion: not researched.
4. **Discord Premium Apps rate above $1M** and payout schedule: only in blocked pages.
5. **WhatsApp pricing page** renders client-side; the model description (service window, FEP, 2026-10-01 changes) was read through a summary tool. Only the EUR rate card file was read directly.
6. **WhatsApp OBA requirements** (who can get Official Business Account status), template category decisions for reminders, and messaging-tier limits: not retrieved from Meta.
7. **WhatsApp `wa.me` formats, Channels and Communities limits, and link-preview rules** rely on search summaries and third-party guides.
8. **Telegram link-preview rules and `@webpagebot`** rely on third-party guides. Whether Telegram reviews bots or Mini Apps before launch: no source found.
9. **Telegram Stars rewards availability in Spain** and the conversion rate: not checked.
10. **Apple Developer Program fee** and whether iMessage apps are limited to Apple devices in any way beyond the framework: not retrieved.
11. **Android:** no first-party way to post to an arbitrary chat besides the Sharesheet; web share from the browser not checked.
12. **Real usage:** the share of Spanish friend groups on WhatsApp, Telegram or Discord was not sourced. The WhatsApp-default assumption comes from the brief.
13. Whether a hosted Music League-style Discord bot exists beyond the two GitHub projects: top.gg tags showed none; an exact "Music League" search there was not possible.

## Sources

Discord
- [Come Build Where the World Plays](https://discord.com/blog/build-where-the-world-plays), 2024-09-26
- [Activities overview](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/overview.mdx) · [How Activities work](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/how-activities-work.mdx) · [Mobile](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/mobile.mdx) · [Networking](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/networking.mdx) · [Growth and referrals](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/development-guides/growth-and-referrals.mdx) · [Building an Activity](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/activities/building-an-activity.mdx) · [Platform: Activities](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/platform/activities.mdx)
- [Embedded App SDK reference](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/developer-tools/embedded-app-sdk.mdx)
- [Monetization overview](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/monetization/overview.mdx) · [Enabling Monetization](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/monetization/enabling-monetization.mdx)
- [Rate limits](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/topics/rate-limits.mdx) · [User resource (Create DM)](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/resources/user.mdx) · [Guild Scheduled Event](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/resources/guild-scheduled-event.mdx) · [Application resource](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/resources/application.mdx) · [Link Previews](https://raw.githubusercontent.com/discord/discord-api-docs/main/developers/link-previews/overview.mdx)
- Blocked (HTTP 403), cited from search summaries only: [Developer Policy](https://support-dev.discord.com/hc/en-us/articles/8563934450327-Discord-Developer-Policy), [Premium Apps Payout](https://support-dev.discord.com/hc/en-us/articles/17299902720919-Premium-Apps-Payout), [App verification](https://support-dev.discord.com/hc/en-us/articles/23926564536471-How-Do-I-Get-My-App-Verified)
- [Music Leek (repo)](https://github.com/snsutton/music-leek), [README](https://raw.githubusercontent.com/snsutton/music-leek/main/README.md) · [musicleague-bot (repo)](https://github.com/eeSquared/musicleague-bot), [README](https://raw.githubusercontent.com/eeSquared/musicleague-bot/main/README.md) · [top.gg tags](https://top.gg/tag/songs) (secondary)

Telegram
- [Mini Apps](https://core.telegram.org/bots/webapps) · [Bots FAQ](https://core.telegram.org/bots/faq) · [Bot features](https://core.telegram.org/bots/features) · [Stars payments](https://core.telegram.org/bots/payments-stars) · [Gaming Platform](https://core.telegram.org/bots/games) · [Bot API changelog](https://core.telegram.org/bots/api-changelog) · [Bot Developer Terms](https://telegram.org/tos/bot-developers)

WhatsApp
- [Pricing](https://developers.facebook.com/docs/whatsapp/pricing) (EUR rate card file linked from it) · [Groups API](https://developers.facebook.com/docs/whatsapp/cloud-api/groups) · [Business Messaging Policy](https://whatsappbusiness.com/policy) · [Terms of Service](https://www.whatsapp.com/legal/terms-of-service) · [Click to chat](https://faq.whatsapp.com/5913398998672934)
- Secondary: [messaging limits](https://chatarmin.com/en/blog/whats-app-messaging-limits) · [Channels vs Communities](https://www.guidingtech.com/whatsapp-channel-vs-community-vs-groups/) · [WhatsApp preview guide](https://opengraphplus.com/consumers/whatsapp/images) · [Telegram preview guide](https://opengraphplus.com/consumers/telegram/tags)

Slack and Cut Club
- [Slack pricing](https://slack.com/pricing) · [Distribution](https://docs.slack.dev/distribution) · [Marketplace guidelines](https://docs.slack.dev/slack-marketplace/slack-marketplace-app-guidelines-and-requirements) · [Rate limits](https://docs.slack.dev/apis/web-api/rate-limits)
- [Cut Club Slack integration](https://www.playcutclub.com/help/slack-integration) · [Cut Club pricing help](https://www.playcutclub.com/help/understanding-pricing) (search summary)

Apple, Android, Meta, Open Graph
- [Messages framework](https://developer.apple.com/documentation/messages) · [App Clips](https://developer.apple.com/documentation/appclip) · [App Clip size](https://developer.apple.com/documentation/appclip/choosing-the-right-functionality-for-your-app-clip) · [TN3156](https://developer.apple.com/documentation/technotes/tn3156-create-rich-previews-for-messages)
- [Android Sharesheet](https://developer.android.com/training/sharing/send)
- [Meta sharing images](https://developers.facebook.com/docs/sharing/webmasters/images) · [Open Graph protocol](https://ogp.me)
