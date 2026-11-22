# Opportunity brief: where a Music League alternative can stand

Status: as-is snapshot, 2026-11-22. Synthesis of study 01 and the 12 closed research tickets of the wayfinder map `crate`. No product decision is taken here; the decisions are listed at the end, each with its ticket.

## Headline

1. **The market is one big incumbent and a crowd of small clones.** Music League claims 1.1 million registered users and has 6,586 iOS ratings; no clone passes about 1,000 to 5,000 Play downloads. The clones already ship most "obvious" differentiators (more services, guess-who, chat, reminders, stats). The unsolved problem is distribution, not features.
2. **The evidenced pain is the experience, not missing features.** In 458 App Store reviews, intrusive mobile ads lead by far (62%, 86% in 2026), then crashes and sign-in failures (about 95), then Spotify lock-in (about 30). What players love is the social side: friends first, discovery second, competition third.
3. **The platforms close every deep integration to a game.** Spotify bans games in its API and, without written approval, in its embeds; Apple charges 99 USD a year and bans monetising Apple Music access; Deezer, TIDAL and SoundCloud bar games or commercial use. **Outbound links are the one route no developer agreement covers**, and EU case law treats links to official pages as lawful.
4. **Audio is the hard limit.** There is no free, lawful way to play a blind clip. The platforms' own players (YouTube with start and end, the Apple embed) are free but show the title. Any other clip needs licences.
5. **A zero-cost base is technically possible.** A PWA on Supabase Free or Cloudflare Free, email magic links plus Google sign-in, Web Push and share links. Email volume is the first ceiling. Never free: a domain (about 12 USD a year) and anything Apple.

## Hard constraints

| Area | Constraint | Source |
|---|---|---|
| Spotify | API: "Do not create a game, including trivia quizzes"; Development Mode capped at 5 users, non-commercial. Embeds: no "game functionality" without written approval (Widget Terms IV.2.d). Links: no developer terms accepted (inference; a lawyer should confirm). | [spotify-access](../tasks/wayfinder/crate/research/spotify-access.md) |
| Apple Music | API and MusicKit need the 99 USD/year programme; DPLA 3.3.6(D) bans monetising access "in any way"; previews may not be a game's soundtrack (5.2.5). Free: iTunes Search (about 20 calls a minute) and the embed. | [apple-music-access](../tasks/wayfinder/crate/research/apple-music-access.md) |
| YouTube | Embedded player is free and keyless, with ad-hoc playlists; it must stay visible (200×200 px minimum), no audio-only, no overlays. Search: 100 calls a day for the whole product. | [youtube-access](../tasks/wayfinder/crate/research/youtube-access.md) |
| Other services | Deezer, TIDAL and SoundCloud bar games or commercial use; Amazon has no open API. | [other-services](../tasks/wayfinder/crate/research/other-services.md) |
| Matching | The free Odesli API is gone; ISRC identifies a recording, not a song; MusicBrainz is free for non-commercial use only. Matching has to be human-assisted. | [song-matching](../tasks/wayfinder/crate/research/song-matching.md) |
| Law (EU, Spain) | GDPR from the first user; consent valid from age 14; newsletters need prior consent (LSSI art. 21); non-essential cookies need consent, so embeds load on click; DSA hosting duties, with the micro/small exemption; no safe income threshold for registering as self-employed. | [business-and-legal](../tasks/wayfinder/crate/research/business-and-legal.md) |
| Group chats | Only Discord can host the whole game; Telegram is a free second; WhatsApp only through share links a person sends. | [group-channels](../tasks/wayfinder/crate/research/group-channels.md) |
| Hosting | Supabase Free or Cloudflare Free fit; Firebase Spark (no scheduled jobs) and Vercel Hobby (non-commercial) do not. | [tech-options](../tasks/wayfinder/crate/research/tech-options.md) |

## Gaps: evidenced, occupied, guessed

| Gap | Evidence from players | Who already covers it | Read |
|---|---|---|---|
| A game without intrusive ads | Strong: 62% of reviews, rising | BandJam, Aux Battles (free, no ads); Music League promises "leaning on ads less" | **Open as experience**, not as a feature |
| Reliability and simple sign-in | Strong: about 95 reviews | Unknown for clones (no data) | **Open**; hard to prove before launch |
| Any music service, YouTube included | Steady: about 30 reviews over 5 years | YapZap (7 services), BandJam, DJ League; Music League 2.0 adds Apple only | **Occupied by clones**, open against Music League |
| Guess who submitted it | Small but unprompted: 6 reviews | BandJam, DJ League | Occupied |
| Chat, reactions, social layer | About 15 reviews | Music League 2.0 (chat, follow, feed), BandJam | Occupied |
| Reminders and nudges | Founders' own story; few reviews | Music League 2.0 (3 channels), BandJam | Occupied |
| Stats and recaps | Third-party "Music League Wrapped" exists, so demand exists | Music League 2.0 Year-in-Review, BandJam 23 charts, Cut Club season recaps | Partly occupied; **an automated per-round story or newsletter was not found anywhere** |
| Accessibility (screen readers) | 3 reviews, severe effect | None found | Open, small |
| Daily or live play | **None** in 458 reviews | Cut Club Daily Cut, YapZap Daily rooms; songbattle.io and Aux Battles are live and have the biggest numbers | Guessed demand among league players; proven demand for live party games |
| Spanish-language product | None found either way | Nothing Spanish-first; several rivals translate their UI | Thin on its own |

