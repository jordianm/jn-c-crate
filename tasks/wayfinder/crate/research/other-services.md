# Other music services: what a small social music game can integrate

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [Which other music services are usable](../07-other-services.md)

Method note. Some developer portals are single-page apps or block bots (TIDAL docs, Bandcamp). Where the live page was unreadable I used an Internet Archive copy; its snapshot date is not shown, so only the version or effective date printed inside the document is quoted. The network path had intermittent proxy failures; every claim below comes from a page that was read, not from a failed fetch. Claims taken from a search-tool summary only are marked **not verified**.

## Answer

- **Deezer's keyless API still works and is the best catalog for search, ISRC and 30 s previews, but it is legally closed to this project.** `api.deezer.com/search` and `/track/isrc:<ISRC>` returned full JSON with no key, no login (observed 2026-11-22, details below). However, the Deezer developer terms (last updated 27 October 2026) say access is "reserved to Developers who have been expressly selected and approved", limit use to "private, personal and non-commercial" purposes, allow audio only "through the Deezer Widget", and state: "No games or businesses based on sound recordings" ([Deezer terms](https://developers.deezer.com/termsofuse)). The current Deezer wording is far stricter than the open-access wording of an older archived copy ([archived terms, undated snapshot](https://web.archive.org/web/2025/https://developers.deezer.com/termsofuse)).
- **New Deezer app registration is closed.** A Deezer community superuser wrote on 2026-06-09 that Deezer "has suspended new application creation indefinitely" ([Deezer community](https://en.deezercommunity.com/other-devices-49/impossible-de-creer-une-app-migration-spotify-vers-deezer-pour-un-projet-de-decouvert-et-jeux-musicaux-82752)); another thread (2026-05-21) says "no information on when they'll reopen registration" ([Deezer community](https://en.deezercommunity.com/features-feedback-44/app-registration-82666)). Community posts are not official statements. I could not open the portal's own message without logging in.
- **TIDAL is the one major alternative service with an open developer path and the features this game needs.** OpenAPI spec: client-credentials token for catalog, `GET /tracks?filter[isrc]=`, `GET /searchResults`, and `POST /playlists` with scope `playlists.write`, all at access tier `THIRD_PARTY` ([TIDAL OpenAPI spec](https://tidal-music.github.io/tidal-api-reference/tidal-api-oas.json)). Limits: terms allow only "non-commercial applications", apps stay "in development" with unpublished quotas, and third parties report no working route to production ([TIDAL terms v2.0](https://web.archive.org/web/2026/https://developer.tidal.com/documentation/guidelines-developer-terms-2_0), [WrzDJ issue, secondary, 2026-11-08](https://github.com/wrzonance/WrzDJ/issues/980)). Its player base is small (see market section).
- **SoundCloud reopened API registration in May 2026, but only for Artist Pro subscribers (USD 99 a year).** Public search and playback need only a client-credentials token ([register](https://developers.soundcloud.com/docs/api/register-app), [blog 2026-06-16](https://developers.soundcloud.com/blog/api-credentials-cli-openapi-github/), [price](https://soundcloud.com/getstarted/pricing/)). The catalog is user uploads, search has no ISRC filter, and the terms ban caching and bar game use without licences ([API terms, effective 30 March 2024](https://developers.soundcloud.com/docs/api/terms-of-use)).
- **Amazon Music has no usable API.** Web API v1 and v2 are in "closed Beta"; access goes through "your Amazon Business Development representative" ([Amazon v2 overview](https://developer.amazon.com/docs/music/API_web_overview_v2.html)). Only link-out is possible: `https://music.amazon.com/albums/<albumASIN>/?trackAsin=<trackASIN>` ([Amazon tracks v2](https://developer.amazon.com/docs/music/API_web_track_v2.html)).
- **Bandcamp, Qobuz, Anghami, Boomplay and JioSaavn are not options.** Bandcamp's API is for "Labels and merchandise fulfillment partners" ([Bandcamp developer page, archived](https://web.archive.org/web/2026/https://bandcamp.com/developer)); Qobuz is partner-only, Anghami's portal is "Coming soon" ([Anghami](https://docs.sdk.anghami.com/developer-portal)); the other two are covered below. Napster and Audiomack are marginal.
- **The cross-service link resolver Odesli/Songlink is gone for keyless use:** I called its endpoint and got `401 PUBLIC_API_ACCESS_DEPRECATED` on 2026-11-22.
- **Who players actually use:** Spotify first, then YouTube (Music), Apple Music and Amazon Music. Deezer is about 1% of global paid subscribers, and TIDAL and Qobuz are smaller (see market section). "Works with any service" through the API is therefore not realistic with the small services; link-out by ISRC or title is.
- **A keyless catalog as the shared search layer: not safely.** Deezer's is technically ideal and legally barred; MusicBrainz is legally open (core data CC0) and keyless, but gives identifiers and metadata only, at 1 request per second, with no previews and no search over what each streaming service has. Details in the last section.

## Deezer

**Status.** Keyless public endpoints work. Developer registration is closed (secondary evidence above). Terms were rewritten on 27 October 2026.

**Observed calls (keyless, 2026-11-22, a handful of requests).**
- `GET https://api.deezer.com/search?q=daft punk around the world&limit=2` returned HTTP 200 JSON with, per track: `id`, `title`, `isrc` (`GBDUW0600009`), `duration` (429 s), `rank`, `preview` (an MP3 URL), `link`, `artist`, `album` (with cover URLs), `readable`.
- `GET https://api.deezer.com/track/isrc:GBDUW0000059` returned the track "Harder, Better, Faster, Stronger", `duration` 226, `release_date` 2001-03-12, `available_countries` (includes `ES`, `US`, `MX`, `BR`), `contributors`. A second ISRC (`USRC17607839`) also resolved. A made-up ISRC returned `{"error":{"type":"DataException","message":"no data","code":800}}` with HTTP 200, so clients must check the body.
- Free-text search works with diacritics dropped (`rosalia malamente` found ROSALÍA's "MALAMENTE Cap.1: Augurio", ISRC `ES5021800275`). The advanced syntax `artist:"..." track:"..."` worked for ASCII names; with an accented artist name it returned 0 results in one test (`artist:"Rosalía" track:"malamente"`).
- **Previews:** the `preview` URL downloaded as a 479,827-byte MP3, consistent with a 30 s clip (inference from size). The URL is signed: its `hdnea` token contains `exp=` about 900 s after the request time (inference from comparing it with the request timestamp), so preview URLs must be fetched fresh, not stored. This matches "30s clips listening restrictions" on the [Deezer guidelines](https://developers.deezer.com/guidelines).
- No rate-limit headers were returned. A secondary source quotes "50 requests / 5 seconds" per IP with error code 4 in the body ([search summary of Deezer docs and client libraries](https://github.com/m38di/deezify)); **not verified** against Deezer's own page (the API pages require login).
- Embeds: `https://widget.deezer.com/widget/dark/track/3135556` returned 200; `https://api.deezer.com/oembed?url=...` returned 200 (not inspected further).

**Terms that bite** ([Deezer for Developers terms](https://developers.deezer.com/termsofuse), "Last updated: 27 October 2026").
- Selective access: "Access to the Services is granted on a selective basis"; Deezer "is under no obligation to grant access ... to provide reasons for refusal, or to process applications within any particular timeframe."
- Commercial: "shall not receive, generate or derive, directly or indirectly, any revenue ... (whether through subscription, advertising or other mechanisms)".
- Audio: "Access by users to sound recordings (whether excerpts or full-length sound recordings) ... is only authorised through the Deezer Widget". This excludes a custom `<audio>` player on the 30 s clip.
- Data: "No creation of Content database, no local copy."
- Games: "The Developer is not authorised to use the sound recordings that form part of the Content, in whole or in part to create games or other applications that constitute or support a separate business."
- AI: no use of Content "in connection with any artificial intelligence systems or large language models".
- The API guidelines page also says the "simple API" needs a login "to accept the terms" ([Deezer API page](https://developers.deezer.com/api)). So the keyless endpoints are probably under the same terms (inference).
- Open legal question: clause 6 is about "sound recordings"; whether metadata-only use (titles, ISRC) escapes it is unclear. A lawyer or a written answer from Deezer is needed.
- Playlist creation and user library need OAuth with an app ID, so they are unavailable without registration.

**Evidence of use.** The project's own market study lists a game that plays "30-second Deezer clips" ([01-market-music-league.md](../../../../research/01-market-music-league.md), citing [Google Play](https://play.google.com/store/apps/details?id=com.mariussty.playlistgame&hl=en_US)). Its compliance with the current terms is **not verified**.

## TIDAL

- **Programme.** Open to anyone with a TIDAL account who accepts the terms; the OpenAPI spec says tokens come from `https://auth.tidal.com/v1/oauth2/token` via client credentials (server) or authorization code with PKCE (user) ([spec](https://tidal-music.github.io/tidal-api-reference/tidal-api-oas.json)). A search-tool summary says any account can register up to ten apps; **not verified**. A tester registered an app on 2026-11-08 and saw no visible route to "Production Mode" ([WrzDJ issue](https://github.com/wrzonance/WrzDJ/issues/980), secondary).
- **Endpoints (spec, tier `THIRD_PARTY`).** `GET /tracks` with `filter[isrc]`, `countryCode`, `include`; `GET /searchResults?filter[query]=` (max 256 characters); `GET /playlists`; `POST /playlists` and `POST /playlists/{id}/relationships/items` with `playlists.write` plus `w_usr`. Track attributes include `isrc`, `duration`, `explicit`, `externalLinks`, `popularity`, `availability`. `GET /trackManifests/{id}` (tier `THIRD_PARTY`, scope `playback`) exposes `trackPresentation: FULL | PREVIEW` and `previewReason`, so previews exist but go through the playback path, not a plain MP3 URL.
- **Embed.** `embed.tidal.com` generates iframe code, with a 30 s limit according to a search summary; **not verified** (the page rendered empty). Source for the player: [tidal-music/embed-player](https://github.com/tidal-music/embed-player). Link format `https://tidal.com/track/<id>` (secondary: [embed-tidal plugin](https://github.com/bjornjohansen/embed-tidal)).
- **Terms.** I read v2.0 ("Version 2.0 as of January 15th, 2024") and v1.0 ("as of September 12th, 2023"). A v3.0 (May 2024) is reported by a third party and adds a ban on AI use; I could not read it, so **v3.0 is not verified**.
  - "You may use the Developer Tools for the sole purpose of developing and distributing non-commercial applications, websites or services".
  - Quotas: "Your Offering will remain in 'in development,' with applicable quota limits and use restrictions. To obtain a quota extension, you must submit Your Offering for formal approval". No numbers are published.
  - Caching: no "stored databases or other compilations"; local hosting only for "temporary caching of metadata and cover art".
  - Previews: "the Playbacks shall only be made available through TIDAL's SDKs, namely an official, unmodified version of the TIDAL Player module." (v2.0 URL: [terms v2.0](https://web.archive.org/web/2026/https://developer.tidal.com/documentation/guidelines-developer-terms-2_0)).
  - No clause about games in v1.0 or v2.0.
- **Fit.** Good API surface for a free, non-commercial game with a few users. Weak for growth: production approval is opaque, and non-commercial wording conflicts with ads or a subscription.

## SoundCloud

- **Status.** Reopened. "In May we opened self-service app registration for Artist Pro subscribers" ([SoundCloud blog, 2026-06-16](https://developers.soundcloud.com/blog/api-credentials-cli-openapi-github/)). "You need a SoundCloud Artist Pro subscription to register API applications" ([Get an API key](https://developers.soundcloud.com/docs/api/register-app)). Artist Pro is "$8.25 / month, billed yearly for $99" ([pricing](https://soundcloud.com/getstarted/pricing/)). Older third-party pages saying registration is closed predate this.
- **Auth and endpoints.** OAuth 2.1 with PKCE; client credentials for "public resources only (search, playback, URL resolution)"; `GET /tracks?q=` search with `access=playable` filter; playlist creation needs the authorization-code flow ([API guide](https://developers.soundcloud.com/docs/api/guide), [OpenAPI](https://raw.githubusercontent.com/soundcloud/api/master/openapi/api.yaml)). The track object has an `isrc` field, but there is no ISRC search filter in the spec.
- **Embed.** Widget API (`https://w.soundcloud.com/player/api.js`, `SC.Widget(...)` with play, pause, events) ([Widget API](https://developers.soundcloud.com/docs/api/html5-widget)). The oEmbed endpoint answered keyless: `https://soundcloud.com/oembed?format=json&url=...` returned 200 with iframe HTML (tested once). Track `access` is `playable`, `preview` or `blocked`.
- **Rate limits** ([Rate Limits](https://developers.soundcloud.com/docs/api/rate-limits)): "on the order of 100 requests per minute"; search 3,000 per hour; stream 1,500 per 24 hours; approved apps may get "up to 10×".
- **Terms** ([API Terms of Use](https://developers.soundcloud.com/docs/api/terms-of-use), "Effective Date: 30 March 2024").
  - Games: User Content may not be used "to incorporate, synchronize or use ... into any advertisement, game, video, film or other audiovisual work, or any other application, unless you've obtained all relevant licenses".
  - Caching: "must not include file-save functionality, or otherwise designed to cache, download or persistently store any User Content"; session caching only.
  - Commercial: "Only the following commercial uses are acceptable" (a short list); unacceptable includes "any app that features any advertising, sponsorship or promotion around User Content".
  - Attribution: credit the uploader and SoundCloud and link to `permalink_url`.
  - No use of content "as input to any artificial intelligence technology".
- **Fit.** The catalog is mostly independent, remix and DJ content (inference); mainstream songs players would submit are often missing. Useful only as an extra source for the long tail.

## Amazon Music

- Developer portal: "The Amazon Music Web API is currently in a closed Beta"; V2 is "in closed Beta (preview) status ... access is limited to already approved developers" ([landing](https://developer.amazon.com/docs/music/landing_home.html), [v2 overview](https://developer.amazon.com/docs/music/API_web_overview_v2.html)). The older Device API is "Deprecated".
- If access were granted: LWA auth with scope `music::catalog`; track objects carry `isrc`, `duration`, `url`, and `eligibility.isPreviewable` ([tracks v2](https://developer.amazon.com/docs/music/API_web_track_v2.html)). A preview URL form `https://music.amazon.com/getSampleTrack/<trackASIN>` appears only in a search summary; **not verified**.
- Link format (official example): `https://music.amazon.com/albums/B084KP4NBH/?trackAsin=B084KPC3Q7`; regional domains exist. Terms were not read (the Developer Services Agreement is linked from the portal; not needed given closed access).

## Bandcamp

- API: "Labels and merchandise fulfillment partners can interact with their accounts via the Bandcamp API. To register for API use, contact us" ([developer page, archived](https://web.archive.org/web/2026/https://bandcamp.com/developer)). Endpoints are account, sales report and merch orders. No catalog search or lookup for third parties.
- Terms (effective "May 07, 2026"): the Service is "provided only for your own personal, non-commercial use" ([Terms of Use, archived](https://web.archive.org/web/2026/https://bandcamp.com/terms_of_use)). I found no clause on embeds, and no embed terms page; embed rules and the oEmbed endpoint (`bandcamp.com/api/oembed`, per a [plugin disclosure](https://xerowp.com/plugins/del-embed-for-bandcamp) found by search) are **not verified**. Bandcamp's site blocked my direct requests ("Client Challenge"), so I did not call the endpoint.
- Fit: link-out or a pasted embed per submission only. No ISRC.

## Qobuz and the others (one line each)

- **Qobuz.** Partner-only; credentials by email to Qobuz; a third-party summary lists `api@qobuz.com` and the `api.json/0.2` base. Terms PDF not read. **Not verified** at a primary source. Link format `https://open.qobuz.com/track/<id>` (forum-sourced). Not usable.
- **Napster.** `developers.napster.com` is now an AI-agent platform ("Napster API ... Omniagent") ([developers.napster.com](https://developers.napster.com/docs)). An archived copy of the old music API page says "Sign up, it's free" ([archived, undated](https://web.archive.org/web/2026/https://developer.napster.com/api)); whether the old catalog API still works is **not verified**. Small user base.
- **Audiomack.** Documented REST API (OAuth 1.0a) with search, song previews (`GET /v1/music/preview/:id`) and playlist create/edit ([docs](https://audiomack.com/data-api/docs)). Getting a key is by contact form (secondary: [AudiomackSwiftLibrary](https://cocoapods.org/pods/AudiomackSwiftLibrary)); terms not found. Niche (hip-hop, Africa) catalog.
- **Anghami.** SDK exists; developer portal is "Coming soon ... contact your Anghami partnership lead" ([docs](https://docs.sdk.anghami.com/developer-portal)). Not open.
- **Boomplay.** No public programme, per a vendor with a commercial interest ([MusicAPI](https://musicapi.com/boomplay-api)); **not verified**.
- **JioSaavn.** A search summary of its API Policy ("Updated on 11.08.2026") says the API is private and no access right is granted to developers ([policy](https://www.jiosaavn.com/corporate/api-policy)); the PDF could not be read here, so **not verified**.
- **Odesli/Songlink.** `GET https://api.song.link/v1-alpha.1/links?url=...` without key returned `{"statusCode":401,"code":"PUBLIC_API_ACCESS_DEPRECATED"}` (2026-11-22). Dead as a free resolver.
- **MusicBrainz (not a streaming service).** `GET https://musicbrainz.org/ws/2/isrc/GBDUW0000059?fmt=json` returned the recording with no key. Limit: "on average 1 request per second" per IP, 503 above it ([rate limiting](https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting)). Core data is CC0; supplementary data and live-feed packets are CC BY-NC-SA 3.0 ([data licence](https://musicbrainz.org/doc/About/Data_License)).

## Market share: which services do players use

All figures are subscriber or usage estimates from the dates shown; none is a measure of this game's player base.

- **Global, end 2025 (MIDiA, via MBW 2026-06-16).** 921.6 M subscribers. Spotify 31.4%, Tencent Music 13.8%, Apple Music 12.6%, YouTube Music 12.4%, Amazon Music 8.5%. YouTube Music is "on track to overtake Apple Music and Tencent in global subscribers in 2026". Spotify "contributed 85% of net additional European subscribers in 2025" and "held its lead in the Americas and Europe" ([MBW](https://www.musicbusinessworldwide.com/the-music-industry-is-closing-in-on-a-billion-global-subscribers-with-spotify-out-in-front/), secondary to MIDiA's paywalled report; also [Music Ally 2026-06-17](https://musically.com/2026/06/17/music-business-ended-2025-with-921-6m-paid-streaming-subscribers/)).
- **Deezer (company results, via MBW 2026-07-29).** 8.9 M subscribers at 30 June 2026, of which 5.8 M direct; about 1% of MIDiA's total (inference: 8.9/921.6) ([MBW](https://www.musicbusinessworldwide.com/deezers-direct-subscribers-grow-to-5-8m-in-h1-2026-but-total-subscriber-base-falls-to-8-9m/); the primary release is at [AMF](https://echanges.dila.gouv.fr/OPENDATA/AMF/ECO/2026/07/FCECO082771_20260728.pdf), not read). France is the core market (direct subscribers: 3.9 M France, 1.9 M rest of world; search summary of the release, **not verified**).
- **TIDAL, Qobuz:** I found no sourced share. Treat both as well under Deezer in subscribers (inference).
- **US (DMN Pro, May 2025, secondary).** Spotify about 37%, Apple Music 31.5%, Amazon Music 21.6%, YouTube 7.1%, Pandora 1.8% ([Digital Music News, 2025-08-21](https://www.digitalmusicnews.com/2025/08/21/music-streaming-market-share-data-august-2025/)). DMN uses its own multipliers; MIDiA's US Apple figure differs (about 25% at end of 2024, per a secondary aggregator).
- **Spain.**
  - IAB Spain Estudio de Audio Digital 2026 (survey May 2026, 1,000 people aged 16+): among app listeners, YouTube and Spotify each 62%, Apple Music 27%, Amazon Music 24% ([PPC Land, 2026-06-13](https://ppc.land/spains-digital-audio-market-58-of-users-listen-online-podcast-leads/), secondary; these are audio apps in general, not only music; Deezer not listed in that excerpt).
  - EGM, wave published 2021-04-14 (old): 45.6% of Spaniards over 14 streamed music in the last six months; YouTube Music 21.3%; Spotify ahead of it ([MarketingNews](https://www.marketingnews.es/investigacion/noticia/1165334031605/spotify-lidera-escucha-de-musica-via-streaming-y-otros-datos-del-egm.1.html); Spotify's exact figure came from a search summary, **not verified**).
  - Promusicae (H1 2026): paid subscriptions EUR 121 M, up 15.1%, but "no breakdown by platform" ([Promusicae](https://www.promusicae.es/en/news/the-recorded-music-market-in-spain-is-consolidating-its-expansion-and-grows-116-in-the-first-half-of-2026-n684/); summarized by search tool).
- **Latin America.** Spotify leads, YouTube Music second (MIDiA via MBW; "Asia Pacific and Latin America have been vital to YouTube's growth"). A 2023 Mexico survey cited by a secondary aggregator gives YouTube Music 65%, Spotify 50%, Amazon 6%, Apple 4%, Deezer 2% of users; low confidence, **not verified** at source.
- **Reading (inference).** For players in Spain, the EU, the US and Latin America, four services cover nearly everyone: Spotify, YouTube/YouTube Music, Apple Music, Amazon Music. Deezer matters mainly in France; TIDAL and Qobuz are enthusiast niches. The services this ticket covers add little reach per integration.

## Ranking: usability for this game

"Usable" means a new, unfunded developer can start today and the terms do not obviously forbid a free social music game. Scale: High, Medium, Low, None.

| Rank | Service | Access for a new developer | Search / ISRC / preview / playlist write | Terms vs this game | Player reach | Verdict |
|---|---|---|---|---|---|---|
| 1 | TIDAL | Open (portal, dev mode) | yes / yes / via player SDK only / yes (`playlists.write`) | Non-commercial only; quotas unpublished; no game clause in v2.0 | Low | Medium: workable for a free prototype with few users |
| 2 | SoundCloud | Open since May 2026, needs Artist Pro (USD 99/yr) | yes (no ISRC filter) / `isrc` field only / widget and oEmbed / yes | Game clause needs licences; no caching; no ads | Low (indie catalog) | Low to medium: long-tail source via embed |
| 3 | Deezer | Closed for new apps; keyless reads open | yes / yes / 30 s MP3, signed, expires / no (needs OAuth) | Bars games, non-commercial, widget-only audio, no local copy | Low (France) | Low: technically best, legally barred |
| 4 | Bandcamp | Partner-only API; embeds public | no / no / embed / no | Personal non-commercial; embed terms not verified | Low | Low: link-out or embed per submission |
| 5 | Audiomack | Key by contact | yes / unknown / yes / yes | Terms not found | Low | Low: niche |
| 6 | Amazon Music | Closed beta, BD contact | n/a | Not read | Medium | None for the API; link-out only |
| 7 | Qobuz, Anghami | Partner-only | n/a | Not read | Low | None |
| 8 | Napster, Boomplay, JioSaavn | Unclear / none / forbidden | n/a | JioSaavn forbids third parties | Low | None |
| n/a | Odesli/Songlink | Keyless deprecated | link resolution only | n/a | n/a | None |
| n/a | MusicBrainz | Open, keyless | metadata and ISRC lookup only / no previews | CC0 core data; 1 req/s | n/a | Useful as a metadata layer, not a music service |

## Can a keyless catalog be the shared search layer?

Not as the sole layer, and not Deezer's without permission. Technically, Deezer's keyless API is the strongest candidate: it returns ISRC, duration, cover art and a 30 s preview in one call, and ISRC lookup works. Legally, its terms (updated 27 October 2026) require prior approval, forbid games based on sound recordings, allow audio only in Deezer's widget, and forbid building a database; app registration is closed. Using it in production would be a breach risk that Deezer can enforce by cutting access at any time ("at any time, for any reason", clause II i). The open alternative, MusicBrainz, is CC0 for core data and can be mirrored from public dumps, but it holds identifiers, not audio, previews, or per-service availability, and its public API allows 1 request per second per IP. A workable design (inference) is: store ISRC plus title and artist as the game's canonical song ID; let each player search in the service they use (Spotify, Apple Music, YouTube, each with its own embed or link); resolve other players' services by ISRC or text search at play time; use MusicBrainz only to normalise metadata. That keeps the game from depending on any one catalog and on terms that forbid games. Whether linking by ISRC to a service's public song page needs that service's API terms is a legal question for the final design.

## Not verified and open questions

- Deezer: whether registration truly remains closed on the portal itself (login needed); the exact rate limit on Deezer's own page; whether metadata-only use of the keyless API is allowed under clause III.6; whether the keyless calls are bound by the terms.
- TIDAL: terms v3.0 (May 2024) and its AI ban; the embed's 30 s limit and iframe format; the ten-app limit; quota numbers; how production approval works (third parties say it is unanswered since Nov 2025).
- SoundCloud: whether non-Artist-Pro keys exist; how often tracks carry a filled `isrc`; whether a free game with no ads is "acceptable" under the commercial list.
- Amazon: preview URL form; the Amazon Music program requirements and developer agreement were not read.
- Bandcamp: embed terms and oEmbed; Qobuz API terms PDF; Napster legacy API status; Audiomack terms and key process; JioSaavn policy text; Boomplay.
- Market share: no primary Spain or Latin America platform split; TIDAL and Qobuz subscriber counts; MIDiA's report is paywalled, so figures come through press coverage.
- Question for the owner (decision, not research): is the first version non-commercial and free of ads, so TIDAL's and Deezer's non-commercial terms can be met? Recommendation: assume yes for the prototype, and do not build on Deezer without a written reply from Deezer.

## Sources

Primary:
- Deezer terms: https://developers.deezer.com/termsofuse (last updated 27 October 2026)
- Deezer guidelines: https://developers.deezer.com/guidelines
- Deezer API (login wall): https://developers.deezer.com/api
- Deezer keyless API calls: https://api.deezer.com/search, https://api.deezer.com/track/isrc:GBDUW0000059 (observed 2026-11-22)
- Deezer older terms (archive): https://web.archive.org/web/2025/https://developers.deezer.com/termsofuse
- TIDAL OpenAPI spec (v1.10.258): https://tidal-music.github.io/tidal-api-reference/tidal-api-oas.json
- TIDAL terms v2.0 (archive): https://web.archive.org/web/2026/https://developer.tidal.com/documentation/guidelines-developer-terms-2_0
- TIDAL terms v1.0 (archive): https://web.archive.org/web/2026/https://developer.tidal.com/documentation/guidelines-developer-terms-1_0
- TIDAL embed player source: https://github.com/tidal-music/embed-player
- SoundCloud: https://developers.soundcloud.com/docs/api/register-app, https://developers.soundcloud.com/docs/api/guide, https://developers.soundcloud.com/docs/api/rate-limits, https://developers.soundcloud.com/docs/api/terms-of-use, https://developers.soundcloud.com/docs/api/html5-widget, https://developers.soundcloud.com/blog/api-credentials-cli-openapi-github/, https://raw.githubusercontent.com/soundcloud/api/master/openapi/api.yaml, https://soundcloud.com/getstarted/pricing/
- Amazon Music: https://developer.amazon.com/docs/music/landing_home.html, https://developer.amazon.com/docs/music/API_web_overview_v2.html, https://developer.amazon.com/docs/music/API_web_track_v2.html
- Bandcamp (archive): https://web.archive.org/web/2026/https://bandcamp.com/developer, https://web.archive.org/web/2026/https://bandcamp.com/terms_of_use
- Anghami: https://docs.sdk.anghami.com/developer-portal
- Audiomack: https://audiomack.com/data-api/docs
- Napster: https://developers.napster.com/docs, https://web.archive.org/web/2026/https://developer.napster.com/api
- JioSaavn: https://www.jiosaavn.com/corporate/api-policy
- MusicBrainz: https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting, https://musicbrainz.org/doc/About/Data_License
- Promusicae: https://www.promusicae.es/en/news/the-recorded-music-market-in-spain-is-consolidating-its-expansion-and-grows-116-in-the-first-half-of-2026-n684/
- Odesli: https://api.song.link/v1-alpha.1/links (call result)

Secondary (articles, community posts, third-party summaries):
- Deezer community, 2026-06-09: https://en.deezercommunity.com/other-devices-49/impossible-de-creer-une-app-migration-spotify-vers-deezer-pour-un-projet-de-decouvert-et-jeux-musicaux-82752
- Deezer community, 2026-05-21: https://en.deezercommunity.com/features-feedback-44/app-registration-82666
- Macamp issue, 2026-09-25: https://github.com/holgerkrupp/Macamp/issues/18
- WrzDJ issue, 2026-11-08: https://github.com/wrzonance/WrzDJ/issues/980
- MBW on MIDiA, 2026-06-16: https://www.musicbusinessworldwide.com/the-music-industry-is-closing-in-on-a-billion-global-subscribers-with-spotify-out-in-front/
- Music Ally, 2026-06-17: https://musically.com/2026/06/17/music-business-ended-2025-with-921-6m-paid-streaming-subscribers/
- MBW on Deezer H1 2026, 2026-07-29: https://www.musicbusinessworldwide.com/deezers-direct-subscribers-grow-to-5-8m-in-h1-2026-but-total-subscriber-base-falls-to-8-9m/
- Deezer H1 release (not read): https://echanges.dila.gouv.fr/OPENDATA/AMF/ECO/2026/07/FCECO082771_20260728.pdf
- Digital Music News, 2025-08-21: https://www.digitalmusicnews.com/2025/08/21/music-streaming-market-share-data-august-2025/
- PPC Land on IAB Spain, 2026-06-13: https://ppc.land/spains-digital-audio-market-58-of-users-listen-online-podcast-leads/
- MarketingNews on EGM, 2021-04-14: https://www.marketingnews.es/investigacion/noticia/1165334031605/spotify-lidera-escucha-de-musica-via-streaming-y-otros-datos-del-egm.1.html
- deezify README (rate limit): https://github.com/m38di/deezify
- Plugins and aggregators: https://github.com/bjornjohansen/embed-tidal, https://xerowp.com/plugins/del-embed-for-bandcamp, https://musicapi.com/boomplay-api, https://cocoapods.org/pods/AudiomackSwiftLibrary
- Project study: /workspace/AI Projects/JN C Crate/research/01-market-music-league.md
