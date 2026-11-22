# How to match a song across services

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [How to match a song across services](../08-song-matching.md)

## Answer

- **The free Odesli API is gone.** Linktree retired the public Songlink/Odesli API (`v1-alpha.1`) on 2026-07-31 and says every request now returns `410 Gone`. Only an allowlist for "developers and teams with a real, ongoing need" remains ([Linktree help, updated 2026-10-14](https://linktr.ee/help/en/articles/15201827)). On 2026-11-22 I called `api.song.link` without a key and got `401 {"code":"PUBLIC_API_ACCESS_DEPRECATED"}`. The `song.link` web pages still work. "Odesli first" is not a free design any more.
- **ISRC is the right key, but it identifies a recording, not a song.** Remasters, edits and mixes get their own ISRC, and the same recording keeps one ISRC across countries ([IFPI: when to assign](https://isrc.ifpi.org/en/why-use-isrc/when-to-assign), [when not to assign](https://isrc.ifpi.org/en/why-use-isrc/when-not-to-assign)). Expect several ISRCs, and several service IDs, for what listeners call one song.
- **ISRC lookup is free and keyless on Deezer only.** `GET https://api.deezer.com/track/isrc:GBFFP0300052` returned the track with no key (observed). TIDAL (`filter[isrc]`, up to 20 per call) and Apple Music (`filter[isrc]`, up to 25) need credentials. Apple needs a paid Developer Program membership ($99/year). Spotify (`isrc:` search filter) needs an app, which in Development Mode is capped at 5 users.
- **MusicBrainz is free and keyless for ISRC lookup and links to streaming services, but the links are sparse.** The ISRC lookup returned a recording for 8 of 8 sampled ISRCs. Only 5 of 8 had any Spotify, Apple, Deezer, TIDAL or YouTube URL relation, and only 1 of 8 had four services (my sample, n=8; see section 4). Limit: 1 request/second per IP, with a meaningful User-Agent ([rate limiting](https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting)). Core data is CC0 ([licence](https://musicbrainz.org/doc/About/Data_License)), but "Non-commercial use of this web service is free" ([API page](https://musicbrainz.org/doc/MusicBrainz_API)).
- **Terms are the real blocker for a game.** Spotify's Developer Policy says "Do not create a game, including trivia quizzes" and "Do not create any product or service which is integrated with streams or content from another service" ([policy, effective 2025-05-15](https://developer.spotify.com/policy)). Deezer's terms bar "games or businesses based on sound recordings" and "creation of Content database" ([Deezer terms, updated 2026-10-27](https://developers.deezer.com/termsofuse)). TIDAL's terms allow only non-commercial offerings and bar using TIDAL content "in podcasts, messaging applications, games" ([TIDAL Developer Terms v3.0](https://developer.tidal.com/documentation/guidelines-developer-terms)).
- **YouTube has no ISRC in its API.** The `videos` resource has no ISRC field ([docs](https://developers.google.com/youtube/v3/docs/videos); zero mentions). A YouTube link can only be matched by title and channel heuristics. Auto-generated "Artist - Topic" channels are the one reliable signal (observed via oEmbed).
- **The least risky free design keeps the match human-assisted.** Resolve what can be resolved with keyless sources (Deezer, MusicBrainz, iTunes Search for Apple links), mark the match with a confidence level, and let the submitter confirm or paste the missing link. Section 8 gives the designs and ceilings.

## 1. ISRC: what it is and where it breaks

- **Definition.** ISRC is the International Standard Recording Code. The ISRC agency says it "identifies a recording regardless of format or bit-rate" and "is not used to identify compositions or lyrics, nor ... products or releases" ([IFPI, when not to assign](https://isrc.ifpi.org/en/why-use-isrc/when-not-to-assign)). The US agency calls a finished ISRC a "'dumb' number" that "simply identifies the sound or music video recording" ([US ISRC Agency](https://www.usisrc.org/)). Compositions use ISWC instead ([MusicBrainz ISRC doc](https://musicbrainz.org/doc/ISRC), secondary).
- **Who assigns.** Rights owners assign them, using a prefix issued by a national ISRC agency; IFPI runs the international agency ([IFPI](https://isrc.ifpi.org/en/), [get a prefix](https://isrc.ifpi.org/en/get-isrc/get-an-isrc-prefix)). Format: 12 characters, country + owner + year + serial ([IFPI structure](https://isrc.ifpi.org/en/isrc-standard/isrc-structure)).
- **Rules that cause pitfalls.**
  - "Any new or materially changed recording must be provided with a new ISRC": different versions, mixes, edits ([IFPI](https://isrc.ifpi.org/en/why-use-isrc/when-to-assign)).
  - For remasters, "circumstances may determine whether a new ISRC is required or not" ([IFPI](https://isrc.ifpi.org/en/why-use-isrc/when-not-to-assign)). So a remaster may or may not share the original's ISRC.
  - The ISRC "should remain the same across different releases or formats" and when licensed or used in other countries (same page). In practice labels do not always follow this (inference).
- **Pitfalls seen live.**
  - One ISRC, two MusicBrainz recordings: `GBFFP0300052` ("Mr. Brightside") returned 2 recordings ([MusicBrainz ISRC lookup](https://musicbrainz.org/ws/2/isrc/GBFFP0300052?fmt=json&inc=url-rels)).
  - One recording, several service IDs: its MusicBrainz page links 3 Deezer track IDs and 2 Spotify track IDs.
  - Placeholder ISRC: Deezer answers `track/isrc:XXXXXXXXXXXX` with a real, unrelated track whose ISRC is literally `XXXXXXXXXXXX`. Reject obviously invalid codes.
  - Deezer returns one track per ISRC; Apple states "one ISRC value may return more than one song" ([Apple](https://developer.apple.com/documentation/applemusicapi/get-multiple-catalog-songs-by-isrc)); TIDAL returns several for a single ISRC with pagination ([TIDAL OpenAPI](https://tidal-music.github.io/tidal-api-reference/tidal-api-oas.json)). Always rank candidates, never take `[0]`.
  - User uploads on YouTube have no ISRC (section 6).
- **Coverage on streaming catalogs.** All four catalogs I checked expose ISRC on tracks (Deezer: field `isrc`; Spotify: `external_ids`; Apple: `isrc` attribute via filter; TIDAL: `filter[isrc]`). I found no primary source with a coverage percentage: **not verified**.

## 2. Streaming APIs: ISRC and access

| Service | ISRC field / lookup | Access needed | Limits and terms |
|---|---|---|---|
| Deezer | `/track/isrc:<ISRC>` returns the track incl. `isrc` (observed, keyless, HTTP 200). `search?q=isrc:...` returned empty (observed), so use the path form. | None for the public endpoints (observed). The terms speak of an application and "Credentials". | "about 50 requests per 5 seconds" only from secondary sources: **not verified**. Terms in section 3. |
| Spotify | Search filter `isrc` (tracks); track object has `external_ids` ([Search](https://developer.spotify.com/documentation/web-api/reference/search)). `external_ids` was marked removed in Feb 2026, then reverted ([Mar 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/march-2026)). | An app. New apps start in Development Mode: owner needs Premium, up to 5 authenticated users ([quota modes](https://developer.spotify.com/documentation/web-api/concepts/quota-modes)). Extended mode needs about 250k MAU (see [research 01](../../../../research/01-market-music-league.md)). | Search `limit` max cut from 50 to 10, default 5; Get Several Tracks removed ([Feb 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/february-2026)). Rate limit is a "rolling 30 second window" with no number published ([rate limits](https://developer.spotify.com/documentation/web-api/concepts/rate-limits)). |
| Apple Music | `GET /v1/catalog/{storefront}/songs?filter[isrc]=...`; "The maximum fetch limit is 25" ([Apple](https://developer.apple.com/documentation/applemusicapi/get-multiple-catalog-songs-by-isrc)). | Developer token (JWT, ES256) from "a member of the Apple Developer Program" ([Apple](https://developer.apple.com/documentation/applemusicapi/generating-developer-tokens)). Membership is "$99 annual" ([Apple programs](https://developer.apple.com/programs/)). Not free. | Rate limit not found: **not verified**. |
| Apple (iTunes Search/Lookup) | No ISRC. Lookup keys are id, UPC, AMG ID ([docs](https://performance-partners.apple.com/search-api)). `lookup?isrc=` returned `resultCount: 0`, and track results carry no `isrc` field (observed). | None. | "approximately 20 calls per minute (subject to change)" (same doc). Useful for title/artist/duration of an Apple link, not for ISRC. |
| TIDAL | `GET https://openapi.tidal.com/v2/tracks?filter[isrc]=...`, up to 20 ISRCs per call; one track per ISRC when several are given ([OpenAPI spec 1.10.258](https://tidal-music.github.io/tidal-api-reference/tidal-api-oas.json)). | OAuth bearer token; client-credentials flow is listed. Registering a developer app is free per secondary sources (not verified; portal is a JS app). | "TIDAL may limit the number of service calls ... in its sole discretion, without notice" ([Terms v3.0, 6 May 2024](https://developer.tidal.com/documentation/guidelines-developer-terms)). No numbers. |
| YouTube | None. | API key. | 100 `search.list` per day; 10,000 units per day for other endpoints ([quota](https://developers.google.com/youtube/v3/determine_quota_cost)). |

## 3. Terms of each streaming API (what blocks "a game")

- **Spotify** (Developer Policy effective 2025-05-15; Developer Terms v10): "Do not create a game, including trivia quizzes"; "Do not create any product or service which is integrated with streams or content from another service"; metadata must carry "a link back to the applicable album, content or playlist on the Spotify Service" ([policy](https://developer.spotify.com/policy), [terms](https://developer.spotify.com/terms)). Matching a Spotify track to other services is exactly "integrated with ... another service". Treat Spotify API use inside a competing game as prohibited (inference; Spotify's actual enforcement unknown).
- **Deezer** (updated 2026-10-27): non-commercial only ("shall not receive, generate or derive ... any revenue"); "No creation of Content database, no local copy"; "No games or businesses based on sound recordings"; access "granted on a selective basis" after review ([terms](https://developers.deezer.com/termsofuse)). Caching ISRC-to-Deezer-ID mappings is arguably a "Content database" (inference). The keyless endpoint works technically, but the terms assume an approved developer account; I could not confirm what applies to anonymous calls.
- **TIDAL** (v3.0, 6 May 2024): "sole purpose of developing and distributing non-commercial applications"; bans using TIDAL Content "in podcasts, messaging applications, games"; "limited to the temporary caching of metadata and cover art"; "Do not store TIDAL Content indefinitely" ([terms](https://developer.tidal.com/documentation/guidelines-developer-terms), text read from the portal's published bundle `developer-terms-3_0`).
- **Apple Music API**: terms and monetization limits are in [research 01](../../../../research/01-market-music-league.md). I did not re-check the MusicKit terms here: **not verified**.
- **YouTube**: API Services terms and quota in [research 01](../../../../research/01-market-music-league.md). Calling `videos.list` costs 1 unit, so about 10,000 lookups per day per project (inference from the quota page).

Pattern: every free catalog API is non-commercial and none explicitly blesses cross-service matching. A hobby, ad-free, non-monetized league is the only comfortable fit; a game that may later earn money is not.

## 4. MusicBrainz and ListenBrainz

- **Rate limit.** "Currently that rate is (on average) 1 request per second" per IP; above it "all your requests will be declined (http 503)" until the rate drops. Global cap 300/s. The page states its rules "as of 2012-01-08" and says they may change at any time ([rate limiting](https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting), revision 78895). I saw HTTP 503 twice at 1.2 s spacing from a shared sandbox IP, so budget for retries.
- **User-Agent.** Required, with contact information: `Application name/<version> ( contact-url )`. "Anonymous" agents (blank, `Java`, `Python-urllib`) are throttled harder (same page). A public project needs a real contact URL.
- **API access and cost.** No key. "Non-commercial use of this web service is free; please see our commercial plans" ([API](https://musicbrainz.org/doc/MusicBrainz_API)). MetaBrainz plans: non-commercial $0; "pre-revenue start-up and expect to have revenue in the future" must use a commercial tier; Stealth Start-Up and Non-profit tiers start at $0/month, Bronze $100/month ([supporters](https://metabrainz.org/supporters/account-type)).
- **Data licence.** "The core data of the database is licensed under the CC0"; supplementary data (tags, ratings) is CC BY-NC-SA 3.0 ([licence](https://musicbrainz.org/doc/About/Data_License)). Core data can be downloaded and mirrored with no restriction.
- **ISRC lookup.** `/ws/2/isrc/<ISRC>?inc=url-rels` "returns a list of recordings" ([API](https://musicbrainz.org/doc/MusicBrainz_API)). Tested: works with `fmt=json`.
- **Streaming links.** Recordings carry URL relations typed "streaming", "free streaming" and "purchase for download". For `GBFFP0300052` I saw Spotify, Apple Music, Deezer, TIDAL, YouTube and YouTube Music URLs. Reverse lookup by URL works: `/ws/2/url?resource=<url>&inc=recording-rels` returned the recording for a Spotify and a YouTube URL (observed).
- **Coverage sample (n=8, my test, 2026-11-22).** ISRCs taken from Deezer for 10 queries (2 hit 503, so 8 usable): Anti-Hero, MONACO, Holocene, Come Together (2009 remaster), Autobahn (2009 remaster), Kyoto, Sodade, Roygbiv. All 8 resolved to a recording. Streaming URL relations: none for 3 (including the 2022 and 2023 hits), Spotify only for 3, Spotify plus YouTube for 1, Spotify, Apple, Deezer and TIDAL for 1. Conclusion: MusicBrainz is good for ISRC-to-recording and for old or popular items, weak as a runtime link source for new releases (inference from a small sample).
- **ListenBrainz.** Same 1 call per second rule ([API docs](https://listenbrainz.readthedocs.io/en/latest/users/api/index.html)). `GET /1/metadata/lookup/` does a fuzzy artist+title to recording-MBID lookup ([docs](https://listenbrainz.readthedocs.io/en/latest/users/api/metadata.html)); the labs site lists a `spotify-id-from-metadata` dataset ([labs](https://labs.api.listenbrainz.org/)). I did not test either: **not verified** for accuracy.

## 5. Odesli / song.link

- **Status of the API.** Retired 2026-07-31. Primary source: "The public Songlink (Odesli) API retired on July 31, 2026 ... Every request to a `v1-alpha.1` endpoint now returns `410 Gone`" ([Linktree help, updated 2026-10-14](https://linktr.ee/help/en/articles/15201827)). Reason given: "Sustained high-volume automated traffic made it harder to keep the matching service behind it reliable."
- **Observed.** `https://api.song.link/v1-alpha.1/links?url=<spotify track>` returned HTTP 401 `{"statusCode":401,"code":"PUBLIC_API_ACCESS_DEPRECATED"}` on 2026-11-22. That differs from the 410 the help page promises. A SongPort blog post saw the same 401 on 2026-09-22 ([SongPort blog](https://songport.link/blog), secondary). I could not reach `api.odesli.co` from my sandbox (proxy error), so it is untested.
- **Access today.** For "Casual or personal use": "Link straight to `https://song.link/<your-url>` instead of calling the API." For integrations: "an allowlist for partners who rely on the API", via a "Request API access" form; "Developers and teams with a real, ongoing need" (same page). Whether a free hobby project qualifies is **not verified**; I did not submit the form (read-only rule).
- **Old limits (obsolete).** Without a key about 10 requests per minute, more on request ([icco/odesli README](https://raw.githubusercontent.com/icco/odesli/main/README.md), secondary, outdated).
- **The web page still resolves.** Fetching `https://song.link/https://open.spotify.com/track/3n3Ppam7vgaVa1iaRUc9Lp` returned HTTP 200 with embedded `__NEXT_DATA__` JSON: title, artist, duration, ISRC `GBFFP0300052` and per-platform links (observed: Spotify, Pandora, Deezer, Amazon Music, TIDAL, Napster, Yandex, Boomplay, Anghami; Apple Music, YouTube and YouTube Music came back empty for that track in my server-side fetch, so rendering may need JavaScript or a country). A YouTube URL returned title and artist but no ISRC (observed). Scraping this page is not an API, has no stated rate limit, and is the kind of automated traffic Linktree named as the reason for the shutdown. Terms: the Odesli Terms link on odesli.co points to a Google Drive document behind a sign-in; I could not read it. **Terms, attribution rules and commercial-use rules are not verified.**
- **Reliability signal.** A free, best-effort service was shut down within the last 4 months. Do not build on it.

## 6. YouTube

- The Data API `videos` resource has no ISRC, and no music metadata beyond title, description, channel and `licensedContent` ([videos docs](https://developers.google.com/youtube/v3/docs/videos)). `search.list` is capped at 100 per day ([quota](https://developers.google.com/youtube/v3/determine_quota_cost)).
- Keyless oEmbed returns title and channel (observed, 2026-11-22). For `m2zUrruKjDQ` (also served under `music.youtube.com`): title "Mr. Brightside", author "The Killers - Topic". For `dQw4w9WgXcQ`: "Rick Astley - Never Gonna Give You Up (Official Video) (4K Remaster)", author "Rick Astley".
- **How to match.** The Topic-channel case is clean: title is the track name, channel minus " - Topic" is the artist. For other uploads the title is free text: "(Official Video)", "(4K Remaster)", "Lyrics", "feat." and live versions pollute it. The MusicBrainz URL lookup can map a YouTube video to a recording when an editor added the link (observed to work for the Topic video above).
- **Odesli's approach.** The page-level data above shows Odesli gave the YouTube entity title and artist but no ISRC, so it matched YouTube to other services by metadata (inference from one observation; Odesli's own method is not documented in anything I could read).
- **Failure modes (inference).** Live and cover versions, remasters matched to the wrong year, uploads of mashups or fan edits, region-blocked videos, video with a different duration than the audio track (music videos with intros), and videos with no catalog equivalent at all. Use duration within a few seconds plus artist and title token match as a score, and require human confirmation below a threshold.

## 7. Other matchers (context only)

- **Songwhip: dead.** Services ceased on 2024-07-22; Sony Music acquired it ([Chris Krycho newsletter, Aug 2024](https://newsletter.music.chriskrycho.com/archive/august-2024-songwhip-is-dead/), secondary). On 2026-11-22 `https://songwhip.com/` answered 302 to `/login?redirectPath=/catalog` (observed). No public API found.
- **Soundiiz / Tune My Music.** Consumer playlist-transfer tools. Soundiiz matches by "track metadata such as the title, artist, and album" and lists unmatched tracks ([Soundiiz](https://soundiiz.com/)); it has a Playlist Import API that creates import links without a key and a User API for a paid Creator account ([Soundiiz API](https://soundiiz.com/api)). Tune My Music says it matches "by ISRC/title/artist" and I found no public developer API ([Tune My Music](https://www.tunemymusic.com/)). Neither is a song-matching API; the import link could serve as an optional "send this round's playlist to my service" exit (not tested).
- **musicapi.com (paid).** "€0.60 per 1,000 — first 5M requests", then €0.45 and €0.30; "Accounts on MusicAPI's managed credentials bill at least €500 per month; your own developer credentials have no minimum" ([pricing](https://musicapi.com/pricing)). Out of budget for a free project. Its matching claim (ISRC first, then fuzzy) is from search summaries, not verified.

## 8. Free designs

Common input: the submitter's service, a URL or a search hit. Common stored record: ISRC (when known), title, artist, duration, and a confidence flag. All three assume the project stays non-commercial and ad-free; any revenue breaks the Deezer, TIDAL and MusicBrainz free terms.

### Design A: "Deezer ISRC hub plus MusicBrainz links, human fixes the rest"

1. Get the ISRC. Deezer link: `GET /track/<id>`. Spotify or Apple link: take title, artist and duration from keyless oEmbed or iTunes Lookup, then search Deezer by artist and track, choose the closest by duration, and read its `isrc`. YouTube: Topic-channel parse as in section 6.
2. With the ISRC, call MusicBrainz `/isrc/<ISRC>?inc=url-rels` for existing Spotify, Apple, Deezer, TIDAL and YouTube URLs. Use TIDAL `filter[isrc]` if a free client-credentials app is approved.
3. For services still missing, show an "open in search" deep link and a "paste your link" box. One member's paste fills the gap for the whole league.

- **Ceiling.** MusicBrainz at 1 req/s per IP is up to about 86,000 ISRC lookups per day; Deezer at the unverified 50 per 5 s is up to about 864,000 calls per day. A league of 20 members and 20 songs per round needs under 100 calls per round. The ceiling is irrelevant at hobby scale.
- **Failure modes.** Wrong version picked from Deezer search (live, remaster); two recordings for one ISRC; MusicBrainz missing URLs for new releases (3 of 8 sampled had none); Apple and Spotify links only reached by search or by the member's paste.
- **Terms risk.** Medium-high. Deezer: possible breach of "Content database" if mappings are stored, and "games ... based on sound recordings"; MusicBrainz: fine while non-commercial. No Spotify API call, so no Spotify policy exposure. Keep calls server-side, cache only MusicBrainz data (CC0) and IDs you derived yourself, and ask Deezer in writing if it matters.

### Design B: "Metadata-only canonical record, member-resolved links" (lowest terms risk)

1. Canonical record: artist, title, duration, thumbnail via oEmbed (Spotify, YouTube) or iTunes Lookup (Apple). No ISRC required.
2. Each member opens the song in their own service through a search deep link built from artist and title. The first member on each service who finds the exact track pastes its URL; the app stores it as that service's link for the song. Later members get it.
3. Optional ISRC from MusicBrainz, if the submitter's service reveals a MusicBrainz match.

- **Ceiling.** No catalog API calls except oEmbed and iTunes (about 20 per minute, about 28,800 per day, per its doc). Effectively unlimited for a hobby league.
- **Failure modes.** Early members do friction work; wrong picks (remaster, live) unless the UI shows duration and album; links stored by members are unverified.
- **Terms risk.** Low. Public oEmbed and deep links; no stored provider catalog data beyond IDs the members supply. Spotify's "integrated with another service" rule is the one to run past a lawyer.

### Design C: "song.link page as a best-effort resolver"

1. Fetch `https://song.link/<url>` server-side, parse the embedded JSON for ISRC and per-platform links, then fall back to Design A or B when links are missing.

- **Ceiling.** Undocumented. Keep to a few calls per minute and cache results.
- **Failure modes.** The page format can change at any time (it is not an API); Apple and YouTube links were missing in my sample; a block would follow high-volume traffic, which is why the API was closed.
- **Terms risk.** High and unknown: terms unreadable, no stated permission for automated access, and the owner explicitly pointed API users to an allowlist. Use only as an optional enrichment, never as the base, unless Linktree grants allowlist access.

### Recommendation

Start with Design B for the shape of the UI, add Design A's ISRC step as an enrichment that fills links automatically, and never depend on Design C. "Bring your own service" is feasible as a promise with a confirm step. It is not feasible as fully automatic exact matching for free, because Odesli's free tier is gone, Spotify and Apple ISRC lookups need app credentials (Spotify capped at 5 users, Apple $99/year), and the free keyless sources cover only Deezer and part of MusicBrainz.

## Not verified and open questions

- **Odesli Terms** (attribution, commercial use, scraping `song.link`): the document sits behind a Google sign-in. Not read.
- **Odesli allowlist** eligibility for a free hobby project: unknown. The form was not submitted.
- **`api.odesli.co`**: unreachable from my sandbox (proxy refusal), so the 410 behaviour on that host is untested.
- **Deezer rate limit** (50 per 5 s) and the claim of an in-body quota error: from secondary sources only ([Deezer quota search results](https://github.com/sydlexius/stillwater/issues/3492)). Whether anonymous keyless use is covered by the developer terms: not clear.
- **Spotify**: whether client-credentials catalog lookups (no user) are subject to the 5-user cap; the numeric quota; that `isrc:` search returns multiple tracks per ISRC. I made no Spotify API call (no key allowed).
- **Apple Music API** rate limits and MusicKit terms: not read.
- **TIDAL**: free app registration and client-credentials access are from secondary sources; I did not call the API. Rate limits unpublished. Terms read from the portal's JS bundle, not the rendered page.
- **ISRC coverage and error rates** on streaming catalogs: no primary statistic found. The IFPI Handbook (Annex A, remasters) was downloaded but not parsed; I relied on the web guidance pages.
- **MusicBrainz coverage** is based on 8 samples. A larger sample (say 200 ISRCs from a real playlist) would give a usable hit rate.
- **MusicBrainz commercial status** if the project ever earns money: a plan tier applies (Stealth or Bronze); confirm with MetaBrainz.
- **Legal questions for a lawyer** (inherited from [research 01](../../../../research/01-market-music-league.md)): whether Spotify's "integrated with ... another service" rule reaches a project that only reads public metadata.

## Sources

Primary
- https://linktr.ee/help/en/articles/15201827 (Odesli API retirement, updated 2026-10-14)
- https://odesli.co/ and https://odesli.co/pricing (site: "all of our features are free"; no API mention)
- https://isrc.ifpi.org/en/ , /why-use-isrc/when-to-assign , /why-use-isrc/when-not-to-assign , /isrc-standard/isrc-structure , /isrc-standard/isrc-handbook
- https://www.usisrc.org/
- https://musicbrainz.org/doc/MusicBrainz_API , /MusicBrainz_API/Rate_Limiting (rev 78895) , /About/Data_License (rev 68951) , /ISRC
- https://metabrainz.org/supporters/account-type
- https://listenbrainz.readthedocs.io/en/latest/users/api/index.html , /users/api/metadata.html , https://labs.api.listenbrainz.org/
- https://developer.spotify.com/documentation/web-api/reference/search , /concepts/quota-modes , /concepts/rate-limits , /references/changes/february-2026 , /references/changes/march-2026 , https://developer.spotify.com/policy (effective 2025-05-15) , https://developer.spotify.com/terms (v10)
- https://developer.apple.com/documentation/applemusicapi/get-multiple-catalog-songs-by-isrc , /generating-developer-tokens , https://developer.apple.com/programs/ , https://performance-partners.apple.com/search-api
- https://developers.deezer.com/termsofuse (last updated 2026-10-27) , https://api.deezer.com/track/isrc:GBFFP0300052
- https://tidal-music.github.io/tidal-api-reference/tidal-api-oas.json (v1.10.258) , https://developer.tidal.com/documentation/guidelines-developer-terms (v3.0, 2024-05-06)
- https://developers.google.com/youtube/v3/docs/videos , https://developers.google.com/youtube/v3/determine_quota_cost
- https://musicapi.com/pricing , https://soundiiz.com/api , https://www.tunemymusic.com/

Observed calls (2026-11-22): `api.song.link` links endpoint (401), `song.link` pages for a Spotify and a YouTube URL, Deezer `track/isrc:` and search, MusicBrainz `isrc` and `url` lookups (User-Agent `crate-research/0.1 (research script)`, at least 1.2 s apart), iTunes Search and Lookup, YouTube and Spotify oEmbed, `songwhip.com`.

Secondary (labeled in text)
- https://songport.link/blog (post about the API retirement, 2026-09-22)
- https://raw.githubusercontent.com/icco/odesli/main/README.md
- https://newsletter.music.chriskrycho.com/archive/august-2024-songwhip-is-dead/
- https://github.com/sydlexius/stillwater/issues/3492 (Deezer limits as recalled by a user)
- Web-search summaries on TIDAL (sonovault.now/tidal-api) and musicapi.com matching: not opened directly.
