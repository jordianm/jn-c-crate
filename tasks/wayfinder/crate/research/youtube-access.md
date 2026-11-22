# What a new social music game can do with YouTube and YouTube Music

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [What a new game can do with YouTube](../06-youtube-access.md)

Page dates are the "Last updated" lines shown on each page, quoted where they matter. Inferences are marked (inference). Anything I could not check against a primary source is marked **not verified**.

## Answer

- **Embedding needs no API key and no quota.** The IFrame Player "does not require authorization just as users do not need to log in to the YouTube website to watch a video" ([Developer Policies](https://developers.google.com/youtube/terms/developer-policies), updated 2026-11-06). That is the one free, universal playback layer. But embeds are not outside the rules: "The YouTube API Terms of Service and Developer Policies apply to all access and use of the YouTube embedded player" ([YouTube Help](https://support.google.com/youtube/answer/171780?hl=en)).
- **An ad-hoc list of songs can be played without the API.** `player.loadPlaylist([id1, id2, …])` and the `playlist=` URL parameter both take video IDs directly ([IFrame Player API](https://developers.google.com/youtube/iframe_api_reference), updated 2026-10-15; [Player parameters](https://developers.google.com/youtube/player_parameters), updated 2026-11-01). No maximum list length is documented (**not verified** in practice).
- **Search is the bottleneck.** Default quota is 100 `search.list` calls per day per project, in its own bucket, plus 10,000 units per day for all other methods ([Quota Calculator](https://developers.google.com/youtube/v3/determine_quota_cost), updated 2026-11-12). The 100 is shared by all your users. At two searches per song pick, that is about 50 picks a day for the whole product (arithmetic).
- **Playlist export through the API is expensive.** `playlists.insert` and `playlistItems.insert` cost 50 units each and need the user's OAuth consent ([playlistItems.insert](https://developers.google.com/youtube/v3/docs/playlistItems/insert)). A 10-song round is 550 units, so about 18 such playlists a day on default quota (arithmetic).
- **More quota needs an audit, with no published size, fee or timeline.** "You must first complete an audit to show that your project is in compliance" ([Quota and Compliance Audits](https://developers.google.com/youtube/v3/guides/quota_and_compliance_audits), updated 2026-11-12). The extra quota is valid only for the approved use case ([Developer Policies](https://developers.google.com/youtube/terms/developer-policies)). No price for API access appears in the terms or the quota pages.
- **The rules that bite a music game:** no background player, no separating audio from video, no overlays on the player, a visible player of at least 200 by 200 px, no incentives for watching, a privacy policy that names YouTube, and a Made For Kids lookup per embedded video. Quotes below.
- **YouTube Music has no official API** that I could find. `music.youtube.com/watch?v=ID` carries the same video ID as youtube.com (observed with oEmbed). Unofficial libraries emulate the web client with the user's cookies, and both sets of YouTube terms prohibit automated access outside the official API (my reading, inference).
- **There is no sanctioned search outside the Data API.** The embedded player's search-results mode was deprecated in 2020 ([IFrame Player API](https://developers.google.com/youtube/iframe_api_reference)). Realistic design: users paste YouTube or YouTube Music links, resolved by oEmbed (no key), with the Data API search as a rationed extra.

## 1. YouTube Data API v3: quota, costs, audit

**Default quota (verified).** "Projects that enable the YouTube Data API have a default quota allocation of 100 search.list calls, 100 videos.insert calls, and 10,000 units per day combined for all other endpoints… Daily quotas reset at midnight Pacific Time (PT)" ([Quota Calculator](https://developers.google.com/youtube/v3/determine_quota_cost), 2026-11-12). The same text appears in [Getting started](https://developers.google.com/youtube/v3/getting-started) and the [audit guide](https://developers.google.com/youtube/v3/guides/quota_and_compliance_audits).

**The June 2026 change (verified, with a nuance).** The [Revision History](https://developers.google.com/youtube/v3/revision_history) (updated 2026-11-17), entry of June 1, 2026: "The YouTube Data API is transitioning to a granular quota system… API calls to the videos.insert and search.list methods will be charged to their own respective quota buckets." The search.list reference says: "Quota impact: 100 calls per day. A call to this method has a quota cost of 1 unit in the Search Queries quota bucket" ([search.list](https://developers.google.com/youtube/v3/docs/search/list), 2026-11-12). A Wayback snapshot of the Quota Calculator (page "Last updated 2025-12-04") shows `search.list` at 100 units out of the 10,000 default, so the effective cap was already about 100 searches a day ([snapshot](https://web.archive.org/web/20260301000000/https://developers.google.com/youtube/v3/determine_quota_cost)). The change did not cut search. It stopped searches from eating the pool the other methods use (see Corrections).

**Unit costs that matter for this game** (all from the [Quota Calculator](https://developers.google.com/youtube/v3/determine_quota_cost)): `videos.list` 1, `playlistItems.list` 1, `playlists.list` 1, `channels.list` 1, `playlists.insert` 50, `playlistItems.insert` 50, `playlistItems.delete` 50. "All API requests, including invalid requests, incur a quota cost of at least one point." Extra result pages of `search.list` each count; `maxResults` is 0 to 50, default 5 ([search.list](https://developers.google.com/youtube/v3/docs/search/list)).

**Realistic daily numbers on default quota (arithmetic from the figures above):**

| Action | Cost | Per day |
|---|---|---|
| Searches | 1 of the 100-call bucket | 100 in total, all users together |
| Metadata lookup by ID (`videos.list`) | 1 unit | up to 10,000 if nothing else is used |
| One playlist of 10 songs created in the user's account | 1 × 50 + 10 × 50 = 550 | about 18 |
| One playlist of 20 songs | 1,050 | about 9 |
| Playlist inserts only (any mix of create and add) | 50 | 200 |

Quota is counted per Cloud project, not per user. Splitting across projects is barred: the Developer Policies require "exactly one (1) API Project for that API Client", forbid sharing credentials with third parties and embedding them "in open source projects", and the [compliance guide](https://developers.google.com/youtube/terms/developer-policies-guide) (updated 2026-09-14) says "You can't create multiple apps/sites or create multiple Google Cloud projects… to artificially acquire more API quota (aka 'sharding')". So a "bring your own API key" scheme to multiply quota is, on my reading, not allowed (inference).

**Caching search results.** The policies allow "temporarily store limited amounts of Non-Authorized Data… not longer than 30 calendar days", after which it must be deleted or refreshed ([Developer Policies](https://developers.google.com/youtube/terms/developer-policies), III.E.4). Caching popular queries for up to 30 days would stretch the 100 searches (inference). Stored data must be refreshed to stay "consistent with the current data".

**Write access needs OAuth.** `playlistItems.insert` requires one of the scopes `youtube`, `youtube.force-ssl` or `youtubepartner` ([playlistItems.insert](https://developers.google.com/youtube/v3/docs/playlistItems/insert)). Google says an app that requests sensitive or restricted scopes without verification gets an unverified-app screen and "will be limited to 100 new users until it is verified" ([Unverified apps](https://support.google.com/cloud/answer/7454865?hl=en)). Whether the `youtube` scope is classed sensitive is **not verified** (the scopes page I read does not show the class). Verification "might require several months" per the same page.

**Audit and quota extension.** The process, from the [audit guide](https://developers.google.com/youtube/v3/guides/quota_and_compliance_audits): fill out the "YouTube API Services - Audit and Quota Extension Form"; "A member of YouTube's API Services team will contact you as soon as possible". After a pass, a further extension within 12 months uses the same form. There is an Appeals Form for failed audits, a Periodic Audit Form if Google contacts you, and a Change of Control Form. The Developer Policies add: "you can apply for a quota extension by completing an API Compliance Audit where you must specify the use case"; "you must use the additional quota granted only for the approved use case. If your API Client's use case changes… [you must] resubmit". Also: YouTube may curtail access "if your API Project has been inactive for 90 consecutive days". The June 2026 revision entry says the granular system "simplifies the path to quota increases by allowing YouTube to verify and approve requests based on specific method usage", so a search-only increase may now be requested alone (inference).

No primary source gives an approval time, a quota size, or approval criteria. Secondary blogs report review times from days to months and frequent partial approvals ([secondary: Adaptly](https://adaptlypost.com/blog/youtube-api-quota-extension), as summarised by a search tool; **not verified**). Compliance work includes the privacy policy and the rules in section 2.

**Cost.** The Terms of Service ([API Services ToS](https://developers.google.com/youtube/terms/api-services-terms-of-service), updated 2026-11-06) and the quota pages state no fee for API access, and the quota table lists only units. The ToS liability cap refers to "the amount paid by you to YouTube", which implies no payment is expected, but it states no price (inference). Money cost: none found. Real costs are the compliance work and the audit wait.

## 2. Terms and policies that affect a music game

Documents and dates: [API Services Terms of Service](https://developers.google.com/youtube/terms/api-services-terms-of-service) (updated 2026-11-06); [Developer Policies](https://developers.google.com/youtube/terms/developer-policies) (2026-11-06); [Compliance guide](https://developers.google.com/youtube/terms/developer-policies-guide) (2026-09-14); [Required Minimum Functionality](https://developers.google.com/youtube/terms/required-minimum-functionality) (2026-11-06); [YouTube Terms of Service](https://www.youtube.com/t/terms?hl=en&gl=US) ("Effective as of December 15, 2023"). The API Terms of Service include the YouTube Terms of Service as a component of "the Agreement" (section 2.1).

**Audio-only, background play, modifying the player** (Developer Policies, section III.I, "You and your API Clients must not…"):
- "separate, isolate, or modify the audio or video components of any YouTube audiovisual content… For example, you must not apply alternate audio tracks to videos"
- "promote separately the audio or video components"
- "create, include, or promote features that play content, including audio or video components, from a background player, meaning a player that is not displayed in the page, tab, or screen that the user is viewing"
- "modify, build upon, or block any portion or functionality of a YouTube player"
- "modify, interfere with, replace, or block advertisements"

The compliance guide gives the example "Using YouTube's API to allow videos to play even when your API service window is closed or minimized" and says custom play buttons over the thumbnail are fine only if tapping initiates playback. Consequence (inference): no audio-only mode, no hidden player, no lock-screen or background play.

**Minimum player and overlays** ([Required Minimum Functionality](https://developers.google.com/youtube/terms/required-minimum-functionality)): "Embedded players must have a viewport that is at least 200px by 200px", with 480 by 270 recommended for 16:9. "You must not display overlays, frames, or other visual elements in front of any part of a YouTube embedded player, including player controls." "You must not make changes to the YouTube player that are not explicitly described by the API documentation." The compliance guide allows overlays only "for the purposes of obtaining user consent or playback controls" that do not conflict with the player UI. So the player must stay fully visible, and a "hide the video to guess the artist" mechanic would conflict (inference).

**Autoplay** (same document): "an API Client must not initiate an automatic playback until the player is visible and more than half of the player is visible". "A page or screen must not have more than one YouTube player that automatically plays content simultaneously." Whether auto-advance inside a `loadPlaylist` list counts as autoplay is **not verified**.

**Incentives and gating** (Developer Policies, Playback Integrity): "API Clients must not charge users to watch content in an embedded YouTube player." They "must not otherwise gate access to a video by requiring a user to take an action other than clicking the play button". They "must not offer or provide incentives, rewards, or other compensation to users for engaging with YouTube Applications (directly or indirectly) by performing actions like viewing content". The compliance guide's example: "Offering the chance to win a prize or offering financial compensation in exchange for a user watching a video." Login is allowed ("normal functionality… such as login or age verification"). Risk for the game (inference): points, badges or unlocks tied to listening to a song. Voting after listening is not a reward for viewing, but I found no clause that clears it either.

**Contests, games, monetising.** I found no clause about games or contests as such. Commercial rules: ad-enabled clients are permitted, but you must not "sell advertising, sponsorships, or promotions on any page or screen that contains YouTube API Data unless other data, content, or material not obtained from YouTube appears on the same page and offers enough independent value"; selling API access or ads "placed on or within YouTube audiovisual content or the YouTube player" needs written approval. The compliance guide adds "You also cannot charge people a fee for services that are offered free of charge on YouTube", and requires "sufficient independent value" if you mimic YouTube experiences. A paid tier for game features (as opposed to YouTube access) looks compatible (inference; ask a lawyer before charging).

**Storing content.** "download, import, backup, cache, or store copies of YouTube audiovisual content" and "make content available for offline playback" are prohibited without written approval (III.E.1). API metadata: 30-day limit above.

**Using anything but the API.** Developer Policies: you must not "use any technology other than YouTube API Services to access or retrieve API Data, including to access any portion of any YouTube audiovisual content". The YouTube Terms: you may not "access the Service using any automated means (such as robots, botnets or scrapers) except (a) in the case of public search engines, in accordance with YouTube's robots.txt file; or (b) with YouTube's prior written permission".

**Privacy and legal text the game must carry** (Developer Policies, III.A): display a link to the YouTube Terms of Service and state in your own terms that users agree to be bound by them; make users agree to a privacy policy that is "prominently displayed", "notif[ies] users that the API Client uses YouTube API Services", links the Google Privacy Policy, discloses third-party content or ads and cookie-like storage, and (for authorised data) links Google's permissions page and gives a contact. Deletion: within 7 calendar days when a user revokes consent or asks for deletion, and API Data tied to a revocation via Google's page within 30 days. Embedded-player data: the player "collects and shares some basic user data with YouTube" on load; setting autoplay to false limits that before interaction. "API Clients must look up the Made For Kids status of each YouTube video that it embeds", and for those videos "turn off tracking" (III.E.4.j; method: [Made for Kids guide](https://developers.google.com/youtube/v3/guides/made_for_kids_status), which uses `videos.list`). Read literally, an embed-only product still needs one `videos.list` call per new video, so it is not fully API-free (inference). Branding: any page showing YouTube content must display YouTube Brand Features per the [Branding Guidelines](https://developers.google.com/youtube/terms/branding-guidelines) (not read in full: **not verified**), and you must not obscure attribution inside the player.

**Player identity.** Embeds must send the HTTP Referer. Error 153 is "The request does not include the HTTP Referer header or equivalent API Client identification" ([IFrame Player API](https://developers.google.com/youtube/iframe_api_reference)). A native app must set the Referer itself ([Required Minimum Functionality](https://developers.google.com/youtube/terms/required-minimum-functionality)).

## 3. IFrame Player API and plain embeds

- **Key and quota.** No key or authorization is needed for the player (quote in the Answer). The docs describe no quota for playback; the Quota Calculator lists only Data API methods. So embeds do not consume Data API quota (inference from the docs; no quota figure for the player is published).
- **Ad-hoc list.** Parameter: "`playlist` specifies a comma-separated list of video IDs to play. If you specify a value, the first video that plays will be the VIDEO_ID specified in the URL path, and the videos specified in the playlist parameter will play thereafter" ([Player parameters](https://developers.google.com/youtube/player_parameters)). JS: `cuePlaylist` / `loadPlaylist` "specifies an array of YouTube video IDs" ([IFrame Player API](https://developers.google.com/youtube/iframe_api_reference)). Controls: `nextVideo()`, `previousVideo()`, `playVideoAt(index)`, `setLoop`, `setShuffle`. The JS array avoids URL-length limits (inference).
- **List limit.** Neither page states a maximum number of IDs. A web search found none. A round of 8 to 30 songs is probably fine, but I could not test in a browser, so the limit is **not verified**.
- **Search mode is gone.** "The ability to load a list of search results is deprecated and will no longer be supported as of 15 November 2020" ([IFrame Player API](https://developers.google.com/youtube/iframe_api_reference)).
- **Embedding blocked by rights holders.** Documented behaviour: error `101` "The owner of the requested video does not allow it to be played in embedded players", `150` "is the same as 101", `100` removed or private, `5` HTML5 error ([IFrame Player API](https://developers.google.com/youtube/iframe_api_reference)). The Data API reports it in advance: `videos.list` field `status.embeddable` ([videos resource](https://developers.google.com/youtube/v3/docs/videos), 2026-11-17), and `search.list` can filter with `videoEmbeddable` and `videoSyndicated` ("only videos that can be played outside youtube.com"). `contentDetails.regionRestriction` lists allowed or blocked countries.
- **How often official music is blocked.** I found no data (one search for a percentage returned only troubleshooting pages). My own sample: oEmbed returned HTTP 200 for 11 of 11 well-known official music videos (see section 4, list of IDs in the calls table). That is a convenience sample of famous videos, not an estimate, and a 200 does not prove playback in every country. Plan for the 101/150 case anyway: show "Open on YouTube", which the compliance guide says must open in the YouTube app where installed.
- **Mobile.** Use OS WebViews (`WebView`/`CustomTabs`, `WKWebView`/`SFSafariViewController`) per [Required Minimum Functionality](https://developers.google.com/youtube/terms/required-minimum-functionality). The background-play prohibition applies to the embedded player, so a native app cannot keep it playing with the screen off (inference).

## 4. oEmbed endpoint (observed 2026-11-22)

`https://www.youtube.com/oembed?url=…` needs no key. It is not documented on developers.google.com/youtube (no hit in any YouTube doc I downloaded); it is listed for YouTube in the [oEmbed provider registry](https://oembed.com/providers.json). Whether it counts as a "YouTube API Service" under the terms is unclear (inference: probably not named, but the embed it returns is covered by the embed rules).

| Call | Result |
|---|---|
| `watch?v=dQw4w9WgXcQ` | 200. JSON: `title`, `author_name`, `author_url`, `type: "video"`, `thumbnail_url` (480×360 `hqdefault.jpg`), `provider_name`, `html` (an iframe on `/embed/ID?feature=oembed`), `width: 200`, `height: 113` |
| `music.youtube.com/watch?v=dQw4w9WgXcQ` | 200. Identical title, author and embed (`youtube.com/embed/dQw4w9WgXcQ`) |
| `youtu.be/dQw4w9WgXcQ?si=abc` | 200, same payload |
| `watch?v=…&list=PLFgquLnL59alCl_2TQvOiD5Vgm1hCaGSI` | 200. Embed URL carries `?list=…` |
| `music.youtube.com/playlist?list=PLFgquLnL59alCl_2TQvOiD5Vgm1hCaGSI` | 200. Title "Popular Music Videos", `type: "video"` (not "playlist"), embed `/embed/videoseries?list=…` |
| `watch?v=aaaaaaaaaaa` (nonexistent) | 400 "Bad Request" |
| `…&maxwidth=640&maxheight=360` | 200, `width: 640`, `height: 360` |
| 11 official videos (IDs 9bZkp7q19f0, kJQP7kiw5Fk, Zi_XLOBDo_Y, fJ9rUzIMcZQ, hTWKbfoikeg, OPf0YbXqDm0, JGwWNGJdvx8, YQHsXMglC9A, e-ORhEE9VVg, sOnqjkJTMaA, hLQl3WQQoQ0) | all 200 with title and author |

Observations: it returns title, channel name and thumbnail, which is enough to show a pasted song in a list. It does not return duration, view count, region or embeddable status. The default embed is 200×113, below the 200×200 minimum viewport, so size the iframe yourself or pass `maxwidth`/`maxheight` (inference). I made about 20 calls in total. For a non-embeddable video, secondary sources say oEmbed answers 401 ([GitHub issue](https://github.com/extractus/oembed-extractor/issues/168), via a search summary); I did not reproduce it (**not verified**).

Related, undocumented: `https://www.youtube.com/watch_videos?video_ids=ID1,ID2,ID3` answered with a 303 redirect to `watch?v=ID1&list=TLGG…`, i.e. YouTube builds a temporary playlist from a list of IDs (one HEAD request; the redirect was not followed). It is not in any documentation I read, so do not rely on it (inference). It would be an outbound "open the round in YouTube" link if it keeps working.

## 5. YouTube Music

- **Official API.** None found. No YouTube Music API appears in the YouTube Developer site pages I read (Data API, IFrame, policies). The only YouTube Music item on Google's OAuth scopes page is `dataportability.youtube.music`, "Move a copy of your uploaded YouTube music tracks and your YouTube music library", a data-export scope ([scopes](https://developers.google.com/identity/protocols/oauth2/scopes), 2026-09-14). Secondary pages say the same ([musicapi.com](https://musicapi.com/blog/youtube-music-api-2026-developer-access-endpoints-integration), a vendor that sells a unified music API, so it has an interest). Absence of evidence, not proof (**not verified** that no private or partner API exists).
- **Links to video IDs.** `music.youtube.com/watch?v=ID` is the same 11-character ID as `youtube.com/watch?v=ID` (observed: oEmbed returned the same video and embed URL). `music.youtube.com/playlist?list=ID` is a normal playlist ID (observed). Album and artist pages (`/browse/…`) were not tested: **not verified**. The same song can have separate IDs for the art track (Topic channel) and the official video, and YouTube Music can swap art tracks for uploaded videos ([secondary: DistroKid](https://support.distrokid.com/hc/en-us/articles/29268141694099-Why-Was-My-YouTube-Art-Track-Replaced-with-a-Video), via a search summary). So "the" video ID of a song is not unique (**not verified** by a primary source).
- **Unofficial libraries.** [ytmusicapi](https://ytmusicapi.readthedocs.io/en/stable/) (docs v1.12.4) describes itself as an "Unofficial API for YouTube Music" and "emulates YouTube Music web client requests using the user's cookie data for authentication" ([README](https://raw.githubusercontent.com/sigma67/ytmusicapi/main/README.rst)). It offers search, playlist create and edit, library access. Its FAQ says it has a rate limit ("There most certainly is") but gives no numbers.
- **Terms risk (my reading, inference).** (a) The YouTube Terms bar "any automated means (such as robots, botnets or scrapers)" without written permission. (b) The Developer Policies bar "any technology other than YouTube API Services to access or retrieve API Data". (c) Cookie-based auth uses a real user's session, so the enforcement risk lands on that user's Google account. I found no documented ban cases for ytmusicapi (**not verified**; a search tool's summary, not a full search). A product that depends on it would depend on an undocumented interface that can break at any time. Not recommended as a pillar.
- **Background play.** Under the policy above, a third-party player cannot offer it. That YouTube's own apps reserve background play for Premium is general knowledge, **not verified** here.

## 6. Search without the Data API

- **Sanctioned alternatives: none found.** The player's search mode was deprecated (section 3). oEmbed resolves a URL, it does not search. Scraping search pages or using proxies such as Invidious is "automated means" under the YouTube Terms (inference).
- **Design options inside the rules.**
  1. Users paste a link (YouTube, YouTube Music, youtu.be). Resolve with oEmbed. Zero quota. This is how BandJam works per study 01 (pasting a link).
  2. Search on another catalog (the game's own, or another service's licensed API) and resolve to a YouTube ID only on demand. Resolution still needs a YouTube search, so it hits the same 100-call bucket. Cache each result for up to 30 days.
  3. Data API search as an opt-in helper with a daily budget: 100 searches a day, cached, paged only when needed (each extra page costs 1 of the 100).
- **Arithmetic for a launch community.** 20 active leagues of 8 players, one pick per player per week, two searches per pick: 320 searches a week, about 46 a day, under the cap. 200 leagues would be about 460 a day, over the cap by a factor of 4.6. Cache hit rate and a link-paste default decide this. Playlist export for 20 leagues a week (1 round, 8 songs = 450 units): about 9,000 units a week, fine. For 200 leagues the same figure is about 13,000 units a day, over the 10,000 pool (arithmetic, assumptions stated).

## Options table

| | A. Embed-only, pasted links | B. Data API at default quota | C. Data API after audit |
|---|---|---|---|
| Key / OAuth | None for playback and oEmbed. A key for the Made For Kids lookup (inference) | API key for search, OAuth for playlist writes | Same as B |
| Song discovery | Users paste links; no in-app search | 100 searches a day for the whole product; cache up to 30 days | Higher, size not published; extra quota tied to the approved use case |
| Playback | `loadPlaylist` array or `playlist=`, free of quota | Same | Same |
| Playlist export | Not via API; outbound link only (the `watch_videos` URL is undocumented) | About 18 ten-song playlists a day; OAuth user; unverified-app 100-user cap until verification | Higher; review time and size unpublished |
| Metadata | Title, author, thumbnail via oEmbed; no duration or embeddable flag | `videos.list` 1 unit: `status.embeddable`, region restrictions, made-for-kids | Same |
| Main limits | No search; embed blocks (error 101/150) are known only on play, unless you check with `videos.list` | Search bucket empties fast; playlist inserts eat the 10,000 pool | Audit work, privacy policy, periodic audits, 90-day inactivity rule |
| Terms exposure | Embed rules apply (visible player, 200×200, no overlays, no background, privacy policy, Made For Kids) | Same plus data-handling rules (30-day storage, deletion in 7 and 30 days) | Same; use case must match the approval |
| Money | None | None found | None found; time and compliance work |
| Verdict (inference) | Viable launch core | Viable for a small community; search is the weak point | Needed before real growth; plan the application early |

Not in the table: ytmusicapi and scraping (section 5). They avoid quota but conflict with both sets of terms (inference).

## Corrections to study 01

Section "YouTube Data API" and the summary line of [study 01](../../../../research/01-market-music-league.md):
1. **"Since June 2026, the YouTube Data API allows only 100 searches per day per project by default" reads as a new cut. It was not a cut.** The 100 a day figure is confirmed ([Quota Calculator](https://developers.google.com/youtube/v3/determine_quota_cost)). But before June 2026, `search.list` cost 100 units out of the 10,000 pool, which also meant about 100 searches a day ([Wayback snapshot, page dated 2025-12-04](https://web.archive.org/web/20260301000000/https://developers.google.com/youtube/v3/determine_quota_cost)). The June 1 change gives search its own bucket, so the 10,000 units are now free for everything else. Net effect for this game: search is the same, and playlist writes and lookups got more room. The study's inference (search cannot support a community) still holds.
2. **"Plus 10,000 units per day for everything else"**: confirmed. **"playlists.insert and playlistItems.insert cost 50 units each… about 200 inserts per day"**: confirmed, but 200 counts playlist creation and every added song, so a 10-song playlist is 11 calls (about 18 playlists a day). Add that writes need user OAuth.
3. **"More quota requires a compliance audit… valid only for the approved use case"**: confirmed ([Developer Policies](https://developers.google.com/youtube/terms/developer-policies)). Add: the audit guide's form names, a 12-month window for later extensions, the June 2026 method-specific verification, and the absence of any published size or timeline.
4. **"Forbidden: separating audio from video, promoting them separately, background playback, and downloading or caching content"**: confirmed with quotes, but the caching ban covers audiovisual content only. API metadata may be stored temporarily up to 30 days. The study's inference (visible embedded player, no audio-only mode) is confirmed and sharper: also a 200×200 px minimum viewport and no overlays on the player ([Required Minimum Functionality](https://developers.google.com/youtube/terms/required-minimum-functionality)).
5. **Gaps in the study.** It does not say that embeds are covered by the API terms ([YouTube Help](https://support.google.com/youtube/answer/171780?hl=en)), that embedding needs no key or quota, the Made For Kids lookup, the no-incentive rule, or that the YouTube Terms ban scraping. It cites the Quota Calculator at `/youtube/data/…`, which is a valid redirect of `/youtube/v3/…`.

## Not verified and open questions

- Maximum length of `playlist=` or `loadPlaylist` arrays: not documented; not tested (no browser).
- Frequency of embed-disabled official music: no data found. My 11 of 11 oEmbed 200s is a convenience sample.
- Whether oEmbed returns 401 for non-embeddable videos: secondary source only; no known non-embeddable ID to test.
- Whether auto-advance inside a playlist counts as "autoplay" for the one-autoplay-player rule.
- Whether the `youtube` OAuth scope is "sensitive" (and so triggers the 100-user cap and verification); the cap text is from [Google](https://support.google.com/cloud/answer/7454865?hl=en), the scope class was not shown.
- Audit approval time, outcomes for small apps and the size of granted quota: no primary data; blogs disagree.
- Whether a pasted-link-only product legally needs an API project at all for the Made For Kids check (strict reading says yes). Needs a legal read, not an agent's.
- Whether a game-score mechanic tied to listening breaches the "no incentives" clause: my reading only.
- Whether a private or partner YouTube Music API exists; ytmusicapi ban cases; whether `watch_videos` stays stable.
- The [Made for Kids guide](https://developers.google.com/youtube/v3/guides/made_for_kids_status) says the default quota "is sufficient to check the MadeForKids video status of up to 5000 videos", which does not match the 1-unit cost of `videos.list` ([videos.list](https://developers.google.com/youtube/v3/docs/videos/list)); the guide looks stale.
- Branding Guidelines not read in full.
- Also whether `videos.list` accepts 50 IDs per call: the `id` parameter is a "comma-separated list", the cap was not shown.

## Sources

Primary (YouTube / Google):
- https://developers.google.com/youtube/v3/determine_quota_cost (Quota Calculator, updated 2026-11-12)
- https://developers.google.com/youtube/v3/revision_history (updated 2026-11-17)
- https://developers.google.com/youtube/v3/getting-started (2026-11-12)
- https://developers.google.com/youtube/v3/guides/quota_and_compliance_audits (2026-11-12)
- https://developers.google.com/youtube/v3/docs/search/list (2026-11-12)
- https://developers.google.com/youtube/v3/docs/playlistItems/insert (2026-11-12)
- https://developers.google.com/youtube/v3/docs/playlists/insert (50 units)
- https://developers.google.com/youtube/v3/docs/videos and https://developers.google.com/youtube/v3/docs/videos/list (2026-11-17)
- https://developers.google.com/youtube/v3/guides/made_for_kids_status (2026-11-12)
- https://developers.google.com/youtube/terms/api-services-terms-of-service (2026-11-06)
- https://developers.google.com/youtube/terms/developer-policies (2026-11-06)
- https://developers.google.com/youtube/terms/developer-policies-guide (2026-09-14)
- https://developers.google.com/youtube/terms/required-minimum-functionality (2026-11-06)
- https://developers.google.com/youtube/iframe_api_reference (2026-10-15)
- https://developers.google.com/youtube/player_parameters (2026-11-01)
- https://www.youtube.com/t/terms?hl=en&gl=US (YouTube Terms of Service, effective as of December 15, 2023)
- https://support.google.com/youtube/answer/171780?hl=en (Embed videos and playlists)
- https://support.google.com/cloud/answer/7454865?hl=en (Unverified apps)
- https://developers.google.com/identity/protocols/oauth2/scopes (2026-09-14)
- Live calls: `https://www.youtube.com/oembed` (about 20 requests, 2026-11-22); one HEAD request to `https://www.youtube.com/watch_videos`

Other:
- https://oembed.com/providers.json (oEmbed registry, YouTube entry)
- https://web.archive.org/web/20260301000000/https://developers.google.com/youtube/v3/determine_quota_cost (Wayback copy of the old Quota Calculator)
- https://ytmusicapi.readthedocs.io/en/stable/ and https://raw.githubusercontent.com/sigma67/ytmusicapi/main/README.rst (library's own docs)

Secondary, used only to find primaries or flagged as such (read through a search tool's summary, not fetched): https://adaptlypost.com/blog/youtube-api-quota-extension, https://musicapi.com/blog/youtube-music-api-2026-developer-access-endpoints-integration, https://github.com/extractus/oembed-extractor/issues/168, https://support.distrokid.com/hc/en-us/articles/29268141694099-Why-Was-My-YouTube-Art-Track-Replaced-with-a-Video
