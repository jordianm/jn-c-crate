# What a new game can do with Spotify (late 2026)

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [What a new game can do with Spotify](../04-spotify-access.md)

Method note: primary pages were fetched as raw HTML or read through WebFetch. Policy text below is quoted from the fetched page. Anything from forums, news or app-store listings is labeled secondary. I made no logins, no app registration, and no authenticated API calls, so any statement about what the live API returns to a new app is documentation-based, not tested.

## Answer

- **The Developer Policy forbids games, flatly.** Section III: "Do not create a game, including trivia quizzes." The Compliance Tips go wider: "Games or trivia quizzes: Incorporating Spotify into any gaming or quiz functionality." The policy has no approval route and no mention of contests. Policy effective 15 May 2025. [Policy](https://developer.spotify.com/policy), [Compliance Tips](https://developer.spotify.com/compliance-tips)
- **Embeds have their own, older rule with a written-approval carve-out.** Widget Terms (v2.0, effective 27 May 2014) IV.2.d: "Unless you receive Spotify's written approval, you may not use the Spotify Platform to incorporate Spotify Content into any game functionality (including trivia quizzes)." Study 01 did not consider this document. Whether a pasted-link-plus-embed league is "game functionality" is a legal question. [Widget Terms](https://developer.spotify.com/documentation/embeds/terms)
- **Development Mode cannot carry a product.** It is for "personal projects for non-commercial use by individual developers": app owner needs Premium, up to 5 authenticated users per Client ID, a reduced endpoint set. Extended quota needs a registered organization with a launched service and at least 250k MAU, and Spotify reviews the app "for compliance with our Developer Policy", so the game ban applies there too. [Feb 2026 post](https://developer.spotify.com/blog/2026-02-06-update-on-developer-access-and-platform-security), [Quota modes](https://developer.spotify.com/documentation/web-api/concepts/quota-modes)
- **The Web API pieces a league needs still exist in Development Mode:** search (max 10 results per page), single-track get (with `external_ids.isrc`), `POST /me/playlists`, `POST /playlists/{id}/items` (100 per request), scopes `playlist-modify-public` and `playlist-modify-private`. But each user has to authorize, and refresh tokens now expire after 6 months. [Migration guide](https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide), [Search](https://developer.spotify.com/documentation/web-api/reference/search), [Add items](https://developer.spotify.com/documentation/web-api/reference/add-items-to-playlist), [Refresh token post](https://developer.spotify.com/blog/2026-06-18-refresh-token-expiration)
- **No Web API app is needed for embeds, oEmbed, `open.spotify.com` links or `spotify:` URIs.** The oEmbed endpoint answered without a key (observed 2026-11-22). It returns title and thumbnail, not the artist. Playback in an embed is full-track only for a logged-in listener in a supported browser; otherwise a preview of under 30 seconds. Previews are the fallback, per Spotify's troubleshooting page. [oEmbed reference](https://developer.spotify.com/documentation/embeds/reference/oembed), [Troubleshooting](https://developer.spotify.com/documentation/embeds/tutorials/troubleshooting)
- **Spotify's docs set no limit on embeds per page.** The iFrame API is documented for "a single Embed or ... multiple Embeds in the same web app". One controller can switch songs with `loadEntity`. [iFrame API tutorial](https://developer.spotify.com/documentation/embeds/tutorials/using-the-iframe-api)
- **The Web Playback SDK is for Premium listeners only, uses the `streaming` scope, and makes the app a "Streaming SDA".** A Streaming SDA may not sell access, show ads, or take payments. [Policy IV](https://developer.spotify.com/policy), [SDK docs](https://developer.spotify.com/documentation/web-playback-sdk)
- **Competitors differ, and none shows a quota status.** DJ League's policy says song search and playlist creation run through "a system-level Spotify integration" (one operator-owned account). BandJam's privacy policy lists Apple Music or Spotify tokens used "to play previews". YapZap's store listing claims full in-app Spotify playback. All three are exposed to the same policy text; I found no evidence of an agreement with Spotify for any of them.
- **Net for a new entrant (inference):** Spotify cannot be a dependency. The Web API route is closed to a commercial game (Development Mode is non-commercial and capped at 5 users; extended quota is out of reach). The links-and-embeds route has no technical block but carries an unresolved legal risk from the Widget Terms games clause. Details in the options table.

## Documents and versions

| Document | Version or date shown | URL |
|---|---|---|
| Developer Terms | "Version 10, effective as of 15 May, 2025" | https://developer.spotify.com/terms |
| Developer Policy | "Effective as of 15 May, 2025" | https://developer.spotify.com/policy |
| Compliance Tips | no date or version on the page | https://developer.spotify.com/compliance-tips |
| Widget Terms of Use (this is the Embeds terms page) | "Version 2.0. Effective as of 27 May 2014." | https://developer.spotify.com/documentation/embeds/terms |
| Design Guidelines | no date or version on the page | https://developer.spotify.com/documentation/design |
| Quota modes | no date; text names the 250k MAU criterion | https://developer.spotify.com/documentation/web-api/concepts/quota-modes |

The Developer Terms list the Developer Policy, Terms and Conditions of Use and Branding Guidelines as parts of the agreement. The Widget Terms say that using other developer tools puts you under the Developer Terms instead.

## 1. Policy and terms: exact text

All quotes from [Policy](https://developer.spotify.com/policy) unless stated.

**Games and quizzes.** "Do not create a game, including trivia quizzes." Compliance Tips example: "a 'name that tune' quiz would not be allowed" ([Compliance Tips](https://developer.spotify.com/compliance-tips)). Music League is not a name-that-tune quiz, but "Incorporating Spotify into any gaming or quiz functionality" is a broad wording. Whether a themed song-submission and voting league is a "game" is **not verified**: no Spotify text says. Community posts asking how Hitster-type apps comply, or how to get written approval for a game, have no replies ([post 1](https://community.spotify.com/t5/Spotify-for-Developers/Approval-for-a-Game-Using-Spotify-Web-Playback-SDK/td-p/7089786), [post 2](https://community.spotify.com/t5/Spotify-for-Developers/Getting-written-permission-to-use-embeds-in-a-game/m-p/6953516); secondary).

**Contests.** The policy, terms and tips do not use the word. (Checked by text search; the only "contest" hits are the verb "contest the validity" of trademarks.)

**Combining with other services.** "Do not create any product or service which is integrated with streams or content from another service." The Widget Terms say the same for Widgets (IV.2.f). A league that matches a song across Spotify, Apple Music and YouTube is exposed to this on its face (inference). The Design Guidelines add that platforms aggregating several providers "must give Spotify fair treatment - anything made available to all other partners must be available to Spotify" ([Design](https://developer.spotify.com/documentation/design)).

**Other prohibitions that touch a league game:**
- "Do not analyze the Spotify Content or the Spotify Service for any purpose, including ... usage statistics, user metrics, or building profiles of users." Taste stats built on Spotify data would hit this (inference). Vote counts are not Spotify content (inference).
- "Do not build products or services that mimic, or replicate or attempt to replace a core user experience of Spotify ... Your product or service must add independent value or functionality that improves users' interactions with Spotify."
- "Do not use the Spotify Platform or any Spotify Content to train a machine learning or AI model." (Also Developer Terms IV.)
- "Do not build an SDA that enables the transfer of data to another service, except ... the metadata of the user's playlists."
- "Do not build products and services which are targeted to children."

**Streaming and commercial use (Policy IV).**
- "Streaming of music sound recordings through the Spotify Platform shall only be made available to subscribers to the Premium Spotify Service."
- Widgets and Audio Preview Clips "may be made available to Spotify users who do not subscribe to the Premium service".
- Streaming SDAs: commercial uses are not permitted: no sale, "e-commerce ... initiated via a Streaming SDA", or "advertising, sponsorships, or promotions on the Streaming SDA itself".
- Non-Streaming SDAs: "the sale of advertising, sponsorships, or promotions" and "the sale of, or sale of access to, a Non-Streaming SDA" are the only permitted commercial uses.
- Developer Terms definitions: "Streaming" means "using the Spotify Platform to enable playback of sound recordings ... including using the Spotify Platform to control a background Spotify application"; "the use of (i) Widgets or (ii) Audio Preview Clips, are not included in the definition of Streaming". Compliance Tips list the Web Playback SDK, `/v1/me/player/play`, and the iOS/Android SDKs as streaming. ([Terms](https://developer.spotify.com/terms), [Compliance Tips](https://developer.spotify.com/compliance-tips))

**License scope.** Developer Terms III.1: Spotify grants a right to build SDAs "(i) for private personal use; and (ii) on Approved Devices; and (iii) in accordance with the Developer Policy." Read literally, "private personal use" sits uneasily with a public multi-user product. How Spotify applies it is **not verified** (question for Spotify).

**Caching and storage (Developer Terms IV).** "you may not store, aggregate or create compilations or databases of Spotify Content, other than as strictly necessary to operate your SDA ... Do not store Spotify Content indefinitely." Local caching is limited to "temporary caching of: metadata and cover art" or Premium-only conditional downloads. "Spotify Content" includes "metadata, playlists, and user data". A permanent league archive of titles, artists and art is in tension with this (inference). Widget Terms: "You may not use a Widget to locally cache any Spotify Content."

**Scraping and ripping.** Developer Terms IV: no "robot, spider, site search/retrieval application ... to retrieve, duplicate, or index any portion of the Spotify Service or Spotify Content (which includes playlist data)", and nothing that enables "stream ripping".

**Attribution and branding.** Policy II: displayed content must be "clearly attribute[d] ... by using the Spotify Marks"; "Metadata, cover art and Audio Preview Clips must be accompanied by a link back"; metadata and cover art must be shown whenever you play Spotify content in a Streaming SDA. Policy VI: the app name "should not begin with 'Spot' or be confusing in sound or spelling to Spotify". Design Guidelines: do not crop artwork or put your logo over it; link text must be one of "OPEN SPOTIFY, PLAY ON SPOTIFY or LISTEN ON SPOTIFY" when the Spotify app is installed. ([Design](https://developer.spotify.com/documentation/design))

**Data and users (Policy I, Terms V).** Privacy policy and end-user agreement are mandatory; a disconnect mechanism is mandatory; on disconnect, delete that user's Spotify personal data; no emailing users without consent; US DMCA safe-harbor steps for user-submitted content. These apply to any Web API app.

**Preview clips (Policy V).** "Audio Preview Clips may only be used to promote the underlying content and not for personalization or messaging products", must link back, and may not be a standalone product.

## 2. Quota modes and the application process

Source: [Quota modes](https://developer.spotify.com/documentation/web-api/concepts/quota-modes) unless stated.

**Development Mode today (after Feb 2026).**
- New Client IDs have been under the new rules since 2026-02-11; existing integrations since 2026-03-09. Postponed on 2026-03-09 for existing integrations: only the endpoint changes. Premium requirement, user cap and Client ID limit took effect as planned ([blog update](https://developer.spotify.com/blog/2026-02-06-update-on-developer-access-and-platform-security)).
- Requirements: "Development Mode use will require a Spotify Premium account"; "Each Client ID will be limited to up to five authorized users"; "API access will be limited to a smaller set of supported endpoints." Intended for "learning, experimentation, and personal projects for non-commercial use by individual developers" and "should not be relied on as a foundation for building or scaling a business on Spotify."
- Premium lapse: "If the owner's Premium subscription lapses, the app will stop working" ([migration guide](https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide)).
- Each extra user must be on the app's allowlist (name and Spotify email entered by the owner). A non-allowlisted user can log in, but API calls with their token return 403.
- July 2026: Client IDs per developer raised from 1 to 25, and quota is now counted per developer account ("they will share the same quota buckets"). Exceeded quota returns 429 with `"reason": "QUOTA_EXCEEDED"` ([July 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/july-2026)). The quota numbers are not published: "The specific groupings and limits are subject to change."
- Rate limit is a "rolling 30 second window", lower for Development Mode ([Rate limits](https://developer.spotify.com/documentation/web-api/concepts/rate-limits)); the exact number is not on the page.

**Extended quota.** Apps in this mode have no allowlist and "a higher rate limit". Criteria on the page (and in the [2025-04-15 post](https://developer.spotify.com/blog/2025-04-15-updating-the-criteria-for-web-api-extended-access)):
- "as of May 15th 2025, Spotify only accepts applications from organizations (not individuals)", sent "through a company email by using this form";
- "Established Business Entity (legally registered business or organisation)"; "Operating an active, and Launched Service"; "at least 250k MAUs"; "Being available in key Spotify markets"; "Commercial Viability"; "Adherence to Terms".
- The 2025-04-15 post says extended access is "reserved for apps with established, scalable, and impactful use cases that help drive our platform strategy ... and promote artists and creator discovery", and that "over 95%" of past applications "fall short of basic security, privacy, and licensing standards". Previously approved, active apps "remain unaffected".
- Process: approved partner form first, then in the dashboard the app is evaluated "for compliance with our Developer Policy"; "This review process can take up to six weeks." Policy VII: "Spotify makes no guarantees or promises on processing times, or that such extended access request will be approved."
- Extended quota is granted for "only the use case that Spotify reviewed".
- Extended-quota apps are not affected by the Feb 2026 migration: "all existing endpoints, fields, and behaviors remain unchanged" ([migration guide](https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide)). Any incumbent with legacy extended access (Music League's status is **not verified**) keeps the old API surface; a new entrant does not.

**Changelog coverage.** Changelogs found: February, March, May and July 2026. The newest listed is July 2026. May 2026 only adds `account_id` to `GET /me`. The blog index page could not be fetched (404), and a web search found no later announcement, so a post after July 2026 cannot be fully excluded.

## 3. Web API endpoints a league would use

| Need | Endpoint and status for a new app | Source |
|---|---|---|
| Search a song | `GET /search`; `limit` "Range: 0 - 10", default 5 (was 50 and 20); `offset` range 0 to 1000; supports `isrc:` and `track:` filters | [Search](https://developer.spotify.com/documentation/web-api/reference/search), [Feb 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/february-2026) |
| Get a track | `GET /tracks/{id}` only. The multi-get `GET /tracks` is removed. `external_ids` (`isrc`, `ean`, `upc`) was removed in February and "[REVERTED]" in March 2026. `popularity`, `available_markets`, `linked_from` are gone. | [Feb changelog](https://developer.spotify.com/documentation/web-api/references/changes/february-2026), [Mar changelog](https://developer.spotify.com/documentation/web-api/references/changes/march-2026), [Get Track](https://developer.spotify.com/documentation/web-api/reference/get-track) |
| Create playlist | `POST /me/playlists` ("Each user is generally limited to a maximum of 11000 playlists"). `POST /users/{user_id}/playlists` is removed. Scopes `playlist-modify-public`, `playlist-modify-private`; collaborative playlists need both and `public:false`. | [Create Playlist](https://developer.spotify.com/documentation/web-api/reference/create-playlist) |
| Add songs | `POST /playlists/{id}/items` (the `/tracks` path is removed); "A maximum of 100 items can be added in one request." | [Add items](https://developer.spotify.com/documentation/web-api/reference/add-items-to-playlist) |
| Read a playlist | `GET /playlists/{id}/items` returns contents "only for playlists the user owns or collaborates on". `GET /users/{id}/playlists` removed. | [Migration guide](https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide) |
| Other users | `GET /users/{id}` removed; only `GET /me` | same |
| Player control | `/me/player/*` endpoints remain (Premium, streaming) | [Feb changelog](https://developer.spotify.com/documentation/web-api/references/changes/february-2026) |

**Removed for new apps since 2024-11-27:** Related Artists, Recommendations, Audio Features, Audio Analysis, Get Featured Playlists, Get Category's Playlists, "30-second preview URLs, in multi-get responses (SimpleTrack object)", and "Algorithmic and Spotify-owned editorial playlists". Applies to "New apps that are registered on or after today's date" and Development Mode apps without a pending extension. ([2024-11-27 post](https://developer.spotify.com/blog/2024-11-27-changes-to-the-web-api)). Also removed in Feb 2026: browse/new-releases, categories, artist top-tracks, markets, batch fetches. Search without a user token: the Search reference describes `market` handling; Client Credentials is documented as an auth flow ([quota page nav](https://developer.spotify.com/documentation/web-api/concepts/quota-modes)); whether a Development Mode app can call search with it is **not verified**.

**`preview_url`.** The current Get Track and Search references still document `preview_url`: "A link to a 30 second preview (MP3 format) of the track. Can be null", with the note that preview clips "may not be offered as a standalone service". The official 2024 post names only multi-get responses. Community threads report it null for all tracks, including single GET and search (secondary; [thread](https://community.spotify.com/t5/Spotify-for-Developers/Preview-URLs-MP3-no-longer-exist-all-tracks/m-p/6712864), no staff reply in the capture). **Not verified by an actual call.** Plan on it being null.

**Auth and scopes for a league.**
- Playlist creation: `playlist-modify-private` and/or `playlist-modify-public` ([Scopes](https://developer.spotify.com/documentation/web-api/concepts/scopes)). The Compliance Tips advise requesting only needed scopes and note "Sometimes, using the API is not the best way to deliver a product feature. Consider alternatives — like linking to a playlist in Spotify".
- `streaming`: "Control playback of a Spotify track. This scope is currently available to the Web Playback SDK. The user must have a Spotify Premium account."
- Refresh tokens: 6-month life measured from the user's original authorization; refreshing does not extend it; expired tokens return `invalid_grant`. New apps affected from 2026-06-18, existing from 2026-07-20; Client Credentials unaffected ([post](https://developer.spotify.com/blog/2026-06-18-refresh-token-expiration)). For a league lasting weeks this is a minor issue; for a season-long account link it means a re-login (inference).
- User identity: use `account_id` (added May 2026), not `id`, to link accounts ([May 2026 changelog](https://developer.spotify.com/documentation/web-api/references/changes/may-2026)).

## 4. What needs no Web API app

**Embeds.** Three ways to get an embed: copy the HTML from the Spotify client, the iFrame API, or the oEmbed API. The Embeds landing page says using Embeds means accepting the terms (link to the developer terms) and lists a separate "Terms of Use" page, which is the Widget Terms above ([Embeds](https://developer.spotify.com/documentation/embeds)). You can embed a "podcast, episode, track, playlist, artist, or album"; a track embed is `https://open.spotify.com/embed/track/<id>` in an iframe with `allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"` and `loading="lazy"`; the compact layout is for a single track; "Spotify handles the available playback experience ... for the listener and their context" ([Creating an Embed](https://developer.spotify.com/documentation/embeds/tutorials/creating-an-embed)).

**oEmbed** (observed 2026-11-22; two calls, no key, no login). `GET https://open.spotify.com/oembed?url=<open.spotify.com link or spotify: URI>` returned JSON with `html` (a ready iframe), `iframe_url`, `width` 456, `height` 152, `version`, `provider_name`, `provider_url`, `type: "rich"`, `title` (track name only), and `thumbnail_url` (300x300). There is no artist field. Both an `https://open.spotify.com/track/...` URL and a `spotify:track:...` URI worked. The response carries `access-control-allow-origin: *`. So a site can show title and cover from a pasted link with no developer app, but not artist name or ISRC. (Reference: [oEmbed](https://developer.spotify.com/documentation/embeds/reference/oembed).) The oEmbed output is "metadata and cover art", so the caching limits above apply (inference).

**What the embed plays.** Spotify's primary pages say only that "In some situations the Embed will only stream a preview clip of less than 30 seconds", and that removing `encrypted-media` from the iframe leaves only previews; they do not describe per-account behavior ([Troubleshooting](https://developer.spotify.com/documentation/embeds/tutorials/troubleshooting), [Creating an Embed](https://developer.spotify.com/documentation/embeds/tutorials/creating-an-embed)). Policy IV supports the split: full streaming is Premium-only, widgets and previews may go to non-Premium users. The rest is community experience (secondary):
- logged-out visitors get a 30-second preview and a sign-in prompt;
- full tracks only for a logged-in Spotify user (Premium), mostly desktop browsers with third-party cookies allowed; mobile and Safari often stay on previews; the decision is made at load, so the embed needs a reload after login ([community thread](https://community.spotify.com/t5/Spotify-for-Developers/Only-showing-preview/td-p/5485141), [GitHub PR](https://github.com/TheKaoser/classical-portal/pull/88)).
- A Spotify Free listener gets the preview, per the Policy split; what Free listeners get in practice inside an embed is **not verified** from a primary source.

One public embed page for a track (fetched once) ships `isPlayable` and an `audioPreview` URL in its page data, which fits "preview is the fallback". Using that URL outside the embed would be scraping and probably breaches Developer Terms IV and Widget Terms IV.1.g (inference). Do not build on it.

**Many embeds on one page.** No documented limit ([Creating an Embed](https://developer.spotify.com/documentation/embeds/tutorials/creating-an-embed); no limit stated). The iFrame API is built for "a single Embed or ... multiple Embeds in the same web app", with `createController`, `loadEntity` (URI or full URL), `togglePlay`, `destroy`, and events `ready`, `playback_started`, `playback_update` (position, duration, isPaused) ([iFrame API reference](https://developer.spotify.com/documentation/embeds/references/iframe-api)). A round with 10 to 20 songs could use one iframe per song loaded lazily, or one controller with `loadEntity` (inference: far fewer iframes; each iframe loads a full page of about 10 KB HTML plus scripts). Performance with 20+ live iframes was not tested.

**Links and URIs.** Spotify URI and ID formats are documented ([URIs and IDs](https://developer.spotify.com/documentation/web-api/concepts/spotify-uris-ids)). I found no Spotify document that restricts putting a plain `open.spotify.com` hyperlink on a site or in an app. That is not a finding that it is permitted; it is **not verified** and is a legal question. Spotify's own guidance is to link users to Spotify ("always link to the Spotify app"; [Design](https://developer.spotify.com/documentation/design)).

**Embed terms (Widget Terms, v2.0, 2014).** Relevant clauses:
- III.1.a: Widgets only "on any website or webpage controlled by you".
- IV.2.d: games and trivia quizzes need Spotify's written approval (quoted in the Answer). No process for requesting it is documented; the one community post asking has no reply.
- IV.2.f: no integration with "(ii) streams from another service".
- IV.1.f: "Do not use the Spotify Platform ... to build products or services that compete with the Spotify Service ... without our permission."
- IV.3.a-b: show the widget unaltered; do not "obfuscate" it, "whether by banner advertisements or by any other means".
- IV.3.e: "the Spotify Play Button may not be used for commercial purposes. This restriction does not prohibit you from embedding the Spotify Play Button on Websites that contain advertising." Whether a paid subscription is "commercial purposes" is **not verified**.
- IV.3.c: "You may not collect or store personal information about Spotify users such as a name, user ID, or password."
- Spotify places cookies on visitors' browsers; you must disclose this in your privacy policy (Section III and V).
- "Spotify Widget" in these terms means "the Spotify Play Button (or iteration thereof) and the Spotify Follow Button". Whether the iframe Embed and the iFrame API count as an "iteration" is **not verified**; the Developer Terms use the same list ("including the Spotify Play Button (or any iteration thereof)") and exclude Widgets from "SDA" and "Streaming".

## 5. Web Playback SDK

- "The Web Playback SDK requires a Spotify Premium subscription (mobile only types of premium subscriptions are excluded)." Works in Chrome, Firefox, Safari and Edge on desktop and mobile, with iOS limits (playback does not start automatically after a transfer) ([SDK](https://developer.spotify.com/documentation/web-playback-sdk)).
- Needs an OAuth token with the `streaming` scope, valid for a Premium user; the SDK reference says "You will need to execute this with a valid access_token string for a Spotify Premium user", and the SDK reports an error for users without Premium ([reference](https://developer.spotify.com/documentation/web-playback-sdk/reference)). Tokens last up to 60 minutes.
- The reference banner reads: "Streaming applications may not be commercial. The Spotify Platform can not be used to develop commercial streaming integrations."
- It is a Streaming SDA: no sales, ads or payments. It also needs a Client ID, so it counts against Development Mode's 5 users unless you have extended quota ([Quota modes](https://developer.spotify.com/documentation/web-api/concepts/quota-modes)).
- A Free listener would get nothing from it. This breaks the "everyone listens" premise of a social league (inference).

## 6. How competitors integrate Spotify

Evidence is from their own pages; their quota status is **not verified** for all three (the quota status is not public).

| Product | What the evidence says | Source |
|---|---|---|
| Music League (incumbent, for reference) | Search Spotify's catalog in-app, or "paste a track link from Spotify". "The first player in the league to tap Generate on the round page creates the playlist" (not added automatically). For Free users, "Music League automatically adds a 30-second preview track alongside" songs not playable on Free. Its privacy policy (updated 2025-01-21) does not mention Spotify. | [How to play](https://next.musicleague.com/support/how-to-play), [privacy](https://musicleague.com/privacy/) |
| DJ League | Home page: a shared playlist is generated, players vote. In its privacy text (a client-rendered page; wording read from the site's JavaScript bundle): "When you search for songs, we retrieve track metadata from Spotify's API on your behalf. We do not access your personal Spotify account, listening history, or playlists. All song searches and playlist creation are performed through a system-level Spotify integration." The same text says "If you connect your Spotify account, we access only the data required to search for songs and create playlists." The bundle also contains an admin screen that connects one operator "System Spotify account" via OAuth, plus similar Apple and YouTube "system" accounts. Reading: the operator owns the playlist account, so no per-player OAuth is needed for playlist creation (inference). Whether the app is in Development Mode or has extended quota is not stated; the policy bans games either way. | [djleague.app](https://djleague.app/) and its script bundle |
| BandJam | Privacy policy (last updated 2026-05-08): "Music services (optional): Apple Music or Spotify tokens/IDs used to play previews" and "Tokens are used only to play previews and associate tracks with submissions"; YouTube API Services are used "to create and link YouTube Music playlists". The terms say users can create playlists "using third-party music streaming services (e.g., Apple Music, Spotify)". The ticket brief said BandJam uses pasted links only. The policy shows it also holds Spotify tokens, so it is not links-only (how those tokens are obtained, Web API or iOS SDK, is not stated). | [Privacy](https://bandjam.app/privacy.html), [Terms](https://bandjam.app/terms.html) |
| YapZap | App Store listing (secondary): "Spotify with full in-app playback", works with "Spotify, Apple Music, YouTube Music, TIDAL, Amazon Music, or Deezer", "We automatically find every song across all platforms". Full in-app Spotify playback would mean the Web Playback SDK or the mobile SDK, i.e. a Streaming SDA (inference). Its privacy page is client-rendered and returned no text. | [App Store](https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650) |

Takeaway (inference): three small entrants run in the open on Spotify despite the policy text. None has shown an agreement. That is evidence of tolerance, not of permission, and it can end by enforcement: Spotify states that it reviews applications "from time to time" and may take action "including suspension, disabling your application or permanently revoking your access to the Spotify Platform" ([Compliance Tips](https://developer.spotify.com/compliance-tips)).

## 7. Options for a new entrant

| Option | Allows | Forbids or limits | Risk |
|---|---|---|---|
| **(a) Web API, Development Mode** | Search (10 per page), get track with ISRC, create playlist and add songs for allowlisted users. | 5 users per Client ID; owner needs Premium; "non-commercial use by individual developers"; endpoint set reduced; game ban applies; quota unpublished. | Not a launch path. Fine for an internal prototype to test flows. Account loss if Spotify finds a game in production. |
| **(b) Links and embeds only (no developer app)** | Players paste `open.spotify.com` links; site shows title and cover (oEmbed) and plays via embed (full track for logged-in Premium on supported browsers, otherwise preview). No OAuth, no quota, no user cap. | No artist or ISRC from oEmbed. Widget Terms: games need written approval; multi-service integration clause; no obscuring the widget; no caching; cookie disclosure; "Play Button may not be used for commercial purposes". Preview-only for many listeners. | Medium to high legal risk, low technical risk. The games clause is the issue; asking Spotify for written approval is the documented route but has no process. |
| **(c) Players create the round playlist from a list of links** | Site shows the round's songs as `open.spotify.com` / `spotify:` links; each player builds the playlist in Spotify. The organizer can instead create a collaborative playlist and ask players to add their songs (the Web API reference confirms collaborative playlists exist; the in-app flow was not checked). | Manual work per player; breaks anonymity if Spotify shows who added each song (**not verified**); no automation, no Premium gating of metadata. | Low technical risk. Legal risk is the lowest of the Spotify-touching options, since the app uses no Spotify Platform. Needs a lawyer to confirm. Worse product than Music League. |
| **(d) Apply for extended quota later** | Unlimited users, higher rate limit, same endpoints as (a), previously approved apps' old surface not included. | Needs a registered organization, launched service, 250k MAU, key markets, "Commercial Viability". Review up to 6 weeks, no promise. Game ban applies in review. Approved only "for the use case that Spotify reviewed". | Not reachable at launch. Even with 250k MAU, approval is not likely for a game (inference). Do not plan on it. |
| **(e) Web Playback SDK** | Full in-app playback for Premium users. | Premium only; `streaming` scope; Streaming SDA: no sales, ads, or payments; needs Client ID so the 5-user cap applies; non-commercial. | High. Blocks monetization and excludes Free users. Not recommended. |
| **(f) Outbound link only, other catalog for search** | Song identity held in your own (non-Spotify) catalog; each song has a "play on Spotify" link built from a matched ID. | You need another source of IDs. Spotify link building without the API requires a Spotify ID, which comes from a paste or the API (**not verified** how a non-Spotify catalog could produce it). | Not tested in this ticket; cross-service matching also touches the "another service" clause. Listed so the decision map can pick it up. |

**What a new entrant loses by not integrating the Web API at all (as documented):**
- in-app Spotify search (players paste links instead);
- artist name and ISRC from a pasted link (oEmbed gives title and cover only), which weakens cross-service matching by ISRC;
- one-click playlists in players' libraries;
- preview audio for Free listeners in your own player (the official `preview_url` is unreliable for new apps, and the embed is the only sanctioned route).
It does not lose legal exposure on games either way: the Widget Terms apply to embeds.

**Recommendation (inference, decision is the owner's):** build the product so that song identity does not depend on Spotify, and treat Spotify as options (b) and (c) only: paste links, embed, and let players or the organizer build the playlist. Treat legal exposure as open until a lawyer reads the Widget Terms games clause. A written request to Spotify for approval of embeds in a song-voting game costs little; no documented process exists, and nobody on the forum got an answer.

## Corrections to study 01

Checked against the live pages. Most of section 5 holds. These need changing:

1. **`preview_url` removal is overstated.** Study 01 says new apps lost the `preview_url` field and calls returned 403, citing a DEV Community summary because the official post could not be opened. The official post (2024-11-27) lists "30-second preview URLs, in multi-get responses (SimpleTrack object)" only, and says nothing about HTTP 403. Current Get Track and Search references still document `preview_url` ("Can be null"). Community reports that it is null everywhere are secondary. Status: not verified by call. The conclusion (do not rely on it) stands.
2. **The embed route has a games clause study 01 missed.** Study 01 treated only the Developer Policy. The Widget Terms (v2.0, effective 27 May 2014, the page linked as Embeds "Terms of Use") say games need "written approval" (IV.2.d). That changes open question 9 of study 01: links-only is not clearly outside the rules once an embed is used. A plain hyperlink: no Spotify document found; still a legal question.
3. **Commercial use is more specific than "tightly limited".** Policy IV splits Streaming SDAs (no sales, ads or payments) from Non-Streaming SDAs (app sales and ads allowed). Development Mode is separately limited to non-commercial use. Widgets and previews are not "Streaming".
4. **The six-week review claim now has a primary source.** Study 01 cites a forum post; the Quota modes page says "This review process can take up to six weeks."
5. **Extended-quota process.** Study 01 gives the criteria correctly (confirmed). Add: apply by form from a company email; approval is per reviewed use case; the review checks Developer Policy compliance, so the game ban is a second gate, not just the 250k MAU one. Extended-quota apps are exempt from the Feb 2026 endpoint changes, so legacy extended apps keep a wider API than a new entrant gets.
6. **Search details.** Confirmed `limit` max 10. Add default 5 and `offset` max 1000 (Search reference).
7. **Field removals.** Confirmed. Also removed in February: `linked_from` (track), `label` and `album_group` (album), `followers` (artist), and several user fields on `GET /me` (`country`, `email`, `explicit_content`, `followers`, `product`).
8. **Development Mode user count.** Confirmed 5 per Client ID, with grandfathering: "Existing apps are grandfathered: If you already have multiple Client IDs or more than 5 users, you will retain them."
9. **Refresh tokens and 25 Client IDs.** Confirmed. Add that Client Credentials tokens are not affected, and the quota is shared across the developer account.

Nothing else in section 5 contradicts the live pages.

## Not verified and open questions

Marked **not verified** in the text, and gathered here.

For a lawyer:
1. Is a themed song-submission and anonymous-voting league "game functionality" under Widget Terms IV.2.d, and "a game" under Policy III? Does a pasted link plus an embed trigger either?
2. Is the iframe Embed (and iFrame API) a "Widget" under the Widget Terms, or a "Spotify Platform" tool under the Developer Terms? The two documents point at each other.
3. Does a paid subscription, or in-app purchases, count as "commercial purposes" under Widget Terms IV.3.e when the site also embeds the Play Button?
4. May a league archive keep song titles, artists and covers after a season ("do not store Spotify Content indefinitely")? Is a Spotify track ID alone "Spotify Content"?
5. Does the "private personal use" licence wording (Developer Terms III.1) limit a public service?
6. Does a plain `open.spotify.com` hyperlink fall under any Spotify agreement?
7. Does matching one song across several services (even without Spotify's API) trigger the "another service" clause?

For Spotify (only they can answer):
8. Is there a written-approval process for games under Widget Terms IV.2.d, and who grants it? Does the Developer Policy's flat ban override it?
9. How does Music League operate under the "do not create a game" rule (legacy extended access, a separate agreement, or a different reading)? How do DJ League, BandJam and YapZap?
10. Exact Development Mode quota numbers and rate limit; not published.

Technical checks not done (need a registered app or a browser):
11. Whether `preview_url` is null for a brand-new Development Mode app, on single GET and search.
12. Whether a Development Mode app can call search through Client Credentials with no user token.
13. What a Free-tier listener actually hears in an embed, on desktop and mobile, with and without a logged-in session.
14. Behavior and load cost of 10 to 20 embeds on one page.
15. Whether a collaborative Spotify playlist shows who added each track (anonymity).
16. Whether Spotify changed anything after July 2026: the blog index could not be fetched.

Other limits: the Design Guidelines and Compliance Tips pages show no date; I could not confirm when they last changed. The DJ League privacy wording was read from the client-side bundle, not from a rendered page. The YapZap site returned no text, so its policy was not read. The Embeds landing page (what it says about terms and embed types) was read only through a WebFetch summary, not raw text. Policy, Terms, Compliance Tips, Widget Terms, quota, migration and changelog quotes come from raw page text.

## Sources

Primary (Spotify):
- https://developer.spotify.com/policy (Developer Policy, effective 15 May 2025)
- https://developer.spotify.com/terms (Developer Terms, v10, effective 15 May 2025)
- https://developer.spotify.com/compliance-tips
- https://developer.spotify.com/documentation/embeds/terms (Widget Terms of Use v2.0, 27 May 2014)
- https://developer.spotify.com/documentation/design
- https://developer.spotify.com/documentation/web-api/concepts/quota-modes
- https://developer.spotify.com/documentation/web-api/concepts/rate-limits
- https://developer.spotify.com/documentation/web-api/concepts/scopes
- https://developer.spotify.com/documentation/web-api/concepts/spotify-uris-ids
- https://developer.spotify.com/blog/2024-11-27-changes-to-the-web-api
- https://developer.spotify.com/blog/2025-04-15-updating-the-criteria-for-web-api-extended-access
- https://developer.spotify.com/blog/2026-02-06-update-on-developer-access-and-platform-security
- https://developer.spotify.com/blog/2026-06-18-refresh-token-expiration
- https://developer.spotify.com/blog/2026-07-23-web-api-quota-updates
- https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide
- https://developer.spotify.com/documentation/web-api/references/changes/february-2026
- https://developer.spotify.com/documentation/web-api/references/changes/march-2026
- https://developer.spotify.com/documentation/web-api/references/changes/may-2026
- https://developer.spotify.com/documentation/web-api/references/changes/july-2026
- https://developer.spotify.com/documentation/web-api/reference/search
- https://developer.spotify.com/documentation/web-api/reference/get-track
- https://developer.spotify.com/documentation/web-api/reference/create-playlist
- https://developer.spotify.com/documentation/web-api/reference/add-items-to-playlist
- https://developer.spotify.com/documentation/embeds
- https://developer.spotify.com/documentation/embeds/tutorials/creating-an-embed
- https://developer.spotify.com/documentation/embeds/tutorials/troubleshooting
- https://developer.spotify.com/documentation/embeds/tutorials/using-the-iframe-api
- https://developer.spotify.com/documentation/embeds/references/iframe-api
- https://developer.spotify.com/documentation/embeds/reference/oembed
- https://open.spotify.com/oembed (called twice, 2026-11-22)
- https://open.spotify.com/embed/track/4cOdK2wGLETKBW3PvgPWqT (fetched once, 2026-11-22)
- https://developer.spotify.com/documentation/web-playback-sdk
- https://developer.spotify.com/documentation/web-playback-sdk/reference

Competitors (their own pages):
- https://next.musicleague.com/support/how-to-play
- https://musicleague.com/privacy/ (last updated 2025-01-21)
- https://djleague.app/ and its script bundle at https://djleague.app/assets/index-CC4CyFLE.js (hash current at fetch time)
- https://bandjam.app/privacy.html (last updated 2026-05-08), https://bandjam.app/terms.html
- https://apps.apple.com/us/app/yapzap-music-video-leagues/id6748430650 (secondary: store listing)

Secondary (community and search; used for experience, not rules):
- https://community.spotify.com/t5/Spotify-for-Developers/Getting-written-permission-to-use-embeds-in-a-game/m-p/6953516
- https://community.spotify.com/t5/Spotify-for-Developers/Approval-for-a-Game-Using-Spotify-Web-Playback-SDK/td-p/7089786
- https://community.spotify.com/t5/Spotify-for-Developers/Clarification-on-Spotify-playback-what-s-allowed-for-my-app-or/td-p/7550652
- https://community.spotify.com/t5/Spotify-for-Developers/Preview-URLs-MP3-no-longer-exist-all-tracks/m-p/6712864
- https://community.spotify.com/t5/Spotify-for-Developers/Only-showing-preview/td-p/5485141
- https://github.com/TheKaoser/classical-portal/pull/88
