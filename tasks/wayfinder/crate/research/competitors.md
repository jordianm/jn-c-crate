# Competitors one by one: Music League and the products that copy or border it

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [Competitors one by one](../02-competitors.md)

Method: each product's own site, help pages, store listings, changelog or repo was opened. Apple figures come from Apple's lookup API (`https://itunes.apple.com/lookup?id=<id>&country=us`, US storefront). Google Play figures come from the public listing page. Marketing claims are marked as such. "Not verified" means the primary source was not reachable or does not state it. "(inference)" is my reading, not a source statement. Reddit and Product Hunt were not readable (Reddit blocked; Product Hunt returns a Cloudflare 403), so no data from either.

## Answer

- **Direct Music League clones exist, but none has real traction.** Store numbers of the four app-based clones: BandJam has 16 iOS ratings and "1K+" Google Play downloads ([Apple lookup](https://itunes.apple.com/lookup?id=6756460555&country=us), [Google Play](https://play.google.com/store/apps/details?id=app.bandjam)). YapZap has 7 ratings and "100+" downloads. Cut Club has 6 ratings and "50+". DJ League has 2 ratings and "10+". Music League has 6,586 iOS ratings and "100K+" on Play ([Apple](https://itunes.apple.com/lookup?id=1589815321&country=us), [Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US)). All four have App Store release dates between 2025-12 and 2026-03 (YapZap's listing reports 2025-12-22; its App Store ID suggests an earlier creation, not verified).
- **The only large numbers outside Music League are in live, short-session games, not leagues.** songbattle.io (Germany) shows 349,645 games created, 6,596,689 songs submitted and 28,774,086 votes ([songbattle.io](https://songbattle.io/)), and its Discord has 7,838 members ([Discord invite API](https://discord.com/api/v10/invites/p6bBfxY7bN?with_counts=true)). Aux Battles shows 14,360 players joined and 4,957 games played ([auxbattles.app](https://auxbattles.app/)). Both are free and web-only.
- **Music-service breadth is no longer a differentiator.** YapZap lists Spotify, Apple Music, YouTube Music, TIDAL, Amazon Music, Deezer and Qobuz ([App Store listing](https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650)). BandJam lists Spotify, Apple Music, YouTube Music and, since v1.29, TIDAL ([release notes](https://itunes.apple.com/lookup?id=6756460555&country=us)). DJ League lists Spotify, Apple Music and YouTube Music ([djleague.app](https://djleague.app/)). Music League itself now offers Spotify or Apple Music ([help](https://next.musicleague.com/support/how-to-play)). BandJam builds the Spotify and YouTube Music playlists on its own side with "nothing to connect" ([handbook](https://bandjam.app/handbook/playlists/)).
- **Guess-who-submitted, chat and analytics are already taken by BandJam.** It has a guess feature with a separate "Best Friend" leaderboard that does not affect scores, league chat with GIFs and reactions, nudges, deadline reminders and "23 charts" of analytics ([bandjam.app](https://bandjam.app/), [Guess Who](https://bandjam.app/handbook/guess-who/), [notifications](https://bandjam.app/handbook/notifications/)). DJ League gives bonus points for correct guesses ([djleague.app bundle](https://djleague.app/assets/index-CC4CyFLE.js)). So gaps 3, 4, 5 and 6 of study 01 section 4 are partly or fully occupied.
- **Business models differ and only one charges the host.** BandJam: "Free", "No ads" ([bandjam.app](https://bandjam.app/)). Aux Battles: "no paid version, no subscription" ([auxbattles.app](https://auxbattles.app/)). DJ League: ads plus an optional Premiere at "$4/mo" (found in its front-end code, not on a pricing page) ([bundle](https://djleague.app/assets/index-CC4CyFLE.js)). Cut Club: Season Pass "$9.99 / season" with unlimited players, "$1.50 / season" per player, "$99.99 / year" unlimited, and one free trial season ([pricing](https://www.playcutclub.com/pricing), [FAQ](https://www.playcutclub.com/faq)). YapZap price: not verified.
- **Spanish-language market: nothing found.** Searches in Spanish returned only Music League itself and unrelated guessing games (Mystery Mix, Bandle, SongPop). Mystery Mix is an iOS Apple Music "guess who chose it" party game with 0 ratings ([App Store](https://itunes.apple.com/lookup?id=6477337917&country=us)). Several rivals localize the UI (YapZap 12 languages, Aux Battles 6, songbattle FR/ES/PT), so language alone is thin (inference).
- **What looks abandoned:** `bodhello/musicleague` (last commit 2020-10-17), `eeSquared/musicleague-bot` (last commit 2025-06-07), Songlio (now an AI music generator, not a game), JQBX (domain serves a placeholder). Details in the per-product sections.
- **Open lane (inference):** nobody pairs a week-long async league with a live "night" mode, and none has shown the ability to attract users at scale. The unsolved problem in this market looks like distribution, not features: no league clone shows more than the Play "1K+" band (1,000 to 4,999 downloads; BandJam is the highest).

## Comparison table

| Product | Type | Platforms | Music services (how) | Price / model | Traction (stated or store) | Liveness | Maker / country |
|---|---|---|---|---|---|---|---|
| **Music League** (reference) | Async league | Web, iOS, Android | Spotify, Apple Music (API; playlists) | Ads + $2.99/mo or $14.99/yr (study 01) | iOS 6,586 ratings, 4.65; Play 100K+, 2.96K reviews | iOS v1.4.11, 2026-06-24; rebuild announced 2026-11-12 | Music League, LLC, Iowa, US |
| **BandJam** | Async league | iOS, Android, web | Spotify, Apple Music, YouTube Music, TIDAL; YouTube links | Free, no ads | iOS 16 ratings, 4.75; Play 1K+ | iOS v1.29.0, 2026-11-10; Play update 2026-11-20 | Grant's Software LLC, US |
| **DJ League** | Async league | Web, iOS, Android | Spotify, Apple Music, YouTube Music | Free, ads (AdSense), optional Premiere $4/mo | iOS 2 ratings; Play 10+ | iOS v1.0.35, 2026-10-17; Play 2026-10-17 | Individual developer, Colorado, US |
| **YapZap** | Async league + video leagues + daily rooms | iOS, Android, web | Spotify, Apple Music (in-app playback), YouTube Music, TIDAL, Amazon, Deezer, Qobuz | Free listing; any paid tier not verified | iOS 7 ratings, 4.43; Play 100+ | iOS v2.0, 2026-04-07; Play 2026-03-09 | John Pounders, US (Play lists US) |
| **Cut Club** | Seasons (8-12 weeks) + public Daily Cut | iOS, Android, web | YouTube links, Spotify; songs open in Spotify | Host pays per season; free trial season; no ads | iOS 6 ratings, 4.33; Play 50+ | iOS v1.3.47, 2026-11-20; blog 2026-11-19 | Beta Acid, Inc., agency in New York and Barcelona |
| **Aux Battles** (auxbattles.app) | Live room game | Web only | Spotify, YouTube, SoundCloud (embeds; pasted links); Deezer in search | Free, no account, no paid tier | 14,360 players; 4,957 games; 171 self-reported ratings; Discord 82 | v2.18, 2026-09-24; devlog 2026-10-16 | One person, Lithuania |
| **songbattle.io** | Live bracket | Web | Spotify, YouTube, Apple Music, SoundCloud, Suno | Free, "no subscription, no paywall" | 349,645 games; Discord 7,838 | v1.7, 2026-07-26 | songbattle UG, Duisburg, Germany |
| **QueueUp - Music League** | Private async league | iOS | Not stated ("discover and preview music") | Free listing | 1 rating | v1.1.0, 2026-11-07 (released 2026-11-06) | Satellite Media Partners, Inc. |
| **TuneBoxed** | Live battles + daily song + nightly bracket | iOS | Spotify sign-in; previews | Free + "TuneBoxed+" subscription (price not seen) | iOS 21 ratings, 5.0 | v2.25, 2026-11-14 | Aura Brand LLC |
| **Music Leek** | Discord bot, self-hosted | Discord | Spotify URLs and playlists | Free, open source | 1 GitHub star | Last commit 2026-11-15 | Individual (GitHub `snsutton`) |
| **league-of-music** | Web clone, self-hosted | Web | Spotify track URLs | Free | 0 stars | Last commit 2026-10-13 | Individual (GitHub `Master-Chief-117-codes`) |
| **musicleague-bot** | Discord bot | Discord | Links or text | Free | 0 stars | Last commit 2025-06-07 | Individual (GitHub `eeSquared`) |
| **bodhello/musicleague** | Web app source | Web | Spotify | Free | 4 stars | Last commit 2020-10-17 | Individual |

Sources for the table are in the sections below.

## Per-competitor notes

### BandJam
- **What:** Async league with themed rounds. Site: "Social music competitions" ([bandjam.app](https://bandjam.app/)).
- **Mechanics:** Vote budget per round (default "Three up and one down"), optional per-song cap, optional downvotes and upvotes, net scoring, drafts saved to the account, 500-character notes on votes ([Voting and Scoring](https://bandjam.app/handbook/voting-and-scoring/)). Four-step tiebreak: total points, fewest downvotes, best round, correct guesses. Unfinalized ballots lose every upvote the voter's own song earned but keep its downvotes. Guess Who: optional private guesses, separate "Best Friend" leaderboard, no effect on score ([Guess Who](https://bandjam.app/handbook/guess-who/)). Crews persist across leagues, with a shared theme bucket and crew-wide no-repeat song history ([Crews](https://bandjam.app/handbook/crews/)). Also: templates, commissioners, photo prompts, public leagues, 23 analytics charts ([homepage](https://bandjam.app/)).
- **Pacing:** Standard (a phase ends when everyone is done) and Scheduled (four fixed durations, one hour to one month each, with an optional "listening break") ([Pacing](https://bandjam.app/handbook/pacing/)).
- **Reminders:** a day and an hour before a deadline; admins can nudge one person every 12 hours (not in the web app); nothing breaks through Focus mode ([Notifications](https://bandjam.app/handbook/notifications/)).
- **Music integration:** Spotify and YouTube Music playlists are created on BandJam's side with no account or connection. Apple Music builds the playlist in the user's own library, iPhone and iPad only, needing an active subscription. 30-second previews play in voting. Songs submitted as YouTube links are not placed in the Spotify or YouTube Music playlists ([Playlists](https://bandjam.app/handbook/playlists/)).
- **Price:** "Free", "No ads", "nothing to buy" ([homepage](https://bandjam.app/)). No revenue model stated (inference: unfunded or hobby-scale).
- **Traction and liveness:** see table. App Store first release 2025-12-22 ([lookup](https://itunes.apple.com/lookup?id=6756460555&country=us)). Play "Updated on Nov 20, 2026" ([Play](https://play.google.com/store/apps/details?id=app.bandjam)). Copyright "© 2026 BandJam".
- **Company:** Grant's Software LLC, Albany, New York address on Play. Alive and shipping fast (v1.29 in 11 months).

### DJ League
- **What:** Async league. "DJ League is a competitive music league where friends submit songs to themed rounds, generate a shared playlist, vote, and crown a winner. Free to play." ([djleague.app](https://djleague.app/)).
- **Mechanics (from the site's front-end bundle and FAQ, so partly marketing):** private and public leagues; admin sets rounds, pace, songs per player, likes per voter and whether dislikes are allowed; song bans; rule-based bonus-point criteria; points for guessing the submitter (defaults +2 for a correct guess, -1 for being guessed); elimination rounds; theme library; spectators; Discord integration; AI players (Premiere only) ([bundle](https://djleague.app/assets/index-CC4CyFLE.js)). I read these strings as text; I did not run the code.
- **Music:** "Playlists are automatically generated in Spotify, Apple Music, and YouTube Music". Song search runs on those catalogs ([bundle](https://djleague.app/assets/index-CC4CyFLE.js)). The Spotify path likely hits the Spotify API limits in study 01 (inference).
- **Price:** "free to play. We support the app with a small number of advertisements on the public pages." Premiere removes ads: "$4/mo" ([bundle](https://djleague.app/assets/index-CC4CyFLE.js)). No standalone pricing page found. Some analytics charts are gated behind Premiere (same bundle).
- **Platforms:** web; iOS app exists ([App Store](https://itunes.apple.com/lookup?id=6760871879&country=us), released 2026-03-26, 2 ratings); Android Play "10+" downloads ([Play](https://play.google.com/store/apps/details?id=app.djleague.app)).
- **Liveness:** Play and App Store updates 2026-10-17 ("draft song submission"). Built on a no-code/AI site builder (the page carries a Lovable-style artifact tag; inference).
- **Maker:** individual developer (name on Play), Colorado, US.

### YapZap
- **What:** "Music & Video Leagues". Leagues persist across unlimited seasons; members suggest and vote on future themes; submission and voting windows 1 to 14 days; comments; league chat; win streaks; AI theme suggestions; video leagues (YouTube, Instagram, TikTok links) ([App Store listing](https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650)).
- **Latest release notes (v2.0):** "Zap" song recognition, a "Scenes" map of songs being identified nearby, "Daily YapZap" rooms ("fill in 20 minutes and vote in 60"), radio with CarPlay, 12 languages, Qobuz, Discord bot integration, iOS widgets ([lookup](https://itunes.apple.com/lookup?id=6748430650&country=us)). The product is branching away from the pure league format.
- **Music:** "Spotify with full in-app playback", "Apple Music with full in-app playback", YouTube Music playlists auto-generated; others via link matching ("We automatically find every song across all platforms") ([listing](https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650)). How each non-Spotify service integrates is not documented; not verified.
- **Price:** the listing says Free. Whether any in-app purchase or ads exist: not verified (yapzap.com is a single-page app that returned no readable text, and no pricing page was found).
- **Platforms:** iOS ([lookup](https://itunes.apple.com/lookup?id=6748430650&country=us)), web, and Android "100+" downloads, updated 2026-03-09 ([Play](https://play.google.com/store/apps/details?id=com.yapzap.app)).
- **Liveness:** last store update 2026-04-07 (iOS), over 7 months ago. 7 iOS ratings. Looks like a low-activity product (inference).

### Cut Club
- **What:** two games in one app: a public "Daily Cut" (one theme for everyone, about two minutes a day) and private "clubs" running 8, 10 or 12 weekly matchups ([homepage](https://www.playcutclub.com/), [FAQ](https://www.playcutclub.com/faq)).
- **Mechanics:** private clubs: submit one song, then "split 10 points across the rest"; Blind seasons keep picks anonymous until reveal, Open seasons show names throughout (host chooses); emoji reactions; comment threads; recaps, badges, season standings; Slack integration; AI theme generator; pause a season; late joiners play from the current matchup. Daily Cut: vote "Great Cut" or "Not Quite" on five songs a day to keep a streak, then submit a song; ranking weighs approval and vote count; a taste profile ("Crate Digger") built from votes ([FAQ](https://www.playcutclub.com/faq), [pricing](https://www.playcutclub.com/pricing)).
- **Music:** "Every song opens in Spotify, so you can hear it before you vote." Submissions are YouTube or Spotify links ([FAQ](https://www.playcutclub.com/faq)). The store text says "submit a cut with a YouTube link" ([listing](https://itunes.apple.com/lookup?id=6760342114&country=us)). No API-level playback integration is described (inference: link-out only).
- **Price:** Season Pass $9.99 per season (unlimited players); Per Seat $1.50 per player per season ("Good for groups under 7"); Credits $39 for 5 seasons; Unlimited $99.99 per year; "Every new club gets one free trial season... No ads and no monthly subscription required." ([pricing](https://www.playcutclub.com/pricing), [FAQ](https://www.playcutclub.com/faq)). Club creation, season setup and billing stay on the web, not in the app ([listing](https://itunes.apple.com/lookup?id=6760342114&country=us)).
- **Traction:** 6 iOS ratings; Play "50+" downloads ([Play](https://play.google.com/store/apps/details?id=com.cutclub.app)). No user numbers stated.
- **Liveness:** iOS v1.3.47 on 2026-11-20; first iOS release 2026-03-18; a blog post every one to two weeks (latest 2026-11-19), mostly SEO content on team building and "Music League alternative" topics ([blog](https://www.playcutclub.com/blog)). Its comparison posts are marketing, not neutral ([example](https://www.playcutclub.com/blog/5-best-music-league-alternatives-in-2026)). Footer: "© 2026 BETA ACID, INC." Beta Acid describes itself as an agency in New York City and Barcelona ([betaacid.co](https://betaacid.co)).

### Aux Battles (auxbattles.app)
- **What:** live room game. One player creates a room, shares a 4-letter code, everyone joins with a display name, no account. A topic appears, each player submits a song, the room plays all submissions blind and rates each "0.5 to 5 stars"; the highest average wins; submitters are revealed after ([auxbattles.app](https://auxbattles.app/)). About four minutes per round, 3,830 prompts in 16 themes ([compare page](https://auxbattles.app/compare)).
- **Modes:** prompt wheel with custom prompts and respins; bracket mode with anonymous submissions; Twitch chat can submit and vote, no extension needed ([compare](https://auxbattles.app/compare), [v2.18 notes](https://auxbattles.app/)).
- **Music:** pasted Spotify, YouTube or SoundCloud links, played through embedded players. Spotify embeds give the full track to anyone logged into Spotify in that browser, otherwise a 30-second preview. Search pulls from Spotify, YouTube, Deezer and SoundCloud ([auxbattles.app](https://auxbattles.app/)). No Apple Music.
- **Price:** "Free, with no paid tier at all"; "no paid version, no subscription, no in-app purchases and no account" ([auxbattles.app](https://auxbattles.app/), [compare](https://auxbattles.app/compare)).
- **Traction:** 14,360 players, 4,957 games, 31,749 songs, 71,355 votes, "4.91 from 171 player ratings" (self-reported, live counter on the homepage); Discord 82 members ([invite API](https://discord.com/api/v10/invites/M4yxtXK8DK?with_counts=true)).
- **Liveness:** v2.18 on 2026-09-24; six languages since 2026-10-13; devlog 2026-10-16 ([blog](https://auxbattles.app/blog)). Hobby project of one person in Lithuania ([privacy policy](https://auxbattles.app/privacy)); the founder says it was "built in about a week".
- **Not the same product:** an iOS app named "AuxBattle: Song Showdown" (Westfall Group LLC, 2 ratings, judge picks the winner, one-time purchase for prompt packs) is unrelated to auxbattles.app ([lookup](https://itunes.apple.com/lookup?id=6775930155&country=us)).

### songbattle.io
- **What:** head-to-head elimination brackets of up to 128 songs; the audience votes each duel; built for Twitch streams and Discord calls ([songbattle.io](https://songbattle.io/), [for streamers](https://songbattle.io/for-streamers/)).
- **Music:** Spotify, YouTube, Apple Music, SoundCloud, Suno. Exports a game to Spotify or YouTube playlists; matches songs to YouTube music videos; "add all songs" from a playlist or album ([changelog](https://songbattle.io/changelog/)).
- **Price:** "Free, forever. No subscription, no paywall, no catch." ([for streamers](https://songbattle.io/for-streamers/)). How it pays for itself: not verified (the privacy policy says it does not share data for advertising; [privacy](https://songbattle.io/privacy)).
- **Traction:** see Answer. Discord 7,838 members, 986 online.
- **Liveness:** changelog v1.7 on 2026-07-26, v1.6 on 2025-06-10, v1.5 on 2025-02-23. Slow but steady cadence. Copyright "2022-2026".
- **Company:** songbattle UG (haftungsbeschränkt), Duisburg, Germany ([imprint](https://songbattle.io/imprint)).

### QueueUp - Music League
- Private async league on iOS: submit, preview, "rate each submission and edit your votes", achievements, season recaps, notifications. Released 2026-11-06, v1.1.0 on 2026-11-07, 1 rating, Satellite Media Partners, Inc. ([lookup](https://itunes.apple.com/lookup?id=6811379575&country=us)). Music services and price not stated. Too new to judge (liveness: 16 days old).

### TuneBoxed
- Social app with live battle rooms (join by code, no account), "Song of the Day" with daily and weekly leaderboards, a nightly knockout of the day's top 16 songs, and a "Bar for Bar" mode with an AI judge. "TuneBoxed+" is a paid tier (themes, cosmetic items, pick the weekly genre). Spotify sign-in. 21 iOS ratings, v2.25 on 2026-11-14 ([lookup](https://itunes.apple.com/lookup?id=6747647968&country=us)). Adjacent to Music League more than a clone.

### Open-source bots and clones
- **Music Leek** (Discord bot, TypeScript): `/create-league`, `/submit-theme`, `/submit-song`, `/vote`; a theme-submission phase where players suggest prompts and the admin picks; "10-point budget across up to 5 songs"; a DQ marker for players who did not vote; automatic deadline reminders; the admin can create a Spotify playlist from a round. Self-hosted: you create your own Discord bot and Spotify app ([README](https://github.com/snsutton/music-leek)). Created 2025-12-16, last commit 2026-11-15, 1 star ([repo](https://github.com/snsutton/music-leek)). Because Spotify Development Mode now allows 5 users per app (study 01), a self-hosted bot works only for small groups (inference).
- **musicleague-bot** (Python): `/settings`, `/start theme:`, `/submit`, emoji-reaction voting, "up to 3 votes per player", leaderboard ([README](https://github.com/eeSquared/musicleague-bot)). Last commit 2025-06-07, 0 stars. Stale (inference).
- **league-of-music** (web, deployed on Vercel): round-robin prompt author, players "guess who submitted what, then rank their top 3 picks", scoring 2, 1.5 and 1 points, must comment before guessing or ranking, league approval flow, Spotify URL paste and playlist export ([README](https://github.com/Master-Chief-117-codes/league-of-music)). Created 2026-03-04, last commit 2026-10-13, 0 stars.
- **bodhello/musicleague:** last commit 2020-10-17 (a merged PR from the handle `nathancoleman`, the name of a Music League co-founder in study 01); homepage field `musicleague.app` ([repo](https://github.com/bodhello/musicleague)). It is not a fork. I read it as a copy of an early Music League source (inference), not a competitor. Abandoned.
- Other GitHub repos found are stats scrapers or one-off personal projects with 0 to 9 stars: `clydeiii/musicleague`, `media-league` (movies), `amusicleague_clone`, `danielbsimpson/work-music-league-leaderboard` ([GitHub search](https://github.com/search?q=%22music+league%22&type=repositories)). No GitHub topic `music-league-clone` has substantive projects.

### Adjacent products (not leagues)
- **Echo - Rank music!** (Echo Social, Inc): social ranking of albums and songs, 2,083 iOS ratings, v2.1.7 on 2026-11-03 ([lookup](https://itunes.apple.com/lookup?id=6717572746&country=us)). **EQUALS** and **Superfan** are music social networks with feeds, not leagues ([EQUALS](https://itunes.apple.com/lookup?id=6471002462&country=us), [Superfan, Play 5K+](https://play.google.com/store/apps/details?id=com.superfan.app)).
- **Headlights Music League** (REVVSTREET INC): a competition between unsigned artists by city, with fans voting and "prize money". 29 iOS ratings, season 5 live ([lookup](https://itunes.apple.com/lookup?id=1526222689&country=us)). Uses the "music league" name but is a different product.
- **Guessing and party games:** TuneTaste (Android, guess whose song it is, [Play](https://play.google.com/store/apps/details?id=com.tunetaste)), Mystery Mix (iOS, Apple Music, bluff and unmask), Playlist Game (Android, rooms of 1 to 12 rounds, updated 2026-11-05, [Play](https://play.google.com/store/apps/details?id=com.mariussty.playlistgame)). These cover "guess who" as the whole game.

## Mechanics catalogue

Legend: ML = Music League, BJ = BandJam, DJL = DJ League, YZ = YapZap, CC = Cut Club, AB = Aux Battles, SB = songbattle.io, MLk = Music Leek, LoM = league-of-music, QU = QueueUp, TB = TuneBoxed. A blank means no evidence found, not proof of absence. Entries from store text or marketing are weaker than entries from help pages or code.

| Mechanic | Who has it |
|---|---|
| **Voting and scoring** | |
| Fixed point budget spread over songs | ML, BJ, DJL ("likes"), YZ ("allocate points"), CC clubs (10 points), MLk (10 points, max 5 songs) |
| Per-song vote cap | ML, BJ |
| Downvotes (optional or default) | ML (off by default), BJ (1 by default, can be off), DJL (optional) |
| Net score = up minus down | ML (floored at zero per song), BJ (can go negative) |
| Star rating of each song | AB (0.5 to 5 stars), QU ("rate each submission") |
| Binary approve / reject | CC Daily Cut ("Great Cut" or "Not Quite") |
| Ranked top 3 with weights | LoM (2, 1.5, 1) |
| Emoji-reaction votes | musicleague-bot (up to 3) |
| Head-to-head bracket | SB, AB (bracket mode), TB (nightly top 16) |
| Judge picks winner | TB group battles, "AuxBattle: Song Showdown" iOS |
| Penalty for not voting | ML Competitive Mode (lose received upvotes), BJ (always lose upvotes, keep downvotes), MLk (DQ marker) |
| Explicit tiebreak chain | BJ (4 steps); ML not verified |
| Comment attached to a vote | BJ (500 characters), ML (comments while voting) |
| Ballot drafts across devices | BJ |
| **Anonymity and guessing** | |
| Anonymous until reveal | all league products |
| Blind or Open season (host chooses) | CC |
| Guess who submitted, separate board | BJ ("Best Friend"), LoM |
| Guess who submitted, bonus or penalty points | DJL (+2 correct, -1 if guessed, defaults) |
| Reverse bluff (pretend a song is yours) | Mystery Mix (adjacent) |
| **Submission rules** | |
| Song bans, duplicate song/album/artist control | ML, DJL, BJ (crew-wide history) |
| Rule-based bonus points | DJL |
| Several songs per player | ML, BJ |
| Optional submission | ML |
| Photo prompt instead of text | BJ |
| **Theme sourcing** | |
| Admin writes theme | all leagues |
| Members suggest, then vote on themes | YZ, MLk (admin picks) |
| Rotating prompt author | LoM |
| Random draw from a crew theme bucket | BJ |
| Theme library or generator | DJL, CC (AI), YZ (AI), AB (3,830 prompts, wheel) |
| **Social layer** | |
| Chat room per league | BJ, YZ |
| Reactions, GIFs, mentions, threads | BJ, CC (emoji), YZ |
| Nudge a late player | BJ (admin, 12-hour cooldown) |
| Persistent group across leagues | BJ (Crews), YZ, CC (clubs) |
| Public leagues with strangers | ML (old version), BJ, DJL, YZ, CC (Daily Cut) |
| Spectators | DJL |
| Taste matching or profile | BJ ("Best Friend" board), CC (taste type) |
| Streaks | YZ, CC |
| Badges, achievements, crowns | CC, QU, TB |
| League analytics | BJ (23 charts), DJL (Premiere-gated), third-party tools for ML ([musicleaguestats.com](https://musicleaguestats.com/)) |
| AI element | DJL (AI players), TB (AI judge), YZ and CC (theme suggestions) |
| **Pacing** | |
| Fixed deadlines | ML (Steady), BJ (Scheduled), YZ (1 to 14 day windows) |
| Phase advances when all done | ML (Accelerated, Speedy), BJ (Standard) |
| "Listening break" between submit and vote | BJ |
| Seasons ending with a champion | CC (8 to 12 weeks), YZ |
| Elimination of players across rounds | DJL |
| Daily short game | CC Daily Cut, YZ Daily rooms, TB Song of the Day |
| Live room, minutes per round | AB, SB, TB |
| Streamer audience (Twitch chat) | AB, SB |
| **Integrations** | |
| Per-round playlist export | ML, BJ, DJL, YZ, MLk, SB, LoM |
| Discord | DJL, YZ (bot), MLk (is a bot) |
| Slack | CC |
| Run on a call or stream, no account | AB, SB, TB |

## Corrections to study 01

Section 2 of [study 01](../../../../research/01-market-music-league.md) was built from search snippets. Live pages differ as follows.

1. **BandJam ratings and version.** Study: "5.0 from 6 ratings"; "listing from late 2025 or early 2026". Live: 16 ratings, 4.75; v1.29.0 on 2026-11-10; first release 2025-12-22 ([lookup](https://itunes.apple.com/lookup?id=6756460555&country=us)). Play has "1K+" downloads, which study 01 did not have ([Play](https://play.google.com/store/apps/details?id=app.bandjam)).
2. **BandJam and YouTube.** Study: YouTube "by pasting a link". Live: BandJam also builds a YouTube Music playlist automatically, with no account needed, in addition to Spotify; pasted YouTube links are the exception that stays out of playlists ([Playlists](https://bandjam.app/handbook/playlists/)). TIDAL was added in v1.29, which the study lacks.
3. **DJ League has an iOS app.** Study: "iOS not verified". Live: iOS app released 2026-03-26 ([lookup](https://itunes.apple.com/lookup?id=6760871879&country=us)).
4. **DJ League price is not just "Free".** Study: "Free (per its site)". Live: free with ads and an optional Premiere at "$4/mo" that removes ads and gates some features and AI players ([bundle](https://djleague.app/assets/index-CC4CyFLE.js)). Play downloads are "10+", which is the traction figure study 01 said no source gave.
5. **YapZap has an Android app.** Study: "no Android listing found". Live: `com.yapzap.app`, "100+" downloads, updated 2026-03-09 ([Play](https://play.google.com/store/apps/details?id=com.yapzap.app)). Study: "Alive (receives updates)". Live: last iOS update 2026-04-07, 7 ratings. Study omits Qobuz, daily rooms, Zap recognition and the Discord bot. Price is still not verified.
6. **Cut Club playback and price.** Study: "Playback via YouTube, no Spotify dependency". Live: "Every song opens in Spotify"; submissions are YouTube or Spotify links ([FAQ](https://www.playcutclub.com/faq)). Study lists two price points; live has four ($9.99, $1.50, $39 for 5, $99.99 a year) and a free trial season ([pricing](https://www.playcutclub.com/pricing)).
7. **Aux Battles services.** Study: "Spotify, YouTube, YouTube Music, SoundCloud". Live: the page names Spotify, YouTube and SoundCloud, and search also pulls Deezer; YouTube Music is not named ([auxbattles.app](https://auxbattles.app/)). Study gave no traction; live shows 14,360 players. It is a live game, not a Music League clone, so study 01's "five direct clones" overstates it.
8. **songbattle.io traction.** Study gave none. Live: 349,645 games created, 28.8 million votes, Discord 7,838 members. Study's service list (Spotify, YouTube, Apple Music, SoundCloud, Suno) is confirmed.
9. **musicleague-bot activity.** Study: "activity not verified". Live: last commit 2025-06-07, 0 stars.
10. **bodhello/musicleague is not a clone.** Study: "self-hosted web clones". Live: last commit 2020-10-17, with a merged PR from a handle matching a Music League co-founder; I read it as an early copy of Music League's own source (inference).
11. **Songlio.** Study: "Probably dead: redirected to encoremusicians.com". Live: songlio.com serves "Songlio - AI music, tuned to your taste", an AI song generator ([songlio.com](https://songlio.com/)). It left the guessing-game space.
12. **JQBX.** Study: "bought by Turntable LIVE in 2023; current status not verified". Live: jqbx.fm returns a 127-byte placeholder page with no app ([jqbx.fm](https://jqbx.fm/)). deepcut.fm redirects to deepcut.live, which serves a page titled "deepcut.fm - play music together" ([deepcut.live](https://deepcut.live/)). The cause of the JQBX change is not verified.
13. **playlist-party.com.** Study: "Alive". Live: returned HTTP 500 on 2026-11-22 ([playlist-party.com](https://playlist-party.com/)). A single failure; it may be temporary.
14. **Music League rebuild date.** Study 01 section 1 said "autumn 2026, exact date not verified". The announcement post is dated November 12, 2026 ([Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)). That is ten days before this access date. The new help center says Music League asks for Spotify or Apple Music "the first time you search for a song to submit or make a playlist", and that Apple Music needs a paid subscription ([How to Play](https://next.musicleague.com/support/how-to-play)).
15. **Study 01 gaps table, section 4.** Gap 3 (reminders and nudges), gap 4 (chat), gap 5 (stats and a recap) and gap 6 (guess-the-submitter, alternative voting) are all present in BandJam's live docs, with the exception of a "Wrapped"-style recap, which BandJam's analytics page may or may not match (not verified). They are no longer open differentiators on their own.

## Not verified and open questions

1. **YapZap price and in-app purchases.** The site is a script-rendered page with no readable text, and I found no pricing page. The App Store JSON does not list a price.
2. **How YapZap integrates non-Spotify services** (API, link matching, previews). Only the store text is available.
3. **DJ League's `$4/mo` Premiere** comes from strings in its front-end code, not from a pricing page or checkout. Its real price and the ad network volume are not verified.
4. **Real active users of every clone.** Store counts are the only signal. No monthly active user figure exists for BandJam, DJ League, YapZap, Cut Club or QueueUp. Discord counts exist only for Aux Battles and songbattle.io, and none for the four league clones.
5. **Whether any clone has Spotify extended quota.** BandJam says its Spotify playlists are made on its side and need no account ([handbook](https://bandjam.app/handbook/playlists/)), which suggests a server-side Spotify account (inference). How it stays within Spotify's developer policy is not stated. This matters for the decision map's Spotify ticket.
6. **songbattle.io funding.** The site says free forever. No ads or donations were visible in what I could read. The "Support Us" link target was not readable.
7. **Product Hunt and Hacker News.** Product Hunt returned a 403 to automated fetches; a Product Hunt web search found no Music League-style product. The HN Algolia API found no relevant "Show HN". Neither proves absence.
8. **Spanish-language and other non-English products.** Searches in Spanish and App Store/Play searches for "liga musical" and "juego de canciones amigos" found none. Searches in other languages were not done.
9. **Google Play search** returns only Music League for "music league"; the clones do not rank in the first 20 results ([Play search](https://play.google.com/store/search?q=music+league&c=apps)). I read this as weak discoverability (inference); I did not test other regions.
10. **Hangout.fm** (a "listening party" companion for Music League playlists, per a search summary) now shows a page for "GRAI: Music with friends" with an email waitlist ([hangout.fm](https://hangout.fm/blog/posts/hangout-and-music-league)). Its status and relation to Music League are not verified.
11. **Music League's current tiebreak rules and paid tiers** were not re-checked in this ticket.

## Sources

**Apple App Store (lookup API, US storefront)**
- https://itunes.apple.com/lookup?id=1589815321&country=us (Music League)
- https://itunes.apple.com/lookup?id=6756460555&country=us (BandJam)
- https://itunes.apple.com/lookup?id=6748430650&country=us (YapZap)
- https://itunes.apple.com/lookup?id=6760342114&country=us (Cut Club)
- https://itunes.apple.com/lookup?id=6760871879&country=us (DJ League iOS)
- https://itunes.apple.com/lookup?id=6811379575&country=us (QueueUp)
- https://itunes.apple.com/lookup?id=6747647968&country=us (TuneBoxed)
- https://itunes.apple.com/lookup?id=6775930155&country=us (AuxBattle: Song Showdown)
- https://itunes.apple.com/lookup?id=6717572746&country=us (Echo)
- https://itunes.apple.com/lookup?id=1526222689&country=us (Headlights Music League)
- https://itunes.apple.com/lookup?id=6477337917&country=us (Mystery Mix)
- https://itunes.apple.com/lookup?id=6471002462&country=us (EQUALS)
- https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650
- https://itunes.apple.com/search?term=music%20league&entity=software&country=us (and terms "song league", "music competition friends", "liga musical", "juego de canciones amigos")

**Google Play listings**
- https://play.google.com/store/apps/details?id=app.bandjam
- https://play.google.com/store/apps/details?id=app.djleague.app
- https://play.google.com/store/apps/details?id=com.yapzap.app
- https://play.google.com/store/apps/details?id=com.cutclub.app
- https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US
- https://play.google.com/store/apps/details?id=com.superfan.app
- https://play.google.com/store/apps/details?id=com.tunetaste
- https://play.google.com/store/apps/details?id=com.mariussty.playlistgame
- https://play.google.com/store/search?q=music+league&c=apps

**Competitor sites**
- https://bandjam.app/ , https://bandjam.app/handbook/voting-and-scoring/ , https://bandjam.app/handbook/guess-who/ , https://bandjam.app/handbook/playlists/ , https://bandjam.app/handbook/pacing/ , https://bandjam.app/handbook/notifications/ , https://bandjam.app/handbook/crews/
- https://djleague.app/ , https://djleague.app/assets/index-CC4CyFLE.js
- https://yapzap.com/
- https://www.playcutclub.com/ , https://www.playcutclub.com/pricing , https://www.playcutclub.com/faq , https://www.playcutclub.com/blog , https://www.playcutclub.com/blog/5-best-music-league-alternatives-in-2026 (secondary, marketing) , https://betaacid.co
- https://auxbattles.app/ , https://auxbattles.app/compare (a competitor's marketing comparison) , https://auxbattles.app/blog , https://auxbattles.app/privacy
- https://songbattle.io/ , https://songbattle.io/changelog/ , https://songbattle.io/for-streamers/ , https://songbattle.io/imprint , https://songbattle.io/privacy
- https://songlio.com/ , https://jqbx.fm/ , https://deepcut.live/ , https://playlist-party.com/ , https://hangout.fm/blog/posts/hangout-and-music-league
- https://musicleaguestats.com/

**Music League (current help center)**
- https://next.musicleague.com/news/why-we-rebuilt-music-league
- https://next.musicleague.com/support/how-to-play
- https://next.musicleague.com/support/league-rules-and-scoring
- https://next.musicleague.com/support/league-schedule-and-pacing

**Source repositories (GitHub)**
- https://github.com/snsutton/music-leek
- https://github.com/eeSquared/musicleague-bot
- https://github.com/Master-Chief-117-codes/league-of-music
- https://github.com/bodhello/musicleague
- GitHub search API, queries `topic:music-league`, `"music league" in:name,description`, `music-league-clone`, `musicleague discord bot` (run 2026-11-22)

**Other**
- https://discord.com/api/v10/invites/p6bBfxY7bN?with_counts=true (songbattle.io server), https://discord.com/api/v10/invites/M4yxtXK8DK?with_counts=true (Aux Battles server): public invite metadata, member counts at access time
- https://hn.algolia.com/api/v1/search (queries "music league", "song league", "music league alternative"; no relevant results)
- https://www.periodismo.com/2026/11/15/una-plataforma-para-jugar-con-playlists-de-spotify/ (Spanish press piece about Music League itself, secondary)
- Study 01: /workspace/AI Projects/JN C Crate/research/01-market-music-league.md