## Jordi's raw ideas against the evidence

Recorded in [ticket 12](../tasks/wayfinder/crate/12-jordis-ideas.md). This section sets each idea next to what the research says; whether each one stays is for the grilling.

| Idea | What the research says |
|---|---|
| Links only, listening happens on the platforms | Fits the safest legal route and the zero-cost base. Cost: no in-app listening; the player leaves the app to listen, which is where engagement can break. |
| A short audio clip where possible | Only through the platform's own player (YouTube start/end, Apple embed): free, but it shows the title and loads third-party cookies. Raw preview files breach terms; self-hosted clips need three sets of rights. |
| Daily game, a "musical Wordle" | No daily music game documents a licence for its audio; Bandle recreates songs and calls licensing costly. Formats with no audio get traction (Spotle, Lyricle). Text and images with a link out at the end fit the constraints; lyrics licensing is not researched. No league player asked for it. |
| Compete with friends, gamification | Matches what players love (the social side). Mechanics already shipped by rivals give no edge on their own. |
| Better mobile and web experience | The strongest evidenced gap (ads, crashes, sign-in). Mostly about Music League's legacy 1.x app; 2.0 is in beta and may close part of it. |
| Newsletter and automated stories per league, "matchday status" | The only format found nowhere as an automated per-league product. Built on the game's own data, it needs no music API (inference). Newsletters need prior consent; email is the tightest free resource; free sharing from the web is Web Share, OG cards and images, not direct posting to Instagram or TikTok. |
| Cross-selling through links later | Affiliate is the safest paid route: Amazon.es pays 3 EUR per Music Unlimited trial; Apple's programme pays an unpublished amount and accepts few partners; no Spotify or YouTube programme exists. Small money. |
| Simple, strong base first, minimum cost | The research supports it: every deep integration is closed or paid, and the clones show that feature breadth does not win. |

## Candidate directions (for discussion, not chosen)

**A. Link-first league, done well.** Async themed rounds, any service by pasted link, matching assisted by the submitter, no ads, PWA. Edge: experience and reliability, plus the automated round story. Risk: little technical moat; Music League 2.0 may fix its own experience; distribution still unsolved.

**B. League plus a daily habit.** Direction A, plus a no-audio daily game (text and images, link out at the end) whose result feeds the league's story and standings. Edge: a reason to open the app every day, and a share mechanic that has driven growth in this niche (the Wordle grid). Risk: more to build; no league player asked for it; a daily game must stand on its own to get traction.

**C. Live mode first.** Short synchronous sessions (the format with the biggest numbers: songbattle.io, Aux Battles), with the async league as the second step. Edge: proven traction, quick to play on a call or a Discord server. Risk: different product from Music League; YouTube's visible-player rule shapes the experience; Discord-heavy audience.

Every direction shares the same base: link-out, no hosted audio, free tiers, consent-based email, share links that render well in WhatsApp.

## What only Jordi can decide

1. **Ambition and destination** ([ticket 13](../tasks/wayfinder/crate/13-ambition-and-destination.md)): hobby for his groups, side project to grow, or business; time per week; acceptable spend (a domain? the 99 USD Apple programme?); does the proposed destination (an MVP spec) stand.
2. **First audience** ([ticket 14](../tasks/wayfinder/crate/14-first-audience.md)): his own groups, Spanish-speaking friends, work teams, Discord communities, or Music League players; language.
3. **Music-platform strategy** ([ticket 15](../tasks/wayfinder/crate/15-music-platform-strategy.md)): links only, or links plus the platforms' own embeds (YouTube, Apple), and whether to ask Spotify for written approval.
4. **Business model** ([ticket 16](../tasks/wayfinder/crate/16-business-model.md)): free, donations, host-pays, affiliate, or none for now.
5. **Product form** ([ticket 17](../tasks/wayfinder/crate/17-product-form.md)): PWA, native, or inside Discord or Telegram.
6. **MVP scope** ([ticket 20](../tasks/wayfinder/crate/20-mvp-scope.md)): which of the ideas above go in the first version and which wait. Fed by the core-loop and submission-flow prototypes (tickets 18 and 19).

## Holes in the evidence

- **Reddit was not reached** (blocked to automated access). The largest source of long-form player opinion is missing; Jordi can export threads by hand into `inbox/`.
- **Music League 2.0 is in beta;** all reviews are about the 1.x app. Its experience may improve before Crate launches.
- **No clone publishes active users;** store counts are the only signal.
- **Legal points need a lawyer before any money:** whether a league with Spotify embeds is "game functionality"; cover art and metadata in generated stories; minors; paid-feature wording.
- **Not researched:** lyrics licensing, name and trademark availability, Spain and Latin America platform shares.

## Where the detail is

Study 01 ([01-market-music-league.md](01-market-music-league.md)) is the first, unverified pass; its correction note lists what the later research superseded. The verified findings, one per ticket, are in [`tasks/wayfinder/crate/research/`](../tasks/wayfinder/crate/research/); the map with one line per closed ticket is [`tasks/wayfinder/crate/_map.md`](../tasks/wayfinder/crate/_map.md).
