# Daily music games and automated recaps, as they exist today

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [Daily music games and automated recaps](../21-daily-games-and-recaps.md)

Method note: I opened primary pages where the network allowed (the games' own sites, store listings, Apple's lookup API, vendor docs). Several sites (heardledecades.com, songless.pro, musicianle.com, alldle.net, nytco.com, Spotify's Variety coverage) were blocked or paywalled from this environment; where a claim rests on a search-result summary of such a page I say so. Anything not opened myself is marked "not verified". "(inference)" is my reading, not a source statement. This ticket states the market; it does not decide anything. Findings from earlier studies are reused, not redone: Spotify bans games in its policy and embed terms ([spotify-access.md](spotify-access.md)), Apple guideline 5.2.5 bans previews as a game soundtrack ([apple-music-access.md](apple-music-access.md)), Deezer terms say "No games or businesses based on sound recordings" and SoundCloud terms bar game use without licences ([other-services.md](other-services.md)), YouTube embed rules ([youtube-access.md](youtube-access.md)).

## Answer

- **No daily music game I found plays commercial audio under a documented, public licence, except by paying for it or by recreating the music.** Bandle rebuilds each song from instrument layers it makes itself and says licensing is "complicated and expensive", with "a large share" of ad revenue going to it ([Berklee interview, July 2025](https://online.berklee.edu/takenote/bandle-creator-johann-levy-on-the-music-quiz-100k-daily-players-love/)). The others route audio through third parties (SoundCloud, Apple store previews) or state nothing. Songless's own site claims "real, licensed songs" but gives no licensor and says this "may vary in unofficial versions" ([songless.org](https://songless.org)).
- **The audio routes actually in use are four, and each collides with a term already studied.** SoundCloud embeds (Heardle, Heardle Decades, Sampledle); Apple store preview URLs (lessgames Songless page data, Musicle via "the Apple Music API", Crosstune per one review); self-hosted copies of clips (lessgames serves `.aac` files from its own CDN); and recreated audio (Bandle). I found no daily game that documents using YouTube embeds with `start` and `end` parameters, although the parameters exist ([YouTube player parameters](https://developers.google.com/youtube/player_parameters)).
- **Several formats work with no audio at all.** Spotle (guess an artist from attribute tiles, 1,000 artists, artwork from Apple's image CDN), Harmonies (Connections-style grouping of music-related text), Lyricle (lyrics), Relatle and Framed's film analogue (images). Spotle is the second most widely played music daily on one aggregator's ranking ([Dailydles](https://dailydles.com/categories/music)), so audio is not required for traction. Whether lyrics themselves need a licence was not researched.
- **Heardle died because its owner closed it, not because of a takedown.** Spotify bought it in July 2022 and shut it on 5 May 2023, saying only that it would "focus our efforts on other features for music discovery". Visits had fallen from 10 million (January 2023) to 6 million (March 2023), after 69 million in March 2022 ([TechCrunch 2022](https://techcrunch.com/2022/07/12/spotify-acquired-heardle-wordle-music-game), [Music Business Worldwide](https://www.musicbusinessworldwide.com/spotify-to-shutter-music-trivia-game-heardle-less-than-a-year-after-acquiring-it/)). No source documents a takedown or a label complaint against Heardle or a clone. One site claims most clones went dead because they stream recordings they cannot license; it cites no specific case (not verified).
- **Money in this niche is small and comes from ads, one-off packs and subscriptions.** Bandle: song packs are "the biggest earners", then ads; Google Play shows in-app items from EUR 0.99 to EUR 29.99 and 1M+ downloads. Lessgames: "ad revenue and subscriptions". Songless.org: Mediavine ads. Musicle: ads or a one-time "lifetime ad-free" fee. Framed: merch. Spotify gave Heardle away free. The price of the Musicle fee was not visible in static HTML.
- **Growth in this niche is share-your-result plus creators.** Wordle's emoji grid is the model (spoiler-free grid, pasted as text). Bandle credits streamers (Northern Lion, theneedledrop, Tom Scott quoted in the store text) and Reddit rather than an in-game share feature ([NBC News, 2024-04-23](https://www.nbcnews.com/tech/tech-news/bandle-song-guessing-game-builds-buzz-online-rcna149012), [Apple listing](https://apps.apple.com/us/app/bandle-guess-the-song-games/id6471419531)).
- **Automated recaps are dominated by platform-owned data; a third-party league recap already exists.** Spotify Wrapped 2025 reached 250 million engaged users in 65 hours with 575 million shares, per reports of Spotify's figures (Variety page not opened). "Music League Wrapped" is offered by an unaffiliated stats site (post dated 2026-10-01). Cut Club advertises season recaps and BandJam 23 charts of analytics. A per-league recap built on a game's own data needs no music-service API (inference).
- **A web app can share for free in four ways, and none posts to Instagram or TikTok by itself.** Web Share API with files (opens the OS share sheet; Firefox desktop only behind a preference), Open Graph tags for link previews, copy-to-clipboard text grids, and PNG download. Instagram's Stories URL scheme and TikTok's Share Kit are native iOS and Android only; TikTok's web Share Video API is deprecated, and its replacement posts privately until the app passes an audit.
- **Existing league apps already bolt on a daily mode.** Cut Club's Daily Cut, YapZap's Daily rooms and TuneBoxed's Song of the Day ([competitors.md](competitors.md)). None of the three is a Heardle-type audio-guess game as far as the studied descriptions show.

## Daily music games

"Live" means the game's site or store listing answered on 2026-11-22. "Traction" figures are from the cited source and date. Aggregator rankings (Dailydles) do not state their method.

| Name | Mechanic | Audio source | Live / dead | Traction | Money | Link |
|---|---|---|---|---|---|---|
| **Heardle** (original, Omakase Studios) | One song a day; clip grows with each miss, 1 s up to 16 s; 6 tries | SoundCloud (songs chosen "semi-randomly" at release) | Dead: closed 5 May 2023 | 69M monthly web visits (Mar 2022); 41M (Jun 2022); 10M (Jan 2023); 7.3M (Feb); 6M (Mar), Similarweb via press | Ko-fi donations before sale; free under Spotify | [Wikipedia](https://en.wikipedia.org/wiki/Heardle), [TechCrunch](https://techcrunch.com/2022/07/12/spotify-acquired-heardle-wordle-music-game), [MBW](https://www.musicbusinessworldwide.com/spotify-to-shutter-music-trivia-game-heardle-less-than-a-year-after-acquiring-it/) |
| **Heardle Decades** and artist editions | Heardle clone with decade, genre or artist song sets | SoundCloud ("a good selection of songs available on Soundcloud"), per a search summary of its FAQ; page not opened | Listed live by an aggregator (rank 8); site not opened | Not verified | Not verified | [FAQ](https://heardledecades.com/faq/) (not opened), [Dailydles](https://dailydles.com/categories/music) |
| **Bandle** (Johann Levy, SAS BANDLE, Paris) | One song a day, heard one instrument at a time (drums first, vocals last); 6 guesses; extra modes and packs | Recreated by the creator and a volunteer in Logic Pro (MIDI, "one to three hours" a song); licensing paid | Live: iOS update 2026-11-21 | "100,000 fans each day" (Berklee, July 2025); Google Play 1M+ downloads, 3,242 ratings; iOS 1,559 ratings (lookup 2026-11-22); launched Aug 2022, app Dec 2023 | Song packs ("biggest earners"), ads, one-off bundle; Play in-app items EUR 0.99 to EUR 29.99; Levy says he stays independent | [Berklee](https://online.berklee.edu/takenote/bandle-creator-johann-levy-on-the-music-quiz-100k-daily-players-love/), [NBC](https://www.nbcnews.com/tech/tech-news/bandle-song-guessing-game-builds-buzz-online-rcna149012), [Play](https://play.google.com/store/apps/details?id=com.bandlegame.bandleguessasong&hl=en_US), [iOS](https://apps.apple.com/us/app/bandle-guess-the-song-games/id6471419531) |
| **Songless** (several unrelated sites share the name) | Intro snippet grows with each skip or miss; 6 tries (songless.org says up to 16 s; lessgames says 0.1 s start) | lessgames.com: page data lists, per track, a `fileUrl` on `cdn.lessgames.com` (self-hosted `.aac`), an `itunesPreviewUrl` (Apple) and an `scTrackUrn` (SoundCloud) (observed). songless.org: claims "real, licensed songs" with no licensor named | Live (several sites) | No creator figures. iOS "Songless" by Quynh Dau: 12 ratings (lookup); Play 50K+ downloads per a search summary (not verified) | lessgames: "ad revenue and subscriptions". songless.org: Mediavine ads. Songless+ paid tier on songless.pro (not opened) | [lessgames](https://lessgames.com/songless), [lessgames about](https://lessgames.com/about), [songless.org](https://songless.org), [songless.org privacy](https://songless.org/privacy) |
| **Spotle** (Flatwhite Studios per the site's JSON-LD) | Guess a mystery artist in 10 tries from 1,000; each guess shows attribute tiles (debut year, members, popularity rank, gender, genre, country per secondary sources) | None in the guess loop. Artist images from Apple's CDN with an `itunesId` per artist (observed). A track after a correct guess is claimed by a secondary source (not verified) | Live | Rank 2 of music dailies on Dailydles; no figures | Ads or other income not visible in static HTML (only a Google tag found); sister game "Unshuffle" promoted | [spotle.io](https://spotle.io), [Screen Rant](https://screenrant.com/spotle-spotify-wordle-game-play-how/) (not opened) |
| **Crosstune** (Flatwhite Studios per a review site) | Daily crossword whose clues are audio snippets | Apple Music snippet, per one review site only (not verified) | Listed live (rank 3) | Not verified | Not verified | [Dailydles](https://dailydles.com/categories/music), [aqviz](https://aqviz.com/crosstune/) (not opened) |
| **Harmonies** | Sort 16 music-related items into 4 hidden groups (NYT Connections style) | Appears text-only; maker attribution conflicts across sites | Listed live (rank 4) | Not verified | Not verified | [Dailydles](https://dailydles.com/categories/music) |
| **Lyricle** | Name the song from its lyrics, line by line; Unlimited mode; sister game Movie Grid | Lyrics (source not stated on its pages); after a guess the player can listen on SoundCloud (MakeUseOf) | Live (page answered) | Rank 10; no figures | Not visible | [lyricle.app](https://www.lyricle.app), [privacy policy](https://www.lyricle.app/privacy-policy), [MakeUseOf](https://www.makeuseof.com/spotify-kills-heardle-alternatives/) |
| **Musicle** (@adrianosbr) | Listen to one song, pick from 4; "Royale" mode: 6 songs, 9 options, no mistakes; country rankings | "Data and samples from the Apple Music API"; a "Listen on Apple Music" link after the guess (observed) | Live | Not ranked in the top 10; no figures. An unrelated iOS "Musicle" has 2 ratings | Ads; "one-time fee" for a lifetime ad-free version (price not visible) | [musicle.app](https://musicle.app) |
| **Sampledle** | Hear an original sample (drums, vocals, bass, melody); name the hit that sampled it in 5 tries | SoundCloud player widget (observed in page source) | Live | Not verified | Not verified | [sampledle.com](https://sampledle.com) |
| **SongPop Classic / SongPop** (FreshPlanet, Gameloft) | Not daily: head-to-head "name that tune" on themed playlists, 4 options | Licensing not documented in the sources read; Wikipedia only says iTunes links are provided and SongPop 3 integrates Spotify and Apple Music | Live: iOS update 2026-10-26 | Launched May 2012; 100M downloads by 2015 (Wikipedia); iOS 63,315 ratings (lookup) | Free with in-app purchases; ads; SongPop Plus USD 9.99 with 7-day trial and ads-free USD 3.99 for legacy VIPs, per Gameloft help pages seen in search results (not opened) | [Wikipedia](https://en.wikipedia.org/wiki/SongPop), [iOS lookup](https://itunes.apple.com/lookup?id=975364678&country=us) |
| **Hitster** (Jumbo) | Not daily: physical card game; scan a QR code, the song plays, players place it on a timeline | Plays through the user's streaming service; app connects to Spotify; YouTube Music and Deezer players must search the song by hand; "some songs may not be available in your region due to licensing restrictions" | Live | 1.4k ratings, 4.7, Belgian App Store (search summary; not verified) | Sells the cards; app is a free companion | [Hitster FAQ](https://hitstergame.com/en-us/faq/) |
| **Framed** (film, not music) | Guess the film from six frames; modes for one frame, titleshot, poster | Images, no audio | Live | A counter of 9,860,669 shown on the page (meaning not stated) | Merch: "Every order helps keep Framed going" | [framed.wtf](https://framed.wtf) |
| **Daily modes inside league apps** | Cut Club "Daily Cut" (vote on five songs a day, streak); YapZap "Daily YapZap" rooms; TuneBoxed "Song of the Day" with leaderboards | Link-out to Spotify or YouTube (Cut Club); previews and Spotify sign-in (TuneBoxed) | Live | Cut Club 6 iOS ratings; TuneBoxed 21; YapZap 7 | Host pays per season (Cut Club); subscription (TuneBoxed+) | [competitors.md](competitors.md) |

### Notes

- **Songless is a name, not one product.** A search found at least seven separate sites using it, with no common owner (search summary; not verified). The lessgames and songless.org pages I opened differ in clip length and in monetisation. I treat the lessgames page data as the best evidence of how one implementation plays audio: three sources per track (own file, Apple preview URL, SoundCloud id). Which of them is used in play, and under what licence, is not stated (**not verified**).
- **Apple preview URLs in a web game.** Songless (lessgames) holds `itunesPreviewUrl` values on `audio-ssl.itunes.apple.com`, and Musicle names the Apple Music API. Earlier study 05 reads guideline 5.2.5 and the Search API terms as a grey zone for a game that earns money, and the iTunes Search API has no ISRC lookup ([apple-music-access.md](apple-music-access.md)). Neither game states how it squares with those terms.
- **Why Heardle's audio source matters (inference).** SoundCloud's API terms (effective 30 March 2024) say user content may not be used in a "game ... unless you've obtained all relevant licenses" ([other-services.md](other-services.md), [SoundCloud terms](https://developers.soundcloud.com/docs/api/terms-of-use)). Heardle's SoundCloud-based design predates those terms, and I found no source saying SoundCloud or a rights holder objected to it.
- **Bandle's route is the only one with a stated cost.** Levy says licensing "can be complicated and expensive" and takes a large share of ad revenue; he does not say which licences he holds or how recreations are treated. General background on cover-song licensing (a mechanical licence from the publisher) came from a search summary of CD Baby and is not Bandle-specific (not verified).
- **Spotle's data are facts, not recordings (inference).** Attribute tiles (debut year, genre, country) are metadata; whether Spotify, Apple or MusicBrainz terms allow building such a table was not researched. Spotle's page lists an `itunesId` per artist, which points to Apple's catalogue as the lookup key.
- **Games with no audio exist and rank well.** Spotle (2), Harmonies (4) and Relatle (9) are on Dailydles' top ten without an audio loop. The ranking method is unstated.
- **Daily game as retention inside a league product has precedent.** Wordle shows the daily format needs only a shared puzzle and a spoiler-free result (see below); the three league apps above attach a daily mode to their league product, so it is not an empty field (see [competitors.md](competitors.md)).

## What happened to Heardle and others that died

**Heardle: verified timeline**

| Date | Event | Source |
|---|---|---|
| Dec 2021 | Development begins (Wikipedia, citing NME) | [Wikipedia](https://en.wikipedia.org/wiki/Heardle) |
| 26 Feb 2022 | Released by Omakase Studios (London); audio from SoundCloud | [Wikipedia](https://en.wikipedia.org/wiki/Heardle) |
| 12 Jul 2022 | Spotify announces the acquisition; price undisclosed; first Spotify game purchase; players can hear the full song on Spotify after each game; "look and feel ... will stay the same"; stays free | [TechCrunch](https://techcrunch.com/2022/07/12/spotify-acquired-heardle-wordle-music-game) |
| mid Apr 2023 | Spotify announces closure. MBW dates the tweet 16 April; a Digital Music News URL is dated 14 April (page not opened), so the exact day differs by source | [MBW](https://www.musicbusinessworldwide.com/spotify-to-shutter-music-trivia-game-heardle-less-than-a-year-after-acquiring-it/), [DMN](https://www.digitalmusicnews.com/2023/04/14/heardle-spotify-shutdown/) |
| 4 May 2023 | Last day to screenshot stats | [MakeUseOf](https://www.makeuseof.com/spotify-kills-heardle-alternatives/) |
| 5 May 2023 | Game closed | [MBW](https://www.musicbusinessworldwide.com/spotify-to-shutter-music-trivia-game-heardle-less-than-a-year-after-acquiring-it/), [MakeUseOf](https://www.makeuseof.com/spotify-kills-heardle-alternatives/) |

The brief's version (bought 2022, shut 2023) is correct. The one correction: the closure was announced in April 2023 and took effect on 5 May 2023.

**Reasons: what is stated and what is guessed**

- **Stated by Spotify:** "After careful consideration" it "made the difficult decision to say goodbye to Heardle" to "focus our efforts on other features for music discovery" (quoted in [MBW](https://www.musicbusinessworldwide.com/spotify-to-shutter-music-trivia-game-heardle-less-than-a-year-after-acquiring-it/) and [MakeUseOf](https://www.makeuseof.com/spotify-kills-heardle-alternatives/)). No other reason was given.
- **Reported, not stated:** Billboard, via an IMDb news page, called it a casualty of Spotify's cost-trimming (search summary; page not opened). Spotify closed its live audio app the same month (MBW).
- **Traffic:** Similarweb figures above show a 41M-to-6M monthly-visit fall between June 2022 and March 2023, after a 69M peak in March 2022 (TechCrunch, MBW). MBW notes Wordle's traffic also reportedly fell after the New York Times bought it.
- **Speculation by a commentator:** MakeUseOf suggests regional blocking, TikTok-heavy song choices and repeated artists. These are its opinions, not findings.
- **No documented legal cause.** I found no takedown, label letter or SoundCloud action. A Hacker News comment on the acquisition mentions a looming cease-and-desist; it is a commenter's speculation ([thread](https://news.ycombinator.com/item?id=32070292), not opened). A site claiming clones died from licensing gives no cases (musicianle.com, not opened).
- **A tension worth stating (inference):** Spotify's own Developer Policy says "Do not create a game, including trivia quizzes" ([spotify-access.md](spotify-access.md)). A first-party Heardle sat outside that policy as Spotify's own product, but the same policy would bar a third party from building it on Spotify's platform.

**Others that died or changed form**

- **Heardle clones.** The ecosystem continued as clones (Heardle Decades, Unlimited, artist editions). The clone-maker of Heardle Decades says in its FAQ that all games are one person's side project and that a song may not play in some countries (search summary of the FAQ; not opened).
- **Songlio.** Named as a Heardle alternative in 2023 (MakeUseOf); by 2026 it is "now an AI music generator, not a game" ([competitors.md](competitors.md)).
- **SongPop 1.** Shut in November 2018 over iOS 12 compatibility and replaced by SongPop 2 ([Wikipedia](https://en.wikipedia.org/wiki/SongPop)). A product end for technical reasons, not a rights case.
- **Songspot on playdaily.org.** An aggregator says the original host no longer serves it, with no reason (not verified).
- **No other documented shutdown** of Bandle, Songless, Spotle, Musicle or Lyricle appeared in the searches I ran. Absence of reports is not evidence they are healthy.

## Recap and story formats

| Format | Who | How it is built | Share mechanic | Money | Source |
|---|---|---|---|---|---|
| **Platform year-end story** | Spotify Wrapped 2025 (3 Dec 2025) | In-app stories from the user's own listening history. Needs 30+ songs played 30+ s each and 5+ artists. Added Listening Age, Top Song Quiz, Clubs, Listening Archive (AI-generated daily reports) and Wrapped Party (live, up to nine friends, group awards). Spotify says it uses a large language model for storytelling | Share cards to Spotify Messages or "favorite social channels"; the Spotify page does not name Instagram or TikTok | No direct revenue stated (marketing and retention; inference). At the 2022 Heardle deal Spotify cited "organic social media sharing, as with Spotify Wrapped" | [Spotify Newsroom](https://newsroom.spotify.com/?p=37685), [TechCrunch 2025](https://techcrunch.com/2025/12/03/spotifys-2025-wrapped-becomes-a-multiplayer-experience/) |
| Wrapped traction | Spotify | n/a | 250M engaged users in 65 hours (over a week in 2024); 575M shares; Instagram shares nearly doubled year on year; Listening Age story 65M shares; in-app messaging +100%. Source: Variety's report of Spotify's data (page paywalled; figures seen in search summaries only, not verified). A secondary blog gives about 500M shares | n/a | [Variety](https://variety.com/2025/music/news/spotify-wrapped-breaks-own-record-250-million-engagements-1236603493/) |
| **Wrapped 2026** | Spotify | Not yet released on 2026-11-22. No official date found; third-party sites estimate Wednesday 2 December 2026 (pattern since 2021, inference) | n/a | n/a | [Yahoo News UK](https://uk.news.yahoo.com/does-spotify-wrapped-2026-come-192448915.html) (search summary) |
| **Apple Music Replay** | Apple | Replay 2025 launched 2 Dec 2025; native in the Music app from iOS 26 and at replay.music.apple.com; a "Highlight Reel" of images and video | "Designed to be shared on social media platforms like Instagram and TikTok" | Not stated | [MacRumors](https://www.macrumors.com/2025/12/02/apple-music-replay-2025-fully-available/) |
| YouTube Recap | Google | Launched 2 Dec 2025 in North America (search summary; not opened) | Not verified for 2025 | Not stated | [Thurrott](https://www.thurrott.com/music-videos/330314/youtube-apple-music-amazon-music-more-launch-yearly-recaps) (not opened) |
| **Third-party personal stats** | stats.fm, Receiptify, Obscurify, Last.fm and others | OAuth to the user's Spotify account (read-only), or an uploaded extended streaming history | Image or page the user posts | stats.fm Plus: prices conflict across guides (USD 5.99 to 15 a year, or monthly plans); Receiptify free | [How-To Geek](https://www.howtogeek.com/see-spotify-wrapped-around-the-year-with-these-alternatives/) (search summary) |
| **League or group recap** | "Music League Wrapped" on Music League Stats (unaffiliated) | End-of-season recap: numbers, champions, awards, "the journey"; "ready to share once the final round has been voted on". Works from the group's export data; also pulls Last.fm and MusicBrainz data for genre stats | Not specified (image or link not stated) | "Sign up free"; no prices shown | [Music League Stats blog](https://musicleaguestats.com/blog) (post dated 2026-10-01) |
| League apps' own recaps | Cut Club: "recaps, badges, season standings"; BandJam: "23 charts" of analytics | Built from the league's own votes | Not verified | Cut Club host fee; BandJam free | [competitors.md](competitors.md) |
| **Result cards for daily games** | Wordle and every "-dle" | Spoiler-free emoji grid built from the player's guesses | Copy as text and paste anywhere; Wardle added the share button in Dec 2021 after players typed grids by hand; 1.2M results shared on Twitter 1 to 13 Jan 2022; 90 players on 1 Nov 2021 to 300,000 on 2 Jan 2022 | NYT bought Wordle on 31 Jan 2022 for "low seven figures" (secondary sources; NYT page blocked) | [Wikipedia: Wordle](https://en.wikipedia.org/wiki/Wordle) (not opened; figures from search summaries, discrepancies across sources) |
| Music daily result cards | Songless: "share your score" (songless.org); lessgames string table contains `SHARE_IMAGE` and "You've placed in the top {percentile}% today" (observed); Spotle: scorecard of squares (secondary) | Text or image of the result | Not detailed beyond the strings | See table above | [songless.org](https://songless.org), [lessgames](https://lessgames.com/songless) |
| **Automated league newsletter** | None found | Music League has an admin digest (batched about every 3 hours, "or sooner once 5 things have happened") and round-state emails, plus a separate "Newsletter & Marketing" switch that is the company's own marketing ([music-league-today.md](music-league-today.md)) | n/a | n/a | I found no product that sends an automatically written per-league newsletter in this market (searches limited; not verified) |

**Observations (inference).**

- Platform recaps work because the data are already inside the platform and the story is built in-app; the user's one-tap share is the growth loop. A league has no such listening data, but it has its own submissions, votes, comments and scores, which are enough for the "numbers, champions, awards" recap that Music League Stats sells ([Music League Stats](https://musicleaguestats.com/blog)). A recap from a game's own data needs no music-service API.
- The most-shared Wrapped item of 2025 (Listening Age, 65M shares) was a single-stat card, not the whole story. That is a design hint for per-league cards, stated as inference from the Variety figures above.
- Spotify says its Wrapped uses a large language model to add storytelling and natural-language summaries ([TechCrunch 2025](https://techcrunch.com/2025/12/03/spotifys-2025-wrapped-becomes-a-multiplayer-experience/)), so generated copy is already an expected feature.

## Sharing mechanics a web app can use

What a plain web app (no native app, no review) can do for free, with limits. Browser versions are from MDN's browser-compat-data (fetched 2026-11-22).

| Mechanism | What it does | Limits | Cost | Source |
|---|---|---|---|---|
| **Web Share API** `navigator.share({title, text, url, files})` | Opens the OS share sheet; the user picks the app (Messages, WhatsApp, Instagram and so on) | HTTPS only; needs a user gesture (transient activation); `title` may be ignored; you cannot tell which target was chosen. Use `navigator.canShare({files})` first; the file types allowed are decided by the browser. `share()`: Chrome 128 (desktop), Chrome Android 61, Edge 93, Safari 12.1, iOS Safari mirrors Safari, Firefox Android 79; Firefox desktop only behind the `dom.webshare.enabled` preference. `canShare()`: Chrome Android 75, Safari 14, Firefox Android 96. "Limited availability" on MDN | Free | [MDN share](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/share), [MDN canShare](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/canShare), [browser-compat-data](https://github.com/mdn/browser-compat-data) |
| **Share an image file to Instagram via the share sheet** | Pass a PNG through the Web Share API; on iOS Safari and Android Chrome Instagram appears as a target (developer reports) | Reports say adding a `url` can make the receiving app take the link and drop the image, and that Web Share cannot confirm a Story was posted. These come from GitHub issues, not from Meta (**not verified**) | Free | [example issue](https://github.com/mattkirwan/north-sea-charts/issues/127), [another](https://github.com/tedeuxx/tadeumendonca-io/issues/789) (search summaries; not opened) |
| **Instagram "Sharing to Stories" (Meta docs)** | Opens Instagram's story composer with a background image or video and a sticker | Documented for Android and iOS only; iOS URL scheme `instagram-stories://share?source_application=<AppID>`; Android intent `com.instagram.share.ADD_TO_STORY`; a Facebook App ID is required; background JPG or PNG at least 720x1280 (9:16), video up to 20 s; sticker JPG or PNG; images go through the pasteboard or a content URI. The page says nothing about web | The page states no fee (a Facebook App ID is needed) | [Meta docs](https://developers.facebook.com/docs/instagram-platform/sharing-to-stories/) |
| **TikTok Share Kit** | Native SDK to send photos or videos from an app to TikTok | iOS and Android only; needs a client key and the Share Kit product added to the app; media must be all videos or all images; up to 12 videos; aspect ratio between 1/2.2 and 2.2 (iOS quickstart as summarised in search results) | No fee stated | [Share Kit iOS](https://developers.tiktok.com/docs/en/share-kit-ios-quickstart-v2), [Share Kit Android](https://developers.tiktok.com/docs/en/share-kit-android-quickstart-v2) |
| **TikTok from the web** | The old web "Share Video API" is deprecated; the replacement is the Content Posting API | "All content posted by unaudited clients will be restricted to private viewing mode"; public posting needs an audit; scope `video.publish` | No fee stated; the cost is the audit | [Share Video API (deprecated)](https://developers.tiktok.com/docs/en/web-video-kit-with-web), [Content Posting API](https://developers.tiktok.com/doc/content-posting-api-get-started) |
| **Open Graph tags** | Link previews in chat apps and social feeds | Four required tags: `og:title`, `og:type`, `og:image`, `og:url`; add `og:image:width`, `og:image:height`, `og:image:alt`. The spec gives no size recommendation. Facebook's crawler caches images by URL ("won't be updated unless the URL changes") and needs gzip or deflate. Whether a crawler runs JavaScript was not stated on Meta's page; server-rendered tags are the safe choice (inference). WhatsApp, iMessage and Telegram preview rules were not checked against their own docs | Free | [ogp.me](https://ogp.me/), [Meta sharing docs](https://developers.facebook.com/docs/sharing/webmasters/) |
| **Per-result card image** | Create a PNG in the browser (Canvas) or on a server for the share sheet and for `og:image` | Satori (HTML and CSS to SVG) runs in browser, Node and Web Workers; MPL-2.0; you must supply a font; partial CSS only. On Cloudflare Workers: free plan 100,000 requests a day and 10 ms of CPU per invocation | Free within those limits; Workers Paid starts at USD 5 a month | [Satori](https://github.com/vercel/satori), [Workers pricing](https://developers.cloudflare.com/workers/platform/pricing/) |
| **Copy-to-clipboard text grid** | The Wordle mechanic: spoiler-free emoji grid pasted into any chat | No platform dependence; the user pastes | Free | [Wikipedia: Wordle](https://en.wikipedia.org/wiki/Wordle) (secondary) |
| **Download the PNG** | Fallback where `canShare({files})` is false (for example Firefox desktop); the user posts it by hand | Manual | Free | (inference) |

Conclusion for the sharing table (inference): from a web app the reliable free path to Instagram and TikTok is the OS share sheet with an image file on mobile, plus a pasted link with Open Graph tags; the platform-specific Stories URL scheme and TikTok Share Kit require a native app, and TikTok's web path requires an audit.

### Audio-clip routes, as practiced

The founder's note: a "mini clip" means a short audio clip; if no lawful low-cost route exists, the fallback is links only. This table states what the market does and the term it runs into; it does not recommend a route.

| Route | Who uses it | Terms it meets (earlier studies) | Money cost |
|---|---|---|---|
| Recreate the music yourself | Bandle | Composition rights still need licensing; Bandle says licensing is a large cost; terms not published | Per-song labour (1 to 3 h per song) plus licences (amount not published) |
| SoundCloud embed or widget | Heardle, Heardle Decades, Sampledle | API terms (30 Mar 2024) bar game use without licences and ban caching; registration needs Artist Pro | USD 99 a year for API access; the embed itself is keyless |
| Apple preview URL or Apple Music API | Songless (lessgames page data), Musicle, Crosstune (one review) | Guideline 5.2.5 (no "soundtrack to a game"); Search API terms; Apple Music API needs the Developer Program | Search API: none; MusicKit token: USD 99 a year |
| Self-hosted clip files | lessgames Songless (`cdn.lessgames.com`) | No source states a licence for these files (**not verified**) | Hosting only; legal exposure not assessed |
| Spotify embed or preview | None among the daily games read; Hitster plays through Spotify via its app | Spotify Developer Policy: "Do not create a game, including trivia quizzes"; Widget Terms need written approval for game functionality | None for embeds; no approval route documented |
| YouTube embed with `start` and `end` | No daily game found that documents it (**not verified**) | Visible player of at least 200x200 px, no audio-only, other rules in [youtube-access.md](youtube-access.md) | None; search is capped at 100 calls a day |
| Deezer 30 s preview | None found | Terms: "No games or businesses based on sound recordings" | n/a |
| No audio (metadata, artwork, text, lyrics, links) | Spotle, Harmonies, Lyricle, Relatle; Framed for film | Artwork and metadata terms vary by service; lyrics licensing not researched | Free |

## Open questions

1. Who holds the rights for lessgames' self-hosted `.aac` clips and the Apple preview URLs in its page data, and does any rights holder tolerate this? Not stated anywhere I could read.
2. How Bandle's licensing works in practice (which licences, from whom, cost per song). The Berklee piece says only that it is costly.
3. Whether a game that plays an Apple or SoundCloud preview as the object being judged (not as a soundtrack) is within guideline 5.2.5 and the SoundCloud game clause. Study 05 and study 07 leave this open.
4. Whether any daily game uses YouTube embeds with `start` and `end`, and how YouTube would treat a clip-guessing game. Searches found none.
5. Whether lyrics-based games (Lyricle) license their lyrics; the sources read do not say.
6. Primary confirmation of the Variety figures for Wrapped 2025 and of Wordle's sale price (both pages blocked here).
7. Real traction for Spotle, Songless, Musicle and Crosstune: only aggregator ranks (method unstated) and store ratings were found.
8. Whether an in-game result card posted via the OS share sheet reaches Instagram Stories on iOS and Android in 2026 as the developer reports say. Needs a test on devices; Meta's docs do not cover web.
9. Whether WhatsApp, iMessage and Telegram link previews have image-size or crawler rules that matter for a league invite card.
10. Whether a per-league recap or newsletter exists inside Cut Club or BandJam beyond what their marketing describes (not tested).

## Sources

Heardle and daily games
- https://techcrunch.com/2022/07/12/spotify-acquired-heardle-wordle-music-game (opened)
- https://www.musicbusinessworldwide.com/spotify-to-shutter-music-trivia-game-heardle-less-than-a-year-after-acquiring-it/ (opened)
- https://www.makeuseof.com/spotify-kills-heardle-alternatives/ (opened)
- https://en.wikipedia.org/wiki/Heardle (opened; secondary)
- https://www.digitalmusicnews.com/2023/04/14/heardle-spotify-shutdown/ (not opened; date only)
- https://news.ycombinator.com/item?id=32070292 (not opened)
- https://heardledecades.com/faq/ (not opened; search summary)
- https://online.berklee.edu/takenote/bandle-creator-johann-levy-on-the-music-quiz-100k-daily-players-love/ (opened)
- https://www.nbcnews.com/tech/tech-news/bandle-song-guessing-game-builds-buzz-online-rcna149012 (opened)
- https://bandle.app (opened; metadata only)
- https://apps.apple.com/us/app/bandle-guess-the-song-games/id6471419531 and https://itunes.apple.com/lookup?id=6471419531&country=us (opened)
- https://play.google.com/store/apps/details?id=com.bandlegame.bandleguessasong&hl=en_US (opened as raw HTML)
- https://lessgames.com/songless and https://lessgames.com/about (opened as raw HTML; page data)
- https://songless.org and https://songless.org/privacy (opened)
- https://apps.apple.com/us/app/songless/id6751617472 (opened)
- https://spotle.io (opened as raw HTML), https://screenrant.com/spotle-spotify-wordle-game-play-how/ (not opened)
- https://www.lyricle.app and https://www.lyricle.app/privacy-policy (opened)
- https://musicle.app (opened), https://sampledle.com (opened), https://framed.wtf (opened)
- https://dailydles.com/categories/music (opened; aggregator)
- https://aqviz.com/crosstune/ (not opened; search summary)
- https://en.wikipedia.org/wiki/SongPop (opened; secondary), https://itunes.apple.com/lookup?id=975364678&country=us
- https://hitstergame.com/en-us/faq/ (opened)

Recaps
- https://newsroom.spotify.com/?p=37685 (opened)
- https://techcrunch.com/2025/12/03/spotifys-2025-wrapped-becomes-a-multiplayer-experience/ (opened)
- https://variety.com/2025/music/news/spotify-wrapped-breaks-own-record-250-million-engagements-1236603493/ (paywalled; figures from search summaries)
- https://uk.news.yahoo.com/does-spotify-wrapped-2026-come-192448915.html (search summary)
- https://www.macrumors.com/2025/12/02/apple-music-replay-2025-fully-available/ (opened)
- https://www.thurrott.com/music-videos/330314/youtube-apple-music-amazon-music-more-launch-yearly-recaps (not opened)
- https://www.howtogeek.com/see-spotify-wrapped-around-the-year-with-these-alternatives/ (not opened; search summary)
- https://musicleaguestats.com/blog (opened)
- https://en.wikipedia.org/wiki/Wordle (not opened; search summaries)

Sharing
- https://developer.mozilla.org/en-US/docs/Web/API/Navigator/share (opened)
- https://developer.mozilla.org/en-US/docs/Web/API/Navigator/canShare (opened)
- https://github.com/mdn/browser-compat-data (api/Navigator.json read from raw, v8.1.10)
- https://developers.facebook.com/docs/instagram-platform/sharing-to-stories/ (opened)
- https://developers.tiktok.com/docs/en/share-kit-ios-quickstart-v2 and https://developers.tiktok.com/docs/en/share-kit-android-quickstart-v2 (search summaries)
- https://developers.tiktok.com/docs/en/web-video-kit-with-web (opened)
- https://developers.tiktok.com/doc/content-posting-api-get-started (opened)
- https://ogp.me/ (opened)
- https://developers.facebook.com/docs/sharing/webmasters/ (opened)
- https://github.com/vercel/satori (opened)
- https://developers.cloudflare.com/workers/platform/pricing/ (opened)
- https://developers.google.com/youtube/player_parameters (opened)
- https://github.com/mattkirwan/north-sea-charts/issues/127 and https://github.com/tedeuxx/tadeumendonca-io/issues/789 (not opened; search summaries)

Earlier studies in this folder (reused): spotify-access.md, apple-music-access.md, other-services.md, youtube-access.md, competitors.md, music-league-today.md, group-channels.md.
