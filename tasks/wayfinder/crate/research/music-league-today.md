# Music League today, verified

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [Music League today, verified](../01-music-league-today.md)

Method: I opened the pages themselves (next.musicleague.com help center, news, Terms, Privacy; the App Store and Google Play listings; Spotify's Developer Policy and quota docs; two interviews). The new help center pages carry no date, except the news post, Terms, Privacy and Community Guidelines. "1.0" is the legacy product, "2.0" the rebuilt one at next.musicleague.com; these are Music League's own labels.

## Answer

- **The rebuilt version is a public beta, not a finished relaunch.** The news post dated 2026-11-12 opens with "This is in regards to a Beta version of 2.0" and says 1.0 will be restricted "when 2.0 gets out of the Beta phase" ([news post](https://next.musicleague.com/news/why-we-rebuilt-music-league)). The store apps (App Store 1.4.11, Google Play updated 2026-06-22) are still the legacy app; the new iPhone app is a TestFlight beta ([iOS beta page](https://next.musicleague.com/ios-beta), [App Store](https://apps.apple.com/us/app/music-league/id1589815321), [Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US)).
- **Game settings are deep and mostly admin-controlled.** Songs per player 0–10, upvote pool 0–100, optional downvotes 1–100, per-song caps, three pacing modes, 1–14 day phases, three comment-visibility modes, duplicate song/artist control, Competitive Mode (off by default), 2–100 players, playlist cap 100 songs, 20 rounds for public leagues and no cap for private ones ([League Rules](https://next.musicleague.com/support/league-rules-and-scoring), [Schedule](https://next.musicleague.com/support/league-schedule-and-pacing), [Privacy of leagues](https://next.musicleague.com/support/league-privacy)). Tie-breaking is not documented anywhere I could read.
- **The social layer is bigger than study 01 said.** Per-league chat and song threads, @mentions, follow/block, an activity feed with posts, profile placements, a global "Charts" of most-submitted songs, and a Year-in-Review. Direct messages, friending and muting are "not available yet" ([Follow and Friend](https://next.musicleague.com/support/follow-and-friend), [Notifications](https://next.musicleague.com/support/league-notifications), [The Charts](https://next.musicleague.com/support/the-charts), [How to Play](https://next.musicleague.com/support/how-to-play)).
- **Reminders exist on three channels (in-app, email, push), all on by default and configurable per type.** A reminder goes out about 24 hours before a deadline to players who have not acted; admins get a 24-hour deadline warning plus batched activity digests ([Notifications](https://next.musicleague.com/support/league-notifications)).
- **Music services: Spotify and Apple Music only.** Sign-in is email, Spotify or Apple. A service is needed to search, play and build playlists; Apple Music requires a paid subscription, Spotify Free works with a 30-second preview track added for songs not on the free tier ([Connecting a music service](https://next.musicleague.com/support/connecting-spotify)). Playlists now go into each player's own library. YouTube Music is not offered; the help page asks users to email a request for more services.
- **Money: free with ads, Premium removes ads and unlocks CSV export.** US App Store: $2.99/month or $14.99/year. No third tier exists in the 12 storefronts I could open; higher numbers are local-currency prices (CA$19.99, A$22.99, NZ$29.99 per year). The 2.0 price is login-gated and not verified ([App Store US](https://apps.apple.com/us/app/music-league/id1589815321), [Premium help](https://next.musicleague.com/support/whats-included-in-premium)).
- **Spotify's "Do not create a game" rule: no public statement explains how Music League fits.** The rule is live in the policy effective 2025-05-15 ([Spotify Developer Policy](https://developer.spotify.com/policy)). The only statement I found is the CEO in 2025: Spotify is "kind enough to allow it", with no discussions "beyond what we're currently doing" ([MusicRadar](https://www.musicradar.com/music-industry/we-speak-to-the-maker-of-a-game-putting-the-humanity-back-into-music-discovery)). Its Terms and Privacy Policy do not mention Spotify at all. Everything beyond that is inference (see section 7).
- **Minimum age is 16** in both the Terms and the Privacy Policy (both last updated 2026-11-09), while the App Store rates the app 13+ ([Terms](https://next.musicleague.com/terms), [Privacy](https://next.musicleague.com/privacy), [App Store](https://apps.apple.com/us/app/music-league/id1589815321)).

## 1. League and round settings (2.0)

Source for the table unless stated: [League Rules and Scoring](https://next.musicleague.com/support/league-rules-and-scoring), [Voting Rules](https://next.musicleague.com/support/voting-rules-and-auto-adjustment), [Creating and Editing Leagues](https://next.musicleague.com/support/creating-a-league), [Schedule](https://next.musicleague.com/support/league-schedule-and-pacing). The wizard has five steps: Identity, Rounds, Timing, Settings, Launch ([How to Play](https://next.musicleague.com/support/how-to-play)).

| Setting | What the help center says | Locked at launch? |
|---|---|---|
| Songs per player | "Max songs per player... Anywhere from 0 to 10"; "must submit" 0–10, below the max for partial submissions. Must = 0 makes submitting optional, Steady leagues only | Editable; a change waits for the next round |
| Upvotes | Pool 0–100 per round; "must distribute" 0–100, never above the pool; max per song. Pool = 0 gives a no-score "discovery-and-conversation" league, Steady only | Yes: "Total upvotes per player, max upvotes per song" locked |
| Downvotes | "optional and turned off by default"; may distribute 1–100, must 0 to the "may" number, per-song cap. Must-downvotes require Competitive Mode | Yes, all downvote settings locked |
| Own songs | "Players can never vote on their own submissions" | n/a |
| Scoring | Song score = upvotes minus downvotes, floored at zero. Standings show a percentage: net score divided by the best possible score in that round | Rules locked |
| Competitive Mode | A player who skips mandatory votes "forfeits all the upvotes their submission earned that round"; downvotes against them still count. Off by default | Yes, locked |
| Auto-adjust | If a round has too few songs, the per-song cap is raised just enough so must-spend votes fit; never lowered; optional votes that do not fit are lost; admin is notified | Automatic |
| Pacing | Steady (fixed deadlines), Accelerated (phase ends when everyone is done, deadlines unchanged), Speedy (next phase opens at once) | Editable |
| Phase length | Submission 1–14 days, voting 1–14 days; per-round overrides; breaks between rounds; admin can advance a phase or extend a deadline | Editable |
| Comments | Optional comment per song, up to 5,000 characters. Visibility: during voting (default), at reveal, or player's choice per song | Round toggles lock when voting opens ([Comments](https://next.musicleague.com/support/song-comments-and-visibility)) |
| Vote breakdown | After results, shows how each player voted (default on); off shows totals only | Editable |
| Live tally | Admin picks one of four "voting progress windows" for leagues of 6+ players; under 6 players voting is blind | Per round until voting opens |
| Who has submitted/voted | Show icons (default) or a progress bar only | Lock when voting opens |
| Duplicates | Same song cannot be submitted twice in one round (filter "not perfect" for alternate releases). Songs seen in earlier rounds give a warning and a tag but are allowed. Artist repeat can be banned league-wide (set at creation) or per round; a banned artist is blocked | League-wide choice locked |
| Private/public | Private: not listed, invite link joins need admin approval, in-app invites do not. Public: listed in Discover, anyone joins instantly. Public to Private is allowed, never back | One-way |
| Players | "from two people to one hundred"; playlist cap 100 songs per round, so players × songs per player must be at most 100; a max-players value can be set and changed | Editable |
| Rounds | At least one; private leagues unlimited, public 20 ([League privacy](https://next.musicleague.com/support/league-privacy)); only unstarted rounds or the latest completed round can be deleted | n/a |
| Rounds with too few songs | Fewer than two submitters: voting phase holds, no playlist, no points | n/a ([Lifecycle](https://next.musicleague.com/support/league-lifecycle)) |
| Missed deadlines | No submission: cannot vote that round. Saved but unsubmitted ballot: auto-submitted at the deadline. Nothing saved: not counted | n/a |
| Mid-league joiners | Can join while ongoing; cannot vote until they have submitted a song ([Inviting players](https://next.musicleague.com/support/inviting-players)) | n/a |
| Ending and reviving | League completes automatically; a round can be added within about two months; locked after six months | n/a |

**Tie-breaking: not documented.** I searched all 28 help-center pages, the Terms and the news post for "tie", "tied" and "tiebreak"; there is no rule. Treat as unknown. Not verified because the app itself needs a login.

Also in 2.0: a theme library, custom theme text, league artwork, an invitation e-mail template, drafts, ballot order identical for everyone and equal to playlist order, per-user "you've submitted this before" reminders, a demo league without account ([Themes](https://next.musicleague.com/support/choosing-round-themes), [Demo](https://next.musicleague.com/demo)).

## 2. Reminders and notifications

Source: [Notifications](https://next.musicleague.com/support/league-notifications) (undated).

- **Channels:** In-app, Email, Push (browser/device push; per browser and per device). Each notification row has its own switch per channel. Every toggle is account-wide, not per league. All player notifications are on by default.
- **Player groups:** Round activity (round opens, voting opens, voting deadline extended or shortened, results ready); Reminders (submit before the deadline, vote before the deadline); Chat mentions (@mention or thread reply: in-app and push only, never email; any new league chat message: email allowed; song-thread comments and replies).
- **Reminder timing:** "the reminder sent about 24 hours before the deadline and the nudges sent when the league is waiting on you". Skipped if you already acted. The exact count and timing of the "nudges" is not stated.
- **Schedule shifts:** when an admin change moves later rounds, everyone gets one "bell-only" heads-up even if the related toggle is off.
- **Admins:** a digest of invites accepted or declined, players leaving, songs submitted and votes submitted, sent "about every 3 hours, or sooner once 5 things have happened"; a 24-hour deadline warning when someone has not acted (in-app, email, push); join requests for private leagues (cannot be turned off); @admin mentions; report alerts (always on).
- **Marketing:** a separate Newsletter & Marketing switch. Account and security emails cannot be turned off.
- **Not available:** SMS or other channels are not mentioned. Per-player reminder channel choice beyond the three above does not exist. Legacy 1.0 reminders: not verified (no primary source found; release notes mention only "push notification reliability", 1.4.6, 2026-04-30, [App Store](https://apps.apple.com/us/app/music-league/id1589815321)).

## 3. Social features

| Feature | Status in 2.0 | Source |
|---|---|---|
| Song comments and replies | Yes; threads continue after a round ends, even in completed leagues | [Comments](https://next.musicleague.com/support/song-comments-and-visibility), [Lifecycle](https://next.musicleague.com/support/league-lifecycle) |
| League chat | Yes ("league chat", @league, @admin, thread replies); moderated by admins | [Notifications](https://next.musicleague.com/support/league-notifications), [Admin tools](https://next.musicleague.com/support/admin-moderation-tools) |
| Direct messages | "Coming later"; "chat lives inside leagues, not between individual players" | [Follow and Friend](https://next.musicleague.com/support/follow-and-friend) |
| Follow and block | Follow is one-way and notifies the other person; blocking is reciprocal and hides comments, chat and profile, without changing scores | same |
| Friend (two-way) and mute | Not available yet | same |
| Activity feed | Text, link and photo posts, comments and replies, one-click "Share to my feed" for submissions; visibility set per item (league mates, followers, anyone) | same |
| Profile and stats | Photo, followers and following counts, placements (1st to 3rd in leagues and rounds), latest submission; refreshed standings with a rank chart; private "submitted before" reminders | [Follow and Friend](https://next.musicleague.com/support/follow-and-friend), [How to Play](https://next.musicleague.com/support/how-to-play) |
| The Charts | Home-page ranking of most-submitted songs across public leagues (not private ones), 30-second previews, filter by followers or people you played with | [The Charts](https://next.musicleague.com/support/the-charts) |
| History | Past leagues, standings, submissions, profile info and statistics migrate from 1.0 | [News post](https://next.musicleague.com/news/why-we-rebuilt-music-league) |
| Year-in-Review | Banner "late December through mid-February"; export as PDF or public link | [How to Play](https://next.musicleague.com/support/how-to-play) |
| Reactions (emoji) | None documented | all help pages searched |
| Discover | Public leagues listed with filters (most players, almost full, starting soon, newest) | [Discover](https://next.musicleague.com/discover) |
| Export | Premium only: one CSV with sections for rounds, submissions (incl. Spotify track ID), votes, comments, standings; empty votes section if the breakdown is hidden | [Exporting](https://next.musicleague.com/support/exporting-league-data) |
| Moderation | Report to admin or to Music League; hide, delete, kick, ban; public leagues are reviewed by Music League | [Community Guidelines](https://next.musicleague.com/support/community-guidelines) (updated 2026-11-03) |

## 4. Music services

| Function | Spotify | Apple Music |
|---|---|---|
| Sign-in | "Sign in with Spotify"; creates the account and connects the service. Account email must match; Spotify accounts without email cannot sign in this way | "Sign in with Apple" signs you in only; Apple Music is connected separately |
| Account type | Free or Premium | "active paid subscription"; free Apple accounts do not work |
| Search | Inside the app, plus pasting a Spotify link or picking recently listened (if Spotify is primary) | Inside the app |
| Playback | Plays in Spotify; Free users hear audio ads and may see Spotify-placed songs that cannot be voted on | Plays in Apple Music |
| Playlists | Created on demand: "The first player in the league to tap Generate" builds it; others tap Open, then + to save | Auto-saved to each player's library when voting opens |
| Free tier | Unavailable songs get an extra 30-second preview track for Free listeners | n/a |

Sources: [Connecting a music service](https://next.musicleague.com/support/connecting-spotify), [Signing in](https://next.musicleague.com/support/signing-in-to-music-league), [How to Play](https://next.musicleague.com/support/how-to-play), [Playlists](https://next.musicleague.com/support/league-playlist).

- Players can browse, accept invites, join leagues, create leagues and vote without a service; one is asked for at the first song search or playlist ([Connecting](https://next.musicleague.com/support/connecting-spotify)).
- If both are connected, the player chooses a primary one. Cross-service play is implied: songs "on very rare occasions" are missing in one of the two catalogs.
- "Will Music League connect to other music services? We would love to": users are asked to email support@musicleague.com with the subject "Additional Music Streamer". No YouTube Music, Tidal or Deezer.
- Round and league playlists used to come from one shared Music League Spotify account; now they are created in each user's own library ([Moving to the new Music League](https://next.musicleague.com/support/moving-to-the-new-music-league)).
- Legacy app listing (still live): "an anonymous, shuffled Spotify playlist... a free (or paid) Spotify account is required" ([App Store](https://apps.apple.com/us/app/music-league/id1589815321)); the Google Play listing adds that "Spotify will add songs to any playlist with less than 15 songs" ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US)).
- Where the 30-second previews (including those on The Charts) come from is not stated. Not verified.

## 5. Plans, prices, ads

**Premium scope (2.0 help):** "removes ads from your experience and lets you export your league data as a CSV file. Everything else... works the same". It can be bought through the app stores or on the web; gifts of 1, 3, 6 or 12 months are sold from the Profile page and do not auto-renew; the price is "listed on your Profile page... can vary by region" ([Premium help](https://next.musicleague.com/support/whats-included-in-premium)). The news post says "We are also offering lower prices for Premium users" ([news post](https://next.musicleague.com/news/why-we-rebuilt-music-league)). Actual 2.0 prices: **not verified** (behind login).

**Legacy store prices ("Ad Free Leagues", auto-renewing, App Store storefronts read 2026-11-22):**

| Storefront | Monthly | Annual |
|---|---|---|
| US | $2.99 | $14.99 |
| UK | £2.99 | £14.99 |
| Ireland | €2.99 | €17.99 |
| Canada | $3.99 (CAD) | $19.99 |
| Australia | $4.99 (AUD) | $22.99 |
| New Zealand | $4.99 (NZD) | $29.99 |
| Singapore | S$3.98 | S$19.98 |
| Denmark / Norway | 29 kr / 39 kr | 129 kr / 199 kr |
| Poland | 14,99 zł | 69,99 zł |
| South Africa | R59.99 | R299.99 |
| India | ₹299 | ₹1,499 |

URLs: `https://apps.apple.com/<cc>/app/music-league/id1589815321` for each country code, for example [US](https://apps.apple.com/us/app/music-league/id1589815321), [CA](https://apps.apple.com/ca/app/music-league/id1589815321), [AU](https://apps.apple.com/au/app/music-league/id1589815321), [NZ](https://apps.apple.com/nz/app/music-league/id1589815321). Storefronts for DE, FR, ES, IT, NL, SE, MX, JP and BR did not load (proxy errors, not proof of absence).

- **Is there a tier above $14.99/year?** I found no separate tier: every storefront lists exactly two products, monthly and annual. The numbers above $14.99 are local-currency prices of the same annual product. The AppsHunter claim of $24.99 could not be reproduced (the site returned 403). It may be a regional price (the AU annual is A$22.99), but that is an inference. Not verified.
- **Ad provider:** Nitro (Overwolf's ad network) on the web: the 2.0 Privacy Policy lists Nitro consent cookies and a "Music League (read by Nitro)" opt-out cookie, and the page security policy allows Nitro's script plus Google Ad Manager and AppNexus ad domains ([Privacy](https://next.musicleague.com/privacy), [Nitro interview](https://blog.nitropay.com/publisher-showcase-music-league/)). The Discover page shows a "Sponsored" slot with a "Remove ads" link ([Discover](https://next.musicleague.com/discover)). Mobile ad provider: not verified.
- **Ad stance:** the CEO says the old app "crumbles under its own weight" on ads and plans a model where "all the ads go away, every feature is free", funded by brands, artists and labels once the app reaches about 500,000 monthly users ([Iowa Tech Podcast, 2026-09-08](https://iowapodcast.com/music-league-eric-west/)). A plan, not a commitment.
- **Legacy ad mechanics (iOS release notes):** watch-an-ad rewards from 1.4.0 (2026-01-23); "5 hours ad-free" for rewarded ads in 1.4.4 (2026-03-29); "ad-free experience for your first 14 days after signing up" in 1.4.5 (2026-04-15); "Redesigned Ads & Paywall" in 1.4.6 (2026-04-30) ([App Store](https://apps.apple.com/us/app/music-league/id1589815321)). The release-note layout puts each note above its version label; I read them that way.
- **Merch:** an official store at store.musicleague.com, advertised in the site header ([Discover](https://next.musicleague.com/discover)).

## 6. Relaunch timeline and store status

| Date | Event | Source |
|---|---|---|
| 2025-01-21 | Last update of the legacy Terms (still online) | [old Terms](https://musicleague.com/terms/) |
| 2025-05-22 | CEO interview; says Spotify is "kind enough to allow it" | [MusicRadar](https://www.musicradar.com/music-industry/we-speak-to-the-maker-of-a-game-putting-the-humanity-back-into-music-discovery) |
| 2026-06-22 / 06-24 | Latest legacy releases: Google Play update; App Store 1.4.11 | [Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US), [App Store](https://apps.apple.com/us/app/music-league/id1589815321) |
| 2026-09-08 | Podcast: 1.1M registered, ~200,000 monthly players; Version 2 "targeted for late August" in the summary and "coming out in a few weeks" in the transcript (dates disagree, so the target slipped) | [Iowa Tech Podcast](https://iowapodcast.com/music-league-eric-west/) |
| 2026-11-03 | New Community Guidelines | [Community Guidelines](https://next.musicleague.com/support/community-guidelines) |
| 2026-11-09 | New Terms and Privacy Policy for next.musicleague.com | [Terms](https://next.musicleague.com/terms), [Privacy](https://next.musicleague.com/privacy) |
| 2026-11-12 | Beta announcement post | [news post](https://next.musicleague.com/news/why-we-rebuilt-music-league) |
| 2026-11-22 | Still beta; no 2.0 in the stores; iOS TestFlight page live; Android beta page returns 404 | [iOS beta](https://next.musicleague.com/ios-beta) |

- **Old leagues:** history (completed and active leagues, standings, submissions, profile, statistics) appears automatically, "as long as you connect the same Spotify account you used before". Leagues in progress "finish there": 2.0 links out to the 1.0 web app ([Moving to the new Music League](https://next.musicleague.com/support/moving-to-the-new-music-league)).
- **1.0 sunset:** creation and editing in 1.0 will be "restricted" after beta; new league creation "will eventually be disabled altogether, with advance notice"; 1.0 mobile apps "will not be maintained or updated" after 2.0 is in the stores ([news post](https://next.musicleague.com/news/why-we-rebuilt-music-league)).
- **Public leagues:** live in 2.0 today (Discover lists leagues in progress, with join buttons). Study 01 said they did not exist yet.
- **Beta caveat for admins:** three 1.0 mobile admin tools (exact time resets, mid-league setting edits, inviting past league mates in-app) do not exist in 2.0 mobile; admins of active leagues are advised to wait ([iOS beta page](https://next.musicleague.com/ios-beta)).
- **Platforms:** web and installable PWA (Chrome, Edge, Safari on Mac; not Firefox) ([Installing](https://next.musicleague.com/support/installing-music-league-on-your-computer)).
- **Traction (secondary, CEO statements):** 1.1M+ registered, ~200,000 monthly players in 170 countries ([Iowa Tech Podcast](https://iowapodcast.com/music-league-eric-west/)); "essentially nothing" spent on acquisition ([Nitro](https://blog.nitropay.com/publisher-showcase-music-league/)). Store signals: iOS 4.7 from 6.6K US ratings; Google Play 4.6, 2.96K reviews, 100K+ downloads.

## 7. Spotify's game rule and Music League

**What the rule says.** Developer Policy, effective 15 May 2025, section III, "Some prohibited applications": "Do not create a game, including trivia quizzes." The same section also bans "any product or service which is integrated with streams or content from another service" and any product "targeted to children" ([Developer Policy](https://developer.spotify.com/policy)). Compliance Tips give "a 'name that tune' quiz" as a disallowed example ([Compliance Tips](https://developer.spotify.com/compliance-tips)). A reply marked as the accepted answer on Spotify's developer forum tells a trivia-game developer that such an app "isn't eligible for a quota extension" and that "there isn't a workaround or exception"; whether the answerer is Spotify staff is not verified ([Spotify Community](https://community.spotify.com/t5/Spotify-for-Developers/Extended-Quota-Mode-Request-Independent-Developer-TrackLine/td-p/7384615)). Extended quota is now for organizations with "at least 250k MAUs" and a compliance review ([Quota modes](https://developer.spotify.com/documentation/web-api/concepts/quota-modes)).

**What Music League has said.**
- 2025-05-22, CEO Eric West asked whether Music League could integrate more directly with Spotify: "There's not been direct discussions about anything beyond what we're currently doing... they're kind enough to allow it" ([MusicRadar](https://www.musicradar.com/music-industry/we-speak-to-the-maker-of-a-game-putting-the-humanity-back-into-music-discovery)).
- 2026-09-08, the CEO describes relationships with record labels but says nothing about Spotify's developer terms ([Iowa Tech Podcast](https://iowapodcast.com/music-league-eric-west/)).
- Music League's Terms (updated 2026-11-09) and Privacy Policy do not name Spotify; the Privacy Policy names Apple Music only in a cookie table ([Terms](https://next.musicleague.com/terms), [Privacy](https://next.musicleague.com/privacy)). The legacy Terms (updated 2025-01-21) do not name Spotify either ([old Terms](https://musicleague.com/terms/)).
- I found no Spotify statement, no listing in Spotify's developer materials, and no press article that addresses Music League and the game rule. Whether it has extended quota, a partner agreement, or a tolerance, is **not verified**. Absence of evidence is not evidence of an agreement.

**What the product design suggests (all inference).**
- Playback happens inside Spotify, from a playlist created in the player's own library; Free users hear Spotify's own ads ([Connecting](https://next.musicleague.com/support/connecting-spotify)). That looks like a non-streaming app under Spotify's definitions, which may sell ads and access ([Developer Policy, section IV](https://developer.spotify.com/policy), [Compliance Tips](https://developer.spotify.com/compliance-tips)). It would explain why ads and a subscription are allowed. Spotify has not said so.
- The 200,000 monthly players are below the 250,000 threshold and 2.0 adds Apple Music, so extended access, if it exists, is most likely inherited from before the May 2025 rules.
- Music League is in practice tolerated or classified differently; the sources cannot tell which.

## Corrections to study 01

Study 01 ([research/01-market-music-league.md](../../../../research/01-market-music-league.md)) was built from snippets. Against the live pages:

1. **"Full rebuild (autumn 2026, exact date not verified)"** is imprecise. The post is dated 2026-11-12, explicitly a **Beta** of 2.0, with store apps unchanged and Android beta unconfirmed. Terms and Privacy for 2.0 are dated 2026-11-09. A podcast on 2026-09-08 said "a few weeks"; the target slipped.
2. **"The new version has no public leagues yet"** is wrong. Discover lists public leagues, with join buttons and a Sponsored ad slot; Community Guidelines describe public-league review.
3. **"There is no evidence of player-to-player chat"** is wrong for 2.0: league chat, song threads and @mentions exist. Only direct messages are missing. Legacy also had chat (release note 1.3.8, 2025-12-15, "opening the chat").
4. **"Export: a ZIP holding four CSVs"** describes the legacy export (a third-party repo, not a primary source). 2.0 exports one CSV with five sections and only for Premium subscribers.
5. **"All gameplay and admin tools stay free"** is right, but the export is a Premium feature; "ads removed plus CSV export" is the full Premium scope.
6. **AppsHunter's $24.99** is not an extra tier. Each storefront lists two products; annual prices vary by currency (CA$19.99, A$22.99, NZ$29.99, €17.99).
7. **"Competitive Mode replaces the old 'low stakes' setting"** is not stated on any 2.0 page I read. The legacy guide says missing a voting deadline discards points "unless an admin has activated the 'low stakes' setting" ([legacy guide](https://musicleague.com/user-guide/)); in 2.0 no penalty is the default and Competitive Mode is the opt-in. The inversion is documented; "replaces" is an inference.
8. **Limits:** study 01 was right on 2–100 players, 100-song playlist, 20-round public cap, and pacing modes. Added precisely: songs per player 0–10, upvotes 0–100, downvotes 1–100, phase length 1–14 days. The legacy guide's 100-round limit is confirmed ([legacy guide](https://musicleague.com/user-guide/)).
9. **Comments:** study 01 said the admin "decides when comments become visible". Precisely: three modes (during voting, at reveal, player's choice per song) and a 5,000-character limit.
10. **Spotify Free:** confirmed, with two extras: Free users hear Spotify audio ads and may see Spotify-placed songs in playlists that cannot be voted on.
11. **Ad provider:** confirmed for the web (Nitro in the Privacy Policy cookie table and page security headers). Google Ad Manager and AppNexus domains are also allowed there, which study 01 did not mention.
12. **Traction dates:** the podcast is dated 2026-09-08 on the page itself (study 01 inferred it from search metadata).
13. **Reminders:** "which reminder channels exist today is not verified" is now answered (section 2).
14. **Min age** was not in study 01: 16 in Terms and Privacy; App Store shows 13+; Google Play shows PEGI 3 (listing, [Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US)). I did not check how sign-up enforces age.
15. **Open question 1** is only partly narrowed: no explanation exists; the only primary statement is "kind enough to allow it".

## Not verified and open questions

Study 01 "Open questions" status:

| # | Question | Status |
|---|---|---|
| 1 | How Music League fits the Spotify game rule | **Open.** Only the 2025 CEO quote; the rest is inference (section 7). A lawyer or a direct question to Spotify would be needed. |
| 2 | Relaunch date; Premium change | **Answered in part.** Beta since at least 2026-11-12; no final date announced. 2.0 price: not verified (login-gated), "lower prices" only as a claim. |
| 3 | Tier above $14.99 | **Answered.** None found; regional prices only. The $24.99 source was not reproducible. |
| 4 | Tie-breaking, reminder channels | Reminders **answered** (in-app, email, push, configurable). Tie-breaking **not documented**; would need a test league. |
| 5 | Player chat beyond comments | **Answered.** Yes, league chat and song threads; no DMs. |

Other items not verified:
- 2.0 Premium prices and the exact "lower" amount; whether web purchase has its own price.
- Whether the new Android app is in beta (the post says both are; no Android beta page found).
- Source of the 30-second previews and whether Spotify's API is used for them.
- How age is enforced; how data from Spotify or Apple Music is used (neither policy describes music-service data uses).
- Privacy Policy detail: it says Music League "may sell" personal data and lists ad networks as recipients of identifiers, activity, geolocation and inferences "to show and measure advertising that pays for the free version"; the Google Play listing states "No data shared with third parties". These conflict; the Play listing may describe the legacy app.
- Mobile ad provider and the share of revenue from ads versus Premium (a fathom.tools estimate in study 01 remains unverified).
- Whether public-league volume in 2.0 is significant (Discover showed four leagues in progress on one visit; not a statistic).
- Any Spotify-side confirmation of Music League's quota status. Spotify's developer dashboard is private.

## Sources

**Music League, new version (next.musicleague.com)**
- https://next.musicleague.com/news/why-we-rebuilt-music-league (2026-11-12)
- https://next.musicleague.com/support (index; 28 articles read)
- https://next.musicleague.com/support/how-to-play
- https://next.musicleague.com/support/creating-a-league
- https://next.musicleague.com/support/league-rules-and-scoring
- https://next.musicleague.com/support/voting-rules-and-auto-adjustment
- https://next.musicleague.com/support/league-schedule-and-pacing
- https://next.musicleague.com/support/song-comments-and-visibility
- https://next.musicleague.com/support/league-privacy
- https://next.musicleague.com/support/league-lifecycle
- https://next.musicleague.com/support/inviting-players
- https://next.musicleague.com/support/choosing-round-themes
- https://next.musicleague.com/support/league-notifications
- https://next.musicleague.com/support/follow-and-friend
- https://next.musicleague.com/support/the-charts
- https://next.musicleague.com/support/connecting-spotify
- https://next.musicleague.com/support/signing-in-to-music-league
- https://next.musicleague.com/support/league-playlist
- https://next.musicleague.com/support/moving-to-the-new-music-league
- https://next.musicleague.com/support/whats-included-in-premium
- https://next.musicleague.com/support/exporting-league-data
- https://next.musicleague.com/support/admin-moderation-tools
- https://next.musicleague.com/support/community-guidelines (2026-11-03)
- https://next.musicleague.com/support/installing-music-league-on-your-computer
- https://next.musicleague.com/ios-beta
- https://next.musicleague.com/discover
- https://next.musicleague.com/demo
- https://next.musicleague.com/terms (updated 2026-11-09)
- https://next.musicleague.com/privacy (updated 2026-11-09)
- https://next.musicleague.com/privacy-choices

**Music League, legacy and stores**
- https://musicleague.com/user-guide/
- https://musicleague.com/terms/ (updated 2025-01-21)
- https://apps.apple.com/us/app/music-league/id1589815321 (and the country storefronts us, gb, ie, ca, au, nz, sg, dk, no, pl, za, in)
- https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US (updated 2026-06-22)

**Interviews and secondary (traction and statements)**
- https://iowapodcast.com/music-league-eric-west/ (2026-09-08)
- https://www.musicradar.com/music-industry/we-speak-to-the-maker-of-a-game-putting-the-humanity-back-into-music-discovery (2025-05-22)
- https://blog.nitropay.com/publisher-showcase-music-league/

**Spotify**
- https://developer.spotify.com/policy (effective 2025-05-15)
- https://developer.spotify.com/compliance-tips
- https://developer.spotify.com/documentation/web-api/concepts/quota-modes
- https://community.spotify.com/t5/Spotify-for-Developers/Extended-Quota-Mode-Request-Independent-Developer-TrackLine/td-p/7384615
- https://community.spotify.com/t5/Spotify-for-Developers/What-is-the-reason-for-not-allowing-games-and-quizzes/m-p/6219736/highlight/true (user discussion; no Spotify answer found)

**Not reachable**
- https://appshunter.io/ios/app/1589815321 (403); legacy Zendesk help center (403); Reddit (blocked by the environment).
