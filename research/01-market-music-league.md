# Music League and its market: mechanics, competitors, complaints and platform constraints

Access date for all sources: 2026-11-22.

> **Method note.** No page could be opened directly from this environment: both WebFetch and `curl` returned "CONNECT tunnel failed, 403", and reddit.com is blocked for the search tool. Everything below comes from WebSearch results, which return snippets and summaries of each page, not the full page. The URLs cited are the ones in those results. Anything that needed the full page text is marked **not verified**. Open the source by hand before making a decision that depends on an exact figure.

## Key points

- **Music League is the leader and has just changed a lot.** It was founded in Iowa by Nathan Coleman, Matt Keller and Eric West (CEO). The company claims over 1.1 million registered users and about 200,000 monthly active players ([Iowa Tech Podcast](https://iowapodcast.com/music-league-eric-west/)). It has just rebuilt the product from scratch ([next.musicleague.com](https://next.musicleague.com/news/why-we-rebuilt-music-league)), adding Apple Music, its own accounts and fewer ads.
- **It makes money from ads plus an ad-free subscription.** The US App Store lists $2.99/month or $14.99/year ([App Store](https://apps.apple.com/us/app/music-league/id1589815321)). All gameplay and admin tools stay free.
- **The number-one complaint is ads.** Users say there are too many and they break the app: ads that can't be closed and that force a restart. The next complaints are Spotify lock-in (partly fixed in the new version) and crashes ([mwm.ai](https://mwm.ai/apps/music-league/1589815321), [Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)).
- **At least five direct clones exist, all supporting several music services:** BandJam, DJ League, YapZap, Cut Club and Aux Battles. They offer what Music League lacked or only half-offers: several music services, league chat, guess-who-submitted and live play. None shows public traction comparable to Music League.
- **Spotify is the biggest constraint.** Its Developer Policy literally says "Do not create a game, including trivia quizzes" ([Spotify Developer Policy](https://developer.spotify.com/policy)). Since February 2026, Development Mode allows at most 5 users per app and requires the owner to have Premium. Extended quota mode is granted only to organizations with at least 250,000 monthly active users ([Spotify blog, 2026-02-06](https://developer.spotify.com/blog/2026-02-06-update-on-developer-access-and-platform-security), [Spotify blog, 2025-04-15](https://developer.spotify.com/blog/2025-04-15-updating-the-criteria-for-web-api-extended-access)). A new competitor cannot rely on the Spotify API to reach scale.
- **Apple Music and YouTube are viable, with conditions.** Apple forbids monetizing access to Apple Music, even indirectly; Guideline 4.5.2 names advertising explicitly ([App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)). Since June 2026, the YouTube Data API allows only 100 searches per day per project by default ([YouTube Data API](https://developers.google.com/youtube/data/determine_quota_cost)).
- **Main gap (inference):** a product without intrusive ads, independent of the music service, with a stronger social layer (chat, reminders, league stats or a "Wrapped"-style recap). Third-party tools, some of them paid, already sell those stats ([musicleaguestats.com](https://musicleaguestats.com/)). The business model has to fit Apple's and Spotify's rules, and that is as hard as building the product.

---

## 1. Music League

### Who makes it and history

- **Founders:** Nathan Coleman, Matt Keller and Eric West. Coleman and Keller came up with the idea while working at Workiva (Ames, Iowa). They first played with USB drives and mp3 files, and Coleman then built a web app to run the game. West, Keller's high-school classmate, turned it into a business after the pandemic and is now co-founder and CEO ([Greater Des Moines Partnership](https://www.dsmpartnership.com/news-media/blog/discovering-new-musical-artists-while-making-connections-has-never-been-easier-), [DSM Partnership, Eric West profile](https://www.dsmpartnership.com/news-media/blog/music-league-connects-friends--helps-them-discover-new-music)). MIT Technology Review quotes a co-founder named "Alex Keller" ([MIT Tech Review, 2024-08-16](https://www.technologyreview.com/2024/08/16/1096276/spotify-algorithms-music-discovery-ux/)). The sources disagree on that first name (**not verified**).
- **Timeline:** the game started in 2016 and soon had a simple web version. The official launch came in 2022 with the mobile apps, followed shortly by an upgraded web app ([DSM Partnership](https://www.dsmpartnership.com/news-media/blog/discovering-new-musical-artists-while-making-connections-has-never-been-easier-)). LinkedIn gives 2015 as the founding year and lists headquarters as "Des Moines & New York City" ([LinkedIn](https://www.linkedin.com/company/musicleague)). Coleman told the origin story on Medium ([Medium, Nathan Coleman](https://medium.com/@nathancoleman/music-league-part-1-192de80d1db6)).
- **Company:** Music League LLC, the seller listed on the App Store ([App Store](https://apps.apple.com/app/id1589815321)).

### Size and traction (only what sources state)

| Approx. date | Figure | Source |
|---|---|---|
| Aug 2024 | ~130,000 monthly users, double the year before | [MIT Tech Review](https://www.technologyreview.com/2024/08/16/1096276/spotify-algorithms-music-discovery-ux/) |
| May 2025 | "thousands of daily players" | [MusicRadar, 2025-05-22](https://www.musicradar.com/music-industry/we-speak-to-the-maker-of-a-game-putting-the-humanity-back-into-music-discovery) |
| ~Jun 2026 | nearly 200,000 monthly active users (MAU) in 160 countries | [Music Tectonics](https://www.musictectonics.com/post/can-gamification-fix-music-discovery) |
| ~Sep 2026 | over 1.1 million registered users and ~200,000 monthly active players in 170 countries, with strong adoption in the US, Canada, UK, Australia and Brazil | [Iowa Tech Podcast](https://iowapodcast.com/music-league-eric-west/) |
| ~Sep 2026 | over 1 million registered users; "essentially nothing on user acquisition" | [Nitro blog](https://blog.nitropay.com/publisher-showcase-music-league/) |

The 2026 dates are inferred from the relative age the search tool showed. Google Play shows 4.3 stars from about 2.96K reviews on the Canadian listing ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)). Fathom.tools estimates about $50K in ad revenue ([fathom.tools](https://www.fathom.tools/network/nitropay)), but it is an outside estimate with no stated period (**not verified**).

### Mechanics (new version, official help center)

- **League → rounds → theme.** An administrator (admin) creates the league and sets the number of rounds, songs per round, voting points, themes and deadlines. Once the league starts, the admin has no advantage over other players ([How to Play](https://next.musicleague.com/support/how-to-play)).
- **Submission:** each player submits one or more songs that fit the theme. The admin sets how many songs players may and must submit. Submitting can be optional, and repeat artists or songs can be allowed or blocked, per league or per round ([Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)).
- **Listening:** an anonymous, shuffled playlist is built for the round. It is not created automatically: the first player to tap "Generate" on the round page creates it. The new version can also build one playlist for the whole league. Round playlists used to come from a single shared Music League account ([How to Play](https://next.musicleague.com/support/how-to-play), [Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)).
- **Anonymous voting:** each player hands out upvotes. The admin sets how many they may and must hand out and a cap per song. Nobody can vote for their own song. Downvotes are optional and off by default: the admin picks 1 to 100 per player per round, how many are mandatory, and a cap per song ([League Rules and Scoring](https://next.musicleague.com/support/league-rules-and-scoring), [Voting Rules](https://next.musicleague.com/support/voting-rules-and-auto-adjustment)). One player reports setting "50 upvotes and 50 downvotes" as the maximum allowed ([Tony Coles, Substack](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)).
- **Scoring:** a song scores its upvotes minus its downvotes, floored at zero. Standings add up points round by round and show a percentage: cumulative net score divided by the sum of each round's maximum possible score ([League Rules and Scoring](https://next.musicleague.com/support/league-rules-and-scoring)). With upvotes set to 0, the league becomes "discovery and conversation" only, with no points and no winner ([League Rules and Scoring](https://next.musicleague.com/support/league-rules-and-scoring)). Tie-breaking is **not verified**.
- **Competitive Mode** (optional): a player who doesn't hand out all their mandatory votes loses the upvotes they received that round. It replaces the old "low stakes" setting. Voting rules, Competitive Mode, league-wide duplicate-artist rules and private visibility lock when the league launches. If a round has too few songs, the system raises the per-song vote cap on its own ([League Rules and Scoring](https://next.musicleague.com/support/league-rules-and-scoring)).
- **Pacing:** Steady (fixed deadlines), Accelerated (a phase ends when everyone is done) and Speedy (like Accelerated, but the next phase starts immediately) ([League Schedule](https://next.musicleague.com/support/league-schedule-and-pacing)).
- **Comments:** players comment on each song while voting. The admin decides when comments become visible, and once voting closes everyone sees who submitted what ([How to Play](https://next.musicleague.com/support/how-to-play), [App Store](https://apps.apple.com/us/app/music-league/id1589815321)). There is no evidence of player-to-player chat (**not verified**). The app has an AI-powered support chat, which is not social.
- **Limits:** 2 to 100 players. The real limit is the playlist, which cannot exceed 100 songs: players × songs per player ≤ 100. Private leagues have no round limit; public leagues allow 20. An old guide said 100 rounds ([Creating a League](https://next.musicleague.com/support/creating-a-league), [old user guide](https://musicleague.com/user-guide/)). The recommended setup is 4–6 rounds, 5–15 players and 1–2 songs per round.
- **Other rules:** a player who doesn't submit can't vote that round, and someone who joins mid-league can't vote until they have submitted. Public leagues appear on Home and in Discover, and anyone can join without approval. The new version has no public leagues yet, until enough people move over ([How to Play](https://next.musicleague.com/support/how-to-play), [Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)).
- **Export:** a league exports as a ZIP holding `competitors.csv`, `rounds.csv`, `submissions.csv` and `votes.csv`, without the league name ([musicleague-importer](https://github.com/billslovin-personal/musicleague-importer)).

### Platforms and integrations

- **Platforms:** web, iOS ([App Store](https://apps.apple.com/us/app/music-league/id1589815321)) and Android ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)). The store apps still point to the old version. The new one runs in the browser or as an installable web app, and has an iOS beta ([Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)).
- **Music:** the old version worked only with Spotify ([Vice](https://www.vice.com/en/article/music-league-spotify/)). The new one supports Spotify or Apple Music. Sign-in no longer requires Spotify: email and password, Spotify or Apple all work. Spotify or Apple Music is still needed to search for songs, play previews and build playlists. YouTube Music doesn't appear in any source (**not verified** that it is absent). Spotify Free works: if a song isn't available on the free tier, a 30-second preview is added ([How to Play](https://next.musicleague.com/support/how-to-play)).

### Business model

- Free with ads served by Nitro (NitroPay, part of Overwolf) ([Nitro blog](https://blog.nitropay.com/publisher-showcase-music-league/)).
- Premium ("Ad Free Leagues"): $2.99/month or $14.99/year in the US, and £2.99 or £14.99 in the UK ([App Store US](https://apps.apple.com/us/app/music-league/id1589815321), [App Store UK](https://apps.apple.com/gb/app/music-league/id1589815321)). AppsHunter shows in-app purchases up to $24.99, which suggests another tier (**not verified**) ([AppsHunter](https://appshunter.io/ios/app/1589815321)). In 2024 the quoted price was $2/month or $20/year ([Headphonesty](https://www.headphonesty.com/2024/04/tired-music-streaming-try-music-league/)).
- Rewarded ads exist: watching one buys a stretch without ads. An April 2026 review (v1.4.3) complains that this stretch dropped from 48 hours to 2 hours ([mwm.ai](https://mwm.ai/apps/music-league/1589815321)).

### Recent changes

- **Full rebuild (autumn 2026, exact date not verified):** its own accounts, Apple Music, a whole-league playlist, 13 languages, custom artwork, duplicate control, optional submission and voting, and a promise of "leaning on ads less over time" ([Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)). On the podcast, West says the rebuild was about stability and a better ad experience ([Iowa Tech Podcast](https://iowapodcast.com/music-league-eric-west/)).
- App release notes mention fewer crashes, redesigned ads and paywall, and 14 days ad-free after sign-up ([mwm.ai](https://mwm.ai/apps/music-league/1589815321)).

---

## 2. Competitors and adjacent products

### Comparison table

| Name | What it is | Platforms | Music integrations | Price | Status | Key difference from Music League | Source |
|---|---|---|---|---|---|---|---|
| **BandJam** (Grant's Software LLC) | Asynchronous league with themed rounds | iOS, Android, web | Spotify, Apple Music, YouTube (by pasting a link); no music service required | Free, "No ads"; no paid model stated | Alive; App Store listing from late 2025 or early 2026, 5.0 from 6 ratings | Guess who submitted each song (bonus points and a second leaderboard), chat with GIFs, "Crews", league templates | [bandjam.app](https://bandjam.app/), [handbook](https://bandjam.app/handbook/), [App Store](https://apps.apple.com/us/app/bandjam-music-competitions/id6756460555) |
| **DJ League** | Asynchronous league with themed rounds | Web, Android (iOS not verified) | Spotify, Apple Music, YouTube Music (automatic playlists) | Free (per its site) | Alive (no update date found) | Song bans, per-round bonus points, points for guessing who submitted | [djleague.app](https://djleague.app/), [Google Play](https://play.google.com/store/apps/details?id=app.djleague.app) |
| **YapZap** (John Pounders) | Music and video leagues | iOS, web (no Android listing found) | Spotify, Apple Music, YouTube Music, TIDAL, Amazon Music, Deezer, Qobuz | Not verified | Alive (receives updates) | Widest service catalog, chat, deadline push notifications, streaks, AI theme suggestions, video leagues | [App Store](https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650), [yapzap.com](https://yapzap.com/) |
| **Cut Club** (Beta Acid, Inc.) | 8–12 week seasons with a weekly theme; plus a ~2-minute "Daily Cut" | Web, mobile app | Playback via YouTube, no Spotify dependency | Free to join; clubs cost $9.99/season with unlimited players, or $1.50 per player per season | Alive | Charges per season instead of showing ads; Slack integration (aimed at work teams) | [playcutclub.com](https://www.playcutclub.com/), [its own comparison](https://www.playcutclub.com/blog/music-league-vs-cut-club-which-music-game-is-better-in-2026) |
| **Aux Battles** | Live game: a room joined by code, rounds of ~4 min | Browser | Spotify, YouTube, YouTube Music, SoundCloud (no Apple Music) | Free, no account, no paid tier | Alive | Synchronous, no sign-up, blind 0.5–5 star voting, 3,830 prompts, Twitch mode | [auxbattles.app](https://auxbattles.app/), [compare](https://auxbattles.app/compare) |
| **songbattle.io** | Real-time elimination brackets of up to 128 songs | Browser | Spotify, YouTube, Apple Music, SoundCloud, Suno | Free | Alive | Built for Twitch streams and Discord calls; viewers submit songs | [songbattle.io](https://songbattle.io/), [auxbattles compare](https://auxbattles.app/compare) |
| **Music Leek** (open-source Discord bot) | League inside Discord: /submit-song, /vote | Discord, self-hosted | Spotify playlists | Free | Public repo (activity not verified) | Lives where the group already is; 10 points per player spread over up to 5 songs; disqualification callout for non-voters | [GitHub](https://github.com/snsutton/music-leek) |
| **musicleague-bot** (open-source Discord bot) | League with emoji-reaction voting | Discord, self-hosted | Not stated | Free | Public repo (activity not verified) | Emoji votes, up to 3 per player | [GitHub](https://github.com/eeSquared/musicleague-bot) |
| **bodhello/musicleague, league-of-music** (open-source clones) | Self-hosted web clones | Web | Spotify API | Free | Public repos (activity not verified) | Ranked voting (top 3) in league-of-music; email reminders | [bodhello](https://github.com/bodhello/musicleague), [league-of-music](https://github.com/Master-Chief-117-codes/league-of-music) |
| **Playlist Game: Music Party** | Theme per round; guess who picked each song | Android | 30-second Deezer clips | Not verified | Alive (listing active) | In-person play, no points for quality | [Google Play](https://play.google.com/store/apps/details?id=com.mariussty.playlistgame&hl=en_US) |
| **playlist-party.com** | Collaborative playlist for a party | Web | Not verified | Not verified | Alive | No competition, no accounts | [playlist-party.com](https://playlist-party.com/) |
| **JQBX** | Synchronized listening rooms | Web/desktop | Spotify Premium | Not verified | Bought by Turntable LIVE in 2023; current status not verified | Social but not competitive | [Record of the Day](https://www.recordoftheday.com/news-and-press/turntable-live-acquires-jqbx-unites-two-music-centered-social-platforms) |
| **Turntable.fm / deepcut.fm** | Turn-based DJ rooms | Web | — | — | Relaunched in 2021; current status not verified | Live and social, no leagues | [rip.so](https://rip.so/turntable-fm.html), [TechCrunch 2023](https://techcrunch.com/2023/03/28/turntable-live-nee-tt-fm-raises-7m-ahead-of-public-launch) |
| **Spotify Blend / Jam** | Shared playlist for up to 10 people / live shared queue | Inside Spotify | Spotify only; starting a Jam needs Premium | Included | Alive; in 2026 added "Request to Jam" and listening activity in group messages | No game, no votes: competes for the user's social time | [Blend](https://newsroom.spotify.com/2021-08-31/how-spotifys-newest-personalized-experience-blend-creates-a-playlist-for-you-and-your-bestie/), [Jam](https://support.spotify.com/us/article/jam/), [Newsroom 2026-01-07](https://newsroom.spotify.com/2026-01-07/listening-activity-request-to-jam-messages-updates/) |
| **SongPop Party** | Song-guessing music trivia | Switch, Xbox, PC | Own catalog | $19.99 | Alive | Guessing, not curating | [Xbox Store](https://www.xbox.com/en-US/games/store/songpop-party/9P7ZQRHZW9GK) |
| **Songlio** | Name-that-tune with 20-second clips | Web | Encore | Free | Probably dead: in November 2026 it redirected to encoremusicians.com | Guessing, not curating | [Product Hunt](https://www.producthunt.com/products/songlio), [onlineparty.games](https://onlineparty.games/games/music-games/songlio) |
| **Hitster and clones** (Mixster, Hitify, Melody Fight…) | Place songs on a timeline by release year | Physical cards + app / web | Spotify (Mixster needs Premium); some need no service | Varies | Alive | In-person party game | [Mixster](https://github.com/adriansberg/mixster), [Melody Fight](https://melodyfight.com/hitster-alternative) |

### Tools built around Music League (a demand signal)

- **musicleaguestats.com:** upload the exported ZIP to get vote heatmaps, "taste twins", "nemesis" stats and a Spotify Wrapped-style recap. Core stats are free and Premium costs $0.99/month. It is not affiliated with Music League ([musicleaguestats.com](https://musicleaguestats.com/)).
- **musicleague-importer, music-league-stats, MusicLeagueStats:** spreadsheets and dashboards with lifetime stats across seasons ([importer](https://github.com/billslovin-personal/musicleague-importer), [TheRedSock](https://github.com/TheRedSock/music-league-stats), [mattu82](https://github.com/mattu82/MusicLeagueStats)).
- **music-league-voting-assistant:** turns your notes into a vote allocation ([GitHub](https://github.com/bbailey27/music-league-voting-assistant)).

### Leagues run by hand

Could not be checked. Reddit is blocked for this environment's search tool, so there is no data on r/musicleague or on leagues run in spreadsheets or forums. Forum communities that run leagues on Music League itself do show up: GuitarNutz ([ProBoards](https://guitarnuts2.proboards.com/thread/10254/music-league)), ILX ([ilxor](https://www.ilxor.com/ILX/ThreadSelectedControllerServlet?boardid=41&threadid=115341)) and Gamers With Jobs ([gamerswithjobs](https://www.gamerswithjobs.com/node/1303879)).

---

## 3. User complaints and wishes

Sources are store reviews, review aggregators, forums and personal essays. Reddit could not be read. mwm.ai summarizes 485 iOS reviews: the most-mentioned theme is "Aggressive ads" (52 mentions), followed by "Apple Music support" (15) and "App crashes" (12) ([mwm.ai](https://mwm.ai/apps/music-league/1589815321)).

**A. Intrusive ads that break the app (the most repeated theme)**
- "there are ads that you can't click out of, like there is no 'x'"; the user has to restart the app until an ad comes up that doesn't freeze it ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)).
- "why are you making my hit the X to close the same ad 3 times?" ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)).
- "Ads Ruin Everything… I usually have to force quit the app (sometimes more than once)"; the reviewer recommends the web version instead ([mwm.ai, iOS review v1.4.4](https://mwm.ai/apps/music-league/1589815321)).
- UK reviews: the close button "*always* takes you to the App Store" ([App Store UK](https://apps.apple.com/gb/app/music-league/id1589815321)).
- The developer's own reply: "We've never been happy with the ad experience either" ([mwm.ai](https://mwm.ai/apps/music-league/1589815321)).

**B. Spotify dependency**
- "some people… don't want to join because the game only allows Spotify"; the reviewer asks for Apple Music, Tidal or Bandcamp ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)).
- Vice lists as a drawback that "Music League only works with Spotify" ([Vice](https://www.vice.com/en/article/music-league-spotify/)). The new version partly fixes this by adding Apple Music, but not YouTube Music, Tidal or Deezer.

**C. Stability and bugs**
- Frequent crashes ([AppsHunter](https://appshunter.io/ios/app/1589815321)). A text-box bug: everything gets selected on its own and the next keystroke deletes it ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)).

**D. The app does less than the website**
- "as the admin… I could only adjust the deadlines forward and backward by accessing the website" ([Vice](https://www.vice.com/en/article/music-league-spotify/)). Another review says the app adds nothing to the website "except ads" ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)).

**E. Drop-outs and deadlines**
- One player left because he couldn't keep up with the schedule. When deadlines were changed mid-season, "deadlines were sprayed all over the place" ([Tony Coles](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)).
- Another player only ever made one of the two phases, submit or vote, never both; the admin moved to 72-hour rounds ([Gamers With Jobs](https://www.gamerswithjobs.com/node/1303879)).
- From the start the organizer had to chase late voters by Messenger or email and wanted reminders through each person's preferred channel ([Medium, Coleman](https://medium.com/@nathancoleman/music-league-part-1-192de80d1db6)). Which reminder channels exist today is **not verified**.

**F. Social dynamics: what hooks players also causes friction**
- "The real metagame of *Music League* is in the commenting and the forum side-discussion"; "only play *Music League* if your ego can handle it" ([Tony Coles](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)).
- Winning means playing to the room: "you are simultaneously a candidate and part of the electorate" ([Lamniformes](https://lamniformes.substack.com/p/11292024)). There are complaints about players reading themes too literally ([New Music for Olds](https://newmusicforolds.substack.com/p/down-with-literalism)).
- With few votes per player, almost everyone was frustrated at not being able to reward the songs they liked ([Tony Coles](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)).
- West: "connecting with other people was just as important" as discovery and competition ([Nitro blog](https://blog.nitropay.com/publisher-showcase-music-league/)).

**G. Stats and history**
- No explicit complaints found, but there is an ecosystem of third-party tools, one of them paid, that build stats and a "Wrapped" from the exports (section 2). People paying for one suggests an unmet need (inference).

---

## 4. Gaps and opportunities

| # | Gap or angle | Evidenced or inferred? | Basis |
|---|---|---|---|
| 1 | **An experience without intrusive ads** (or a paid model that doesn't punish free players) | Evidenced | Number-one theme in reviews ([mwm.ai](https://mwm.ai/apps/music-league/1589815321)); the developer admits it. Caveat: Music League promises fewer ads, so this gap may narrow. |
| 2 | **Independence from the music service** (YouTube Music, Tidal, Deezer, on top of Spotify and Apple) | Evidenced as demand; inferred as a gap | Reviews asking for Apple Music, Tidal and Bandcamp ([Google Play](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA)). Music League now covers Apple Music, and YapZap and BandJam cover more. This alone no longer differentiates. |
| 3 | **Deadlines and reminders that reduce drop-outs** (alerts through each player's channel, catching up late players, a "vacation mode") | Evidenced (the pain); the fix is inferred | [Tony Coles](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review), [Gamers With Jobs](https://www.gamerswithjobs.com/node/1303879), [Medium](https://medium.com/@nathancoleman/music-league-part-1-192de80d1db6) |
| 4 | **A built-in social layer** (league chat, reactions, conversation during the round) | Inferred | Comments are the "metagame" ([Tony Coles](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)); people move the talk to Discord. YapZap and BandJam already offer it. |
| 5 | **Native league and season stats and "Wrapped"** | Inferred from demand | Paid third-party tools ([musicleaguestats.com](https://musicleaguestats.com/)) |
| 6 | **Alternative voting mechanics** (ranking, guess the submitter, bans, stars) to soften "playing it safe" | Inferred | BandJam and DJ League already score guess-the-submitter; league-of-music uses ranking; Aux Battles uses stars |
| 7 | **Integration where the group already is** (Discord, WhatsApp, Slack) | Inferred | Discord bots exist ([music-leek](https://github.com/snsutton/music-leek)); Cut Club integrates with Slack. Spotify Jam already lives inside Spotify's messages ([Newsroom](https://newsroom.spotify.com/2026-01-07/listening-activity-request-to-jam-messages-updates/)). |
| 8 | **Corporate or team use** (team building) | Inferred | Cut Club targets Slack and charges per season |
| 9 | **Hybrid format: asynchronous league plus a "live night"** (live voting during a call) | Inferred | Week-long leagues and 4-minute games (Aux Battles, songbattle.io) coexist; no product on record combines both |
| 10 | **Non-English markets / localization** | Inferred, and weak | Music League already has 13 languages ([Why We Rebuilt](https://next.musicleague.com/news/why-we-rebuilt-music-league)); Brazil is among its strong markets |

**Structural brake (inferred from section 5):** Music League's ad model clashes with Apple's Guideline 4.5.2 if the ads surround access to Apple Music. Spotify, for its part, forbids games. Any competitor has to work out first how it fits those rules, and product design comes after.

---

## 5. Platform constraints

### Spotify Web API

- **Games are forbidden.** Developer Policy, section III: "Do not create a game, including trivia quizzes" ([Spotify Developer Policy](https://developer.spotify.com/policy)). The Compliance Tips give a "name that tune" quiz as a forbidden example ([Compliance Tips](https://developer.spotify.com/compliance-tips)). The policy doesn't mention "contests" by name. How Music League fits this rule is **not verified**: no source explains it.
- **Other relevant prohibitions:** combining streams or content with another service; analyzing Spotify content to build metrics or user profiles; using the content to train AI; and replicating a "core Spotify experience" without permission ([Spotify Developer Policy](https://developer.spotify.com/policy)). The first hits a multi-service app head-on and the second hits "taste stats" (inference). Full-track streaming is only for Premium users, and commercial use is tightly limited ([Spotify Developer Policy](https://developer.spotify.com/policy)).
- **2024-11-27:** new apps lost recommendations, audio-features, audio-analysis, related-artists, featured and category playlists, and the `preview_url` field (the 30-second previews). Calling them returns 403 ([DEV Community summary](https://dev.to/birrings/spotifys-audiofeatures-api-died-in-2024-heres-what-i-built-to-replace-it-3dn3); the official post "Introducing some changes to our Web API" could not be opened). This means a new app can't give Spotify previews to Spotify Free users the way Music League does (inference).
- **2025-04-15, extended access (extended quota):** since 2025-05-15 it is granted only to registered organizations with a launched service, at least 250,000 MAU, presence in key Spotify markets and commercial viability. Apps that already had it keep it ([Spotify blog](https://developer.spotify.com/blog/2025-04-15-updating-the-criteria-for-web-api-extended-access), [Quota modes](https://developer.spotify.com/documentation/web-api/concepts/quota-modes)). Review can take up to six weeks ([Spotify forum](https://community.spotify.com/t5/Spotify-for-Developers/Clarification-on-Extended-Quota-Mode-Eligibility/td-p/7503072)).
- **2026-02-06, Development Mode:** now only for personal, non-commercial use. The app owner needs Premium and each Client ID allows at most 5 authorized users. It applies from 2026-02-11 for new apps and from 2026-03-09 for existing ones, though the endpoint cuts were postponed for existing apps ([Spotify blog](https://developer.spotify.com/blog/2026-02-06-update-on-developer-access-and-platform-security), [TechCrunch](https://techcrunch.com/2026/02/06/spotify-changes-developer-mode-api-to-require-premium-accounts-limits-test-users/)). Specific changes ([migration guide](https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide), [Feb 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/february-2026)):
  - search returns at most 10 results (previously 50);
  - batch lookups, artist top tracks, new releases and `/users/{id}/playlists` are gone;
  - playlists move from `/tracks` to `/items`, and their contents are returned only if the user owns or collaborates on the playlist;
  - the popularity and `available_markets` fields are removed;
  - in March 2026 `external_ids` was restored ([Mar 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/march-2026)), a field useful for matching songs across services by ISRC (inference).
- **2026-06-18:** refresh tokens now expire 6 months after authorization. Existing apps are affected from 2026-07-20, and users have to sign in again ([Spotify blog](https://developer.spotify.com/blog/2026-06-18-refresh-token-expiration)). In a long league, that means prompting players to reconnect Spotify (inference).
- **2026-07-23:** up to 25 Client IDs per developer account, with a shared quota, and 429 responses carrying `"reason": "QUOTA_EXCEEDED"` ([Spotify blog](https://developer.spotify.com/blog/2026-07-23-web-api-quota-updates)).
- **Conclusion (inference):** a new competitor starts with 5 users in Development Mode and can't apply for extended access until it has 250,000 MAU and is a company. Using Spotify as a launch pillar is not workable. The alternatives are to treat Spotify as an outbound link only (paste a URL or ISRC and open the song in Spotify) or to launch on Apple Music or YouTube. Whether linking without the API falls under the Developer Policy should be checked with a lawyer.

### Apple MusicKit / Apple Music API

- **Capabilities:** with the user's permission, an app can create playlists in their library (`POST /v1/me/library/playlists`) and add songs to them. The API works on Apple platforms, Android and the web ([MusicKit](https://developer.apple.com/musickit/), [LibraryPlaylistCreationRequest](https://developer.apple.com/documentation/applemusicapi/libraryplaylistcreationrequest)).
- **Tokens:** a developer token is required (ES256 JWT, valid up to 6 months), plus, for the user's library, a Music User Token, which requires an active Apple Music subscription ([Apple Music API documentation](https://developer.apple.com/tutorials/data/documentation/applemusicapi.md)). According to a forum post, the Music User Token expires after about 6 months and can't be renewed without the user signing in again (**not verified** in official docs). That a paid Apple Developer Program membership ($99/year) is required follows from the keys being created in the developer account, but it was **not verified**.
- **App Store Guideline 4.5.2:** the app "may not require payment or indirectly monetize access to the Apple Music service (such as in-app purchase, advertising, requesting user info, etc.)". Guideline 4.10 forbids monetizing Apple services such as Apple Music access. Apple Music data also can't be shared with third parties except to support or improve the app ([App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)). Some versions of the text require user-initiated playback with standard controls ([guidelines history](http://www.appstorereviewguidelineshistory.com/articles/2017-06-08-new-rules-following-wwdc-2017/)); whether that is still in force is **not verified**. Guideline 5.2.5 bars using previews "for their entertainment value (e.g. as the soundtrack to a game)", according to a quote on the forum ([Apple Music API forum](https://developer.apple.com/forums/tags/apple-music-api/?sortBy=newest)).
- **Implication (inference):** an app with ads or an "ad-free" premium has to clearly separate what it charges for (its own game features) from access to Apple Music. Some developers on the forum justify their apps that way ([forum](https://developer.apple.com/forums/tags/apple-music-api/?sortBy=newest)). Using previews as a game mechanic is a risk area.

### YouTube Data API

- **Quota (since 2026-06-01):** by default, 100 `search.list` calls per day in their own quota bucket, plus 10,000 units per day for everything else. `playlists.insert` and `playlistItems.insert` cost 50 units each, which caps you at about 200 inserts per day ([Quota Calculator](https://developers.google.com/youtube/data/determine_quota_cost), [Revision History](https://developers.google.com/youtube/v3/revision_history?hl=en), [playlistItems.insert](https://developers.google.com/youtube/v3/docs/playlistItems/insert)). With 100 searches a day, song search through YouTube can't support even a small community (inference). Search would have to run on another catalog, with YouTube used only for playback.
- **More quota requires a compliance audit** (API Compliance Audit), and the extra quota is valid only for the approved use case ([Developer Policies](https://developers.google.com/youtube/terms/developer-policies)).
- **Forbidden:** separating audio from video, promoting them separately, background playback, and downloading or caching content ([Developer Policies](https://developers.google.com/youtube/terms/developer-policies), [Compliance guide](https://developers.google.com/youtube/terms/developer-policies-guide)). So YouTube playback has to be the visible, embedded video player, not an "audio-only mode" (inference).

---

## Open questions

1. How Music League fits Spotify's "Do not create a game" rule: whether it has an agreement, relies on inherited extended access, or Spotify doesn't consider it a game. No source.
2. The exact relaunch date of the new version, and whether Premium changes in price or scope there.
3. Whether a paid tier above $14.99 exists (AppsHunter shows up to $24.99).
4. How ties are broken, and which reminder channels (email, push) Music League uses.
5. Whether Music League has player-to-player chat beyond comments.
6. Real traction of the competitors (BandJam, DJ League, YapZap, Cut Club): no source gives figures.
7. Sentiment on Reddit (r/musicleague): not accessible.
8. Pricing of YapZap and DJ League, and whether DJ League has an iOS app.
9. Whether an app that only links to Spotify, without using the API, falls under the Developer Policy. This is a legal question.
10. Current status of JQBX and Turntable.fm/deepcut.fm.
11. Whether the user-initiated playback rule and Guideline 5.2.5 are still in the current text of Apple's guidelines.

## Sources

**Music League (own sites and stores)**
- https://next.musicleague.com/news/why-we-rebuilt-music-league
- https://next.musicleague.com/support/how-to-play
- https://next.musicleague.com/support/league-rules-and-scoring
- https://next.musicleague.com/support/voting-rules-and-auto-adjustment
- https://next.musicleague.com/support/creating-a-league
- https://next.musicleague.com/support/league-schedule-and-pacing
- https://musicleague.com/user-guide/
- https://apps.apple.com/us/app/music-league/id1589815321
- https://apps.apple.com/gb/app/music-league/id1589815321
- https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_CA
- https://www.linkedin.com/company/musicleague

**Press, interviews and analysis**
- https://iowapodcast.com/music-league-eric-west/
- https://blog.nitropay.com/publisher-showcase-music-league/
- https://www.musicradar.com/music-industry/we-speak-to-the-maker-of-a-game-putting-the-humanity-back-into-music-discovery
- https://www.musictectonics.com/post/can-gamification-fix-music-discovery
- https://www.technologyreview.com/2024/08/16/1096276/spotify-algorithms-music-discovery-ux/
- https://www.dsmpartnership.com/news-media/blog/discovering-new-musical-artists-while-making-connections-has-never-been-easier-
- https://www.dsmpartnership.com/news-media/blog/music-league-connects-friends--helps-them-discover-new-music
- https://medium.com/@nathancoleman/music-league-part-1-192de80d1db6
- https://www.vice.com/en/article/music-league-spotify/
- https://www.headphonesty.com/2024/04/tired-music-streaming-try-music-league/
- https://www.abc.net.au/listen/doublej/music-reads/features/music-league-footy-tipping-music-nerds/13927100
- https://www.fathom.tools/network/nitropay

**User sentiment**
- https://mwm.ai/apps/music-league/1589815321
- https://appshunter.io/ios/app/1589815321
- https://affectionatediscourse.substack.com/p/music-league-the-definitive-review
- https://lamniformes.substack.com/p/11292024
- https://newmusicforolds.substack.com/p/down-with-literalism
- https://www.gamerswithjobs.com/node/1303879
- https://guitarnuts2.proboards.com/thread/10254/music-league
- https://www.ilxor.com/ILX/ThreadSelectedControllerServlet?boardid=41&threadid=115341

**Competitors and tools**
- https://bandjam.app/ · https://bandjam.app/handbook/ · https://apps.apple.com/us/app/bandjam-music-competitions/id6756460555
- https://djleague.app/ · https://play.google.com/store/apps/details?id=app.djleague.app
- https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650 · https://yapzap.com/
- https://www.playcutclub.com/ · https://www.playcutclub.com/blog/music-league-vs-cut-club-which-music-game-is-better-in-2026 · https://www.playcutclub.com/blog/5-best-music-league-alternatives-in-2026
- https://auxbattles.app/ · https://auxbattles.app/compare
- https://songbattle.io/
- https://github.com/snsutton/music-leek · https://github.com/eeSquared/musicleague-bot · https://github.com/bodhello/musicleague · https://github.com/Master-Chief-117-codes/league-of-music
- https://musicleaguestats.com/ · https://github.com/billslovin-personal/musicleague-importer · https://github.com/TheRedSock/music-league-stats · https://github.com/mattu82/MusicLeagueStats · https://github.com/bbailey27/music-league-voting-assistant
- https://play.google.com/store/apps/details?id=com.mariussty.playlistgame&hl=en_US · https://playlist-party.com/
- https://www.recordoftheday.com/news-and-press/turntable-live-acquires-jqbx-unites-two-music-centered-social-platforms · https://rip.so/turntable-fm.html · https://techcrunch.com/2023/03/28/turntable-live-nee-tt-fm-raises-7m-ahead-of-public-launch
- https://newsroom.spotify.com/2021-08-31/how-spotifys-newest-personalized-experience-blend-creates-a-playlist-for-you-and-your-bestie/ · https://support.spotify.com/us/article/jam/ · https://newsroom.spotify.com/2026-01-07/listening-activity-request-to-jam-messages-updates/
- https://www.xbox.com/en-US/games/store/songpop-party/9P7ZQRHZW9GK · https://www.producthunt.com/products/songlio · https://onlineparty.games/games/music-games/songlio
- https://github.com/adriansberg/mixster · https://melodyfight.com/hitster-alternative

**Platforms (official documentation)**
- https://developer.spotify.com/policy
- https://developer.spotify.com/compliance-tips
- https://developer.spotify.com/terms
- https://developer.spotify.com/documentation/web-api/concepts/quota-modes
- https://developer.spotify.com/blog/2025-04-15-updating-the-criteria-for-web-api-extended-access
- https://developer.spotify.com/blog/2026-02-06-update-on-developer-access-and-platform-security
- https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide
- https://developer.spotify.com/documentation/web-api/references/changes/february-2026
- https://developer.spotify.com/documentation/web-api/references/changes/march-2026
- https://developer.spotify.com/blog/2026-06-18-refresh-token-expiration
- https://developer.spotify.com/blog/2026-07-23-web-api-quota-updates
- https://techcrunch.com/2026/02/06/spotify-changes-developer-mode-api-to-require-premium-accounts-limits-test-users/
- https://dev.to/birrings/spotifys-audiofeatures-api-died-in-2024-heres-what-i-built-to-replace-it-3dn3
- https://community.spotify.com/t5/Spotify-for-Developers/Clarification-on-Extended-Quota-Mode-Eligibility/td-p/7503072
- https://developer.apple.com/musickit/
- https://developer.apple.com/documentation/applemusicapi/libraryplaylistcreationrequest
- https://developer.apple.com/tutorials/data/documentation/applemusicapi.md
- https://developer.apple.com/app-store/review/guidelines/
- https://developer.apple.com/forums/tags/apple-music-api/?sortBy=newest
- http://www.appstorereviewguidelineshistory.com/articles/2017-06-08-new-rules-following-wwdc-2017/
- https://developers.google.com/youtube/data/determine_quota_cost
- https://developers.google.com/youtube/v3/revision_history?hl=en
- https://developers.google.com/youtube/v3/docs/playlistItems/insert
- https://developers.google.com/youtube/terms/developer-policies
- https://developers.google.com/youtube/terms/developer-policies-guide
