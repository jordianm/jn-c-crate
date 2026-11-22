# What a new game can do with Apple Music

Access date for all sources: 2026-11-22 (unless stated).
Ticket: [What a new game can do with Apple Music](../05-apple-music-access.md)

Method note: Apple's developer docs render client-side. I read their JSON sources (`developer.apple.com/tutorials/data/documentation/...`), the policy pages as HTML, and the MusicKit JS v3 docs from their published bundle. The human-readable URLs below are the pages those sources belong to. I called the keyless iTunes Search API four times and fetched one embed URL to observe behaviour.

## Answer

- **Catalog search needs only a developer token, not a user.** Every Apple Music API request needs a developer token signed with a MusicKit private key; the `/catalog` path is public catalog data. A Music User Token is only for `/me` (library) calls. Search returns at most 25 per call (default 5), and `filter[isrc]` looks up songs by ISRC (max 25 values). Song responses carry a `previews` array with an audio URL. ([developer tokens](https://developer.apple.com/documentation/applemusicapi/generating-developer-tokens), [handling requests](https://developer.apple.com/documentation/applemusicapi/handling-requests-and-responses), [search](https://developer.apple.com/documentation/applemusicapi/search-for-catalog-resources-(by-type)), [ISRC lookup](https://developer.apple.com/documentation/applemusicapi/get-multiple-catalog-songs-by-isrc))
- **The developer token requires a paid Apple Developer Program membership: 99 USD per year.** Apple's doc says the token authenticates you "as a trusted developer and member of the Apple Developer Program". Fee waivers exist only for nonprofits, accredited schools and government bodies that sell no digital goods, so they do not apply here. ([enroll](https://developer.apple.com/programs/enroll/), [fee waiver](https://developer.apple.com/help/account/membership/fee-waivers/))
- **Two paths need no membership at all: the keyless iTunes Search API and the Apple Music embed.** The Search API returns `previewUrl` (30 s), artwork and track ids, limited to "approximately 20 calls per minute". It has no ISRC field and no ISRC lookup (observed). The embed iframe (`embed.music.apple.com`) gives non-logged-in listeners a 30-second clip and subscribers full tracks. ([Search API](https://performance-partners.apple.com/search-api), [embed tool](https://artists.apple.com/support/1117-apple-music-marketing-tools))
- **Web playback works without iOS or the App Store.** MusicKit JS v3 plays previews with no authorization, and full tracks only after a subscriber authorizes your app. It can also write playlists to the user's library (`POST /v1/me/library/playlists`) with a Music User Token. ([MusicKit JS v3 docs](https://js-cdn.music.apple.com/musickit/v3/docs/index.html), [create playlist](https://developer.apple.com/documentation/applemusicapi/create-a-new-library-playlist))
- **The monetisation ban is in the developer agreement, not only in App Review.** DPLA 3.3.6(D): "You agree not to require payment for or indirectly monetize access to the Apple Music service (e.g. in-app purchase, advertising, requesting user info) through Your use of the MusicKit APIs, MusicKit JS, or otherwise in any way." That binds a web app too, because MusicKit JS is covered by name and you need the membership to get the key. DPLA page last updated 2026-10-29. ([DPLA](https://developer.apple.com/programs/apple-developer-program-license-agreement/))
- **Previews have their own rule.** Guideline 5.2.5 (updated 2026-10-16): previews "may not be used for their entertainment value (such as as the background music to a photo collage or the soundtrack to a game)", and a link to the music in Apple Music must be shown. The iTunes Search terms add: not "used to promote any other goods or services". ([Guidelines](https://developer.apple.com/app-store/review/guidelines/), [Search API legal](https://performance-partners.apple.com/search-api))
- **The only sanctioned revenue is affiliate commission on Apple Music sign-ups.** Apple Services Performance Partners pays "One-time payment on Membership", 30-day cookie. The amount is not published. Apple says it accepts "a limited number of partners". Spain eligibility is **not verified** on Apple's pages. ([commissions](https://performance-partners.apple.com/commissions-payments), [home](https://performance-partners.apple.com/))
- **For a Music League alternative, the practical line is:** the game can be free or paid for its own features only if Apple Music access itself is not the thing sold or ad-supported (inference, needs legal reading). Safest start is embeds plus iTunes Search at zero cost, with MusicKit JS added later for full playback and library playlists.

## 1. Apple Developer Program

- Fee: "The Apple Developer Program is 99 USD per membership year. Prices may vary by region and are listed in local currency during the enrollment process." ([enroll](https://developer.apple.com/programs/enroll/), [programs](https://developer.apple.com/programs/)). Spanish euro price not checked: **not verified**.
- Fee waiver (nonprofit, accredited educational institution, government entity): the applicant must not be "an individual, sole proprietor, or single-person business" and must not "otherwise sell digital goods or services through any of your apps". ([fee waivers](https://developer.apple.com/help/account/membership/fee-waivers/)). A game charging users does not qualify.
- Where MusicKit lives: the MusicKit service is enabled on an App ID (App Services tab, "Select the MusicKit checkbox") ([MusicKit service](https://developer.apple.com/help/account/services/musickit/)). For non-Apple platforms you create a media identifier and a Media Services private key in Certificates, Identifiers & Profiles; "You can associate two keys with each media identifier"; required role "Account Holder or Admin" ([media identifier](https://developer.apple.com/help/account/capabilities/create-a-media-identifier-and-private-key/)).
- Membership requirement: Apple's token doc states the token authenticates "a trusted developer and member of the Apple Developer Program" ([developer tokens](https://developer.apple.com/documentation/applemusicapi/generating-developer-tokens)). The programs page says "Sign in using your Apple Account and accept the Apple Developer Agreement to register for free" ([programs](https://developer.apple.com/programs/)), but I found no Apple page saying a free account can create the media key. Conclusion that membership is needed is well supported, not stated in one sentence (inference).
- Not needed for: the iTunes Search API, the embed/marketing tools, and the affiliate program (separate application, no fee found; see section 7).

## 2. Apple Music API

Source set: [Apple Music API](https://developer.apple.com/documentation/applemusicapi) (copyright 2026 on the page).

- **Developer token.** ES256 JWT; header `alg` + 10-char `kid`; claims `iss` (Team ID), `iat`, `exp`. "`exp` ... must not be greater than 15777000 (6 months in seconds)". Optional `origin` claim, "recommended for web clients", restricts use to listed origins. Tokens signed otherwise return 401. ([developer tokens](https://developer.apple.com/documentation/applemusicapi/generating-developer-tokens))
- **Music User Token (MUT).** Needed "for any requests for data specific to an Apple Music subscriber, such as to fetch content from the user's library"; sent in the `Music-User-Token` header. MusicKit manages it on Apple platforms and web; "Automatic Music User Token management is not available for Android". ([user authentication](https://developer.apple.com/documentation/applemusicapi/user-authentication-for-musickit))
- **Subscription needed for the MUT?** Mixed:
  - Web: an Apple engineer wrote (Apr 2022) "The authorization flow is only expected to resolve with a valid user token if the user logs in, authorizes your app, and has a valid Apple Music subscription." Secondary source, forum: [thread 704063](https://developer.apple.com/forums/thread/704063).
  - Native Swift: WWDC26 session "Integrate MusicKit into your app": "An Apple Music subscription is not required to use MusicKit, but the app will only be able to access purchased or synced music without one." ([WWDC26 254](https://developer.apple.com/videos/play/wwdc2026/254/))
  - So a non-subscriber can be authorized on iOS but gets no catalog playback or library write of catalog songs (inference from the above).
- **MUT lifetime.** Apple's docs give no figure. Apple staff on the forum say about 6 months, not configurable; some developers report 1-2 days; no refresh mechanism, user must sign in again. Secondary sources: [thread 654814](https://developer.apple.com/forums/thread/654814), [thread 724576](https://developer.apple.com/forums/thread/724576). Official lifetime **not verified**.
- **Catalog search.** `GET /v1/catalog/{storefront}/search?term=...&types=songs`. `limit`: default 5, maximum 25; `offset` pages; `types` include songs, albums, artists, playlists, music-videos, etc. ([search](https://developer.apple.com/documentation/applemusicapi/search-for-catalog-resources-(by-type)))
- **ISRC lookup.** `GET /v1/catalog/us/songs?filter[isrc]=USQE92100257`. "one ISRC value may return more than one song. The maximum fetch limit is 25." ([ISRC](https://developer.apple.com/documentation/applemusicapi/get-multiple-catalog-songs-by-isrc)). Song attributes include `isrc`, `artwork`, `url`, `playParams`, `previews`.
- **Previews in responses.** Song example in the docs: `"previews": [{"url": "https://audio-ssl.itunes.apple.com/.../mzaf_....plus.aac.p.m4a"}]` ([get a song](https://developer.apple.com/documentation/applemusicapi/get-a-catalog-song)). The `Preview` object has `url`, `hlsUrl` and, for videos, artwork ([Preview](https://developer.apple.com/documentation/applemusicapi/preview)).
- **Playlists in the user's library.** `POST https://api.music.apple.com/v1/me/library/playlists` with `attributes` (`name`, `description`, `isPublic`) and optional `tracks` relationship; 201 Created; "This endpoint requires a music user token"; "There may be a delay before a new resource appears in a user's library." Add tracks: `POST /v1/me/library/playlists/{id}/tracks`, 204. ([create](https://developer.apple.com/documentation/applemusicapi/create-a-new-library-playlist), [add tracks](https://developer.apple.com/documentation/applemusicapi/add-tracks-to-a-library-playlist))
- **Rate limits.** Documented only qualitatively: requests over the limit "temporarily receive 429 Too Many Requests"; no number is published. ([developer tokens](https://developer.apple.com/documentation/applemusicapi/generating-developer-tokens)). Numeric limit **not verified** (none exists in the docs).
- **Cost.** No usage fee appears in the API docs or the program pages; the only cost found is the 99 USD membership.

## 3. MusicKit by platform

Overview page: [MusicKit](https://developer.apple.com/musickit/): "users can use your app or website to create playlists, add songs to their library, and play any of the millions of songs in the Apple Music catalog."

- **Web (MusicKit JS v3).** Needs a signed developer token to initialise ("You must have a signed developer token in order to initialize MusicKit on the Web"). Docs: "When a user with a valid Apple Music subscription authorizes your app, MusicKit will allow full playback of content from the Apple Music catalog. If the app does not have user authorization, then playback is restricted to non-DRM preview assets, which are snippets of the full media." "Without user authorization, or for users who do not have a valid Apple Music subscription, your app can still play previews of media from Apple Music, as well as make data requests that do not require the MUT." `previewOnly = true` forces previews. Browsers can block autoplay ("playback ... requires user interaction first"). Library calls via `music.api.music('v1/me/library/...')` after `authorize()`. ([MusicKit JS v3 docs](https://js-cdn.music.apple.com/musickit/v3/docs/index.html), read from the docs bundle; no page date shown.)
- **iOS (MusicKit for Swift).** Catalog search (`MusicCatalogSearchRequest`), two players (`SystemMusicPlayer`, `ApplicationMusicPlayer`), library access, subscription checks and a `musicSubscriptionOffer` view that can carry affiliate info. Developer token is automatic if MusicKit is ticked on the App ID. New in WWDC26: a system Music Picker; without a subscription it shows only library items. ([MusicKit](https://developer.apple.com/documentation/musickit), [WWDC26 254](https://developer.apple.com/videos/play/wwdc2026/254/))
- **Android.** "MusicKit for Android lets you build native Apple Music features into your Android app. Libraries are available to let users sign in to their Apple Music account and play music directly from your app." ([MusicKit](https://developer.apple.com/musickit/)). MUT is not automatic on Android; you follow the SDK's authentication section. I could not open the SDK Javadoc (404 to curl), so the SDK's requirements (for example needing the Apple Music app installed) are **not verified**.
- **Preview behaviour across the three:** web and native both fall back to preview assets without subscription. Previews are non-DRM; an Apple engineer says apps without a subscription "can only play preview assets" (forum, secondary; not re-fetched, quoted via search summary): [thread 761237](https://developer.apple.com/forums/thread/761237).

## 4. Embeds and marketing tools

- **What it is.** Apple Services Marketing Tools "Preview Players": "Post or embed custom players to play a preview of your music." ([tools](https://tools.applemediaservices.com/apple-music))
- **Behaviour.** "Listeners not logged in to Apple Music can play a 30-second clip of a song or see a preview of an entire album or playlist with the full list of songs displayed. If they are logged in to Apple Music, listeners can hear full tracks without ever leaving your website. Listeners can also open Apple Music directly from the player to log in or sign up for a free trial." Create it by searching in the tool and clicking "Copy Embed". ([Apple Music for Artists: marketing tools](https://artists.apple.com/support/1117-apple-music-marketing-tools))
- **No key.** Fetching `https://embed.music.apple.com/us/album/emotional-creature/1613600183?i=1613600188` with curl returned HTTP 200 with no `X-Frame-Options` and no `frame-ancestors` in its CSP (observed 2026-11-22). The URL pattern is the normal `music.apple.com` song URL with the host changed (inference from the observed URL).
- **Terms.** The tools page says: "Embeddable widgets and promotional artwork are provided by Apple as an accommodation only. Apple assumes no responsibility ... Apple reserves the right to de-activate any widget at its sole discretion." (page footer copyright 2026, [tools](https://tools.applemediaservices.com/apple-music)). I found no separate embed terms with a monetisation clause. Whether ads around an embed are allowed is **not verified**.
- **Limits for a game (inference).** The iframe is a closed player: the game cannot read what was played or force a 30-second listening. The game stores the song URL or id and shows the embed.
- **Badges.** Apple Music Identity Guidelines: use Apple-supplied badge art only, never alter it; "If you include an Apple Music badge along with badges for other music services, place the Apple Music badge first"; link to Apple Music wherever a badge is used. ([Identity Guidelines](https://www.apple.com/itunes/marketing-on-music/identity-guidelines.html), page has no date)

## 5. iTunes Search API (no key)

Official doc, hosted by the Performance Partners site: [iTunes Search API](https://performance-partners.apple.com/search-api) (footer copyright 2022; no revision date).

- **Endpoints.** `https://itunes.apple.com/search?term=...` and `/lookup?id=...` (also `upc`, `amgArtistId`). Parameters: `term`, `country`, `media`, `entity`, `attribute`, `limit` ("1 to 200", default 50), `lang`, `explicit`, `callback`.
- **Rate limit.** "The Search API is limited to approximately 20 calls per minute (subject to change)." Heavier use: Apple points to the Enterprise Partner Feed. So the ~20/min figure in study 01's source material is confirmed as documented. My four calls showed no rate-limit headers (observed).
- **Fields observed (song, `country=ES`).** `trackId`, `collectionId`, `artistId`, `trackName`, `artistName`, `collectionName`, `trackViewUrl` (a `music.apple.com/es/...` link), `previewUrl` (`.m4a`, 30 s), `artworkUrl30/60/100`, `trackTimeMillis`, `releaseDate`, `trackExplicitness`, `isStreamable`, prices. **No ISRC field.** `lookup?isrc=USQE92100257` returned `resultCount: 0` (observed; ISRC lookup is not in the docs). A game that must match songs across services by ISRC therefore needs the Apple Music API, not the iTunes API.
- **Terms ("Legal" section).** Promo content (song previews, album art) may be used "for the purposes of promoting the subject of the Promo Content", provided it: (i) sits only on pages that promote that content; (ii) is next to an Apple badge linking to the content; (iii) says "provided courtesy of iTunes" for previews; (iv) is "streamed only, and not downloaded, saved, cached, or synchronized with video"; (v) "is not used for independent entertainment value apart from its promotional purpose"; and (vi) "is not used to promote any other goods or services." The overview adds: previews "only to promote store content and not for entertainment purposes". Governed by California law.
- **Reading for a game (inference, not legal advice).** Playing a 30-second preview so players can judge a song submitted to a round is close to "independent entertainment value" and to promoting the game itself (point vi). The text is written for affiliate sites, and the terms names iTunes, not Apple Music. Treat previews from this API as a grey zone for a product that earns money.

## 6. Rules and terms

### App Review Guidelines (only if there is an iOS app)

Page: [App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/), "Last Updated: October 16, 2026".

- **4.5.2(i)** "MusicKit on iOS lets users play Apple Music and their local music library natively from your apps and games. ... Users must initiate the playback of an Apple Music stream and be able to navigate using standard media controls such as 'play,' 'pause,' and 'skip.' Moreover, your app may not require payment or indirectly monetize access to the Apple Music service (such as in-app purchase, advertising, requesting user info, etc.). Do not download, upload, or enable sharing of music files sourced from the MusicKit APIs, except as explicitly permitted in MusicKit documentation."
- **4.5.2(ii)** MusicKit "is not a replacement for securing the licenses you might need"; playing a specific song at a particular moment or making shareable audio/video needs rights-holder permission. "Cover art and other metadata may only be used in connection with music playback or playlists ... and should not be used in any marketing or advertising without getting specific authorization from rights-holders." Follow the Apple Music Identity Guidelines.
- **4.5.2(iii)** Apple Music user data (playlists, favorites) must be disclosed in the purpose string; "may not be shared with third parties for any purpose other than supporting or improving the app experience. This data may not be used to identify users or devices, or to target advertising."
- **4.10** "You may not monetize built-in capabilities ... or Apple services and technologies, such as Apple Music access, iCloud storage, or Screen Time APIs."
- **5.2.5** "Music from iTunes and Apple Music previews may not be used for their entertainment value (such as as the background music to a photo collage or the soundtrack to a game) or in any other unauthorized manner. If you provide music previews from iTunes or Apple Music, you must display a link to the corresponding music in iTunes or Apple Music."
- **3.1.1** features, subscriptions, in-game currencies, game levels and premium content unlocked in an iOS app "must use in-app purchase". **3.1.3(b)** multiplatform services may let users access content bought elsewhere "provided those items are also available as in-app purchases within the app". So an iOS app charging for league features uses IAP (Apple's cut applies; rate not checked); the charge must not be for Apple Music access (4.5.2, 4.10).
- **Previews as a soundtrack.** 5.2.5 is aimed at decorative use. A game where the previewed song is the object being judged is a different use, but the guideline does not carve this out, so App Review's reading is **not verified** (inference).

### Developer agreement (applies to web too)

Page: [DPLA](https://developer.apple.com/programs/apple-developer-program-license-agreement/), "last updated October 29, 2026". Section 3.3.6(D) "MusicKit":

- Do not use the APIs or MusicKit JS "for purposes unrelated to facilitating access to Your end users' Apple Music subscriptions."
- Follow the Apple Music Identity Guidelines.
- No requiring payment for, or "indirectly monetize access to", Apple Music "through Your use of the MusicKit APIs, MusicKit JS, or otherwise in any way" (examples: in-app purchase, advertising, requesting user info).
- "full songs must be enabled for playback, and users must initiate playback" with standard controls.
- No downloading, uploading or modifying MusicKit Content; it "cannot be synchronized with any other content"; album art and text "may not be used separately from music playback or managing playlists".
- User metadata only for a clearly disclosed, directly relevant function.
- MusicKit JS only "as a stand-alone library", not re-hosted or recombined.

The DPLA defines "Corresponding Product" as "Your website, web application, or other version of Your software application", and 3.3.6(D) names MusicKit JS for "Applications, websites, or web applications". Whether a web app without any iOS app is bound is therefore very likely yes, because the key comes from the membership (inference).

### Web app outside the App Store

- The App Review Guidelines govern App Store distribution; the guidelines themselves say "For everything else there is always the open Internet." A pure web app is not reviewed by Apple.
- The DPLA 3.3.6(D) limits still apply to anyone using the MusicKit key. The iTunes Search terms apply to anyone using that API. Embeds fall under the tool's accommodation notice.
- The unresolved question: does a game that sells league features or shows ads "indirectly monetize access to Apple Music"? Apple's wording lists ads explicitly, so an ad-supported page that is built around MusicKit playback is the clearest risk. Apple does not publish a test. **Not verified.** Needs a lawyer or a written answer from Apple. (inference)

## 7. Apple Services Performance Partners (affiliate)

- **Still exists, renamed.** "Our affiliate program, now called the Performance Partner Program ... Earn commissions on qualifying Apple Music, Apple TV, and Apple Podcasts memberships as well as the sales of movies, TV shows, books, audiobooks and more." ([home](https://performance-partners.apple.com/))
- **Apple Music is commissionable.** Table: Apple Music, devices "iOS, iPadOS, macOS, Android, Windows", rate "One-time payment on Membership", cookie "30 days". The euro or dollar amount is not on the page. ([commissions](https://performance-partners.apple.com/commissions-payments))
- **Tiers.** "Most Partners: Standard Program"; "By Invitation Only: Premier Program" (paid per trial; criteria: trials at scale, trial-to-paid conversion, brand standards).
- **Eligibility.** "Currently, we are only accepting a limited number of partners who can drive volume and quality that meet Apple guidelines." Applications can be rejected for no website or App Store link, a site under construction, trademark use in the domain, and similar reasons ([FAQ](https://performance-partners.apple.com/faq)). Another page says the program "is only open to partners who have content on one of the Apple Media Stores and by invitation to a limited number of other partners" ([partners page](https://performance-partners.apple.com/partners), aimed at labels and artists). The two statements pull in different directions; whether a new game qualifies is **not verified**.
- **Mechanics.** Third-party platform Partnerize; links need `at=<token>` and for Apple Music `app=music`, e.g. `https://music.apple.com/subscribe?app=music&at=XXXXXX&ct=YYYYYY&ls=1` ([linking guide](https://performance-partners.apple.com/linking)). Payout threshold 30 USD or equivalent, paid "approximately 60 - 90 days after the month's end", 60 currencies, 214 countries ([commissions](https://performance-partners.apple.com/commissions-payments)).
- **Spain.** Apple's pages give no country list for Apple Music commissions. A search-engine summary of the Skimlinks listing says Spain is included; I did not open that page: **not verified**.
- **Fit with the DPLA.** Apple itself promotes it for MusicKit apps: in the WWDC26 session, "you have the potential to earn commissions when someone subscribes to Apple Music through your app, as part of the Apple Services Performance Partner Program" via `MusicSubscriptionOffer.Options` ([WWDC26 254](https://developer.apple.com/videos/play/wwdc2026/254/)). So this form is Apple-sanctioned. Expect small amounts (inference: one-time payment per sign-up, 30-day cookie).
- **MusicKit JS affiliate options.** An older MusicKit JS sample page lists `affiliateToken` and `campaignToken` in `configure()` (via a search summary; not read directly). The v3 docs bundle I read has no mention: **not verified** for v3.

## Options table

| | A. Web embeds + iTunes Search | B. Full MusicKit on the web | C. Native iOS (MusicKit Swift) |
|---|---|---|---|
| Fixed cost | 0 (no membership, no key) | 99 USD/year (membership, media key) | 99 USD/year (also needed to ship on the App Store) |
| Search | iTunes Search API, ~20 calls/min, 200 max results, no ISRC | Apple Music API search, 25 per call, ISRC lookup; developer token only | Same API through `MusicCatalogSearchRequest` or the Music Picker |
| Non-subscriber hears | 30-second clip (embed) / `previewUrl` | Previews, no sign-in needed | Previews; library-only without subscription |
| Subscriber hears | Full track in embed if logged in to Apple Music in that browser | Full tracks after authorize() | Full tracks via `ApplicationMusicPlayer` |
| Library writes (round playlist) | None; user opens the link themselves | Yes, with MUT: create playlist, add tracks | Yes, with user permission |
| Game control of playback | None (closed iframe; previews via `previewUrl` are an `<audio>` you control, grey-zone terms) | High (events, queue) | High |
| Monetisation limits | Search API: not used to "promote any other goods or services", no independent entertainment value. Embed: no monetisation clause found, **not verified** | DPLA 3.3.6(D): no payment for or indirect monetisation of Apple Music access, ads and "requesting user info" named. Own game features: unclear (inference) | Same DPLA plus 4.5.2, 4.10, 5.2.5, IAP via 3.1.1 for own features |
| Revenue allowed | Affiliate (if accepted) | Affiliate (if accepted) | Affiliate; IAP for own features (inference) |
| Main risk | Terms written for affiliates; embeds can be changed or removed by Apple | MUT expiry (user must re-sign in); ad-funded page is the clearest violation risk | App Review discretion; Apple's commission on any IAP (rate not checked) |

Android (MusicKit SDK) behaves like C for playback; MUT handling is manual and the SDK was not inspected (**not verified**).

## Corrections to study 01

Section 5 of [01-market-music-league.md](../../../../research/01-market-music-league.md), claim by claim.

1. **"Apple Developer Program membership ($99/year) ... was not verified."** Now confirmed: 99 USD per membership year ([enroll](https://developer.apple.com/programs/enroll/)); token doc ties the token to membership. A fee waiver is not available to a for-profit game.
2. **"Music User Token requires an active Apple Music subscription."** Too flat. On the web, an Apple engineer says authorize() resolves with a token only for subscribers. On native iOS, Apple's WWDC26 session says a subscription "is not required to use MusicKit" (non-subscribers get only purchased or synced music). Also, catalog search needs no MUT at all.
3. **"MUT expires after about 6 months ... not verified."** Still not in official docs. Apple staff say 6 months on the forum; others report 1-2 days; the 6 months in the official docs is the developer token (`exp` max 15777000 s). The study's caveat stands.
4. **Developer token "valid up to 6 months."** Confirmed: 15777000 seconds. The study's URL ends in `.md` and is a JSON/markdown source; the human page is `/documentation/applemusicapi/generating-developer-tokens`.
5. **4.5.2 quote.** Accurate. Missing: the same rule is in the developer agreement (DPLA 3.3.6(D)) and so covers web apps with no App Store listing; the study framed it as an App Review rule only. This is the main correction to the implication paragraph. Also 4.5.2(iii) bans using Apple Music user data "to identify users or devices, or to target advertising".
6. **"Some versions of the text require user-initiated playback ... still in force not verified."** Confirmed in force in the guidelines (4.5.2(i), updated 2026-10-16) and in DPLA 3.3.6(D), which also requires full songs to be enabled for playback.
7. **"5.2.5 bars previews as entertainment, according to a quote on the forum."** Now verified from the primary page. Exact text differs from the study's paraphrase: "(such as as the background music to a photo collage or the soundtrack to a game)"; it also requires "a link to the corresponding music in iTunes or Apple Music".
8. **4.10.** Accurate: "Apple services and technologies, such as Apple Music access".
9. **Implication paragraph "an app with ads or an 'ad-free' premium has to clearly separate ...".** Plausible but Apple's DPLA lists "advertising" as an example of banned indirect monetisation; no Apple source confirms the "separation" reading. Keep it as inference.
10. **Omissions the study did not cover:** iTunes Search API terms and ~20/min limit; embeds; affiliate commissions; no ISRC in iTunes API; search limit 25; MusicKit JS previews without authorization.
11. **Study 01 open question 11** (are user-initiated playback and 5.2.5 still in force) is answered: yes, both, as of 2026-10-16.

## Not verified and open questions

- Official MUT lifetime and whether a refresh path exists (only forum statements by Apple staff).
- Numeric rate limit of the Apple Music API (none documented; only 429).
- Whether a free Apple Account can create the media identifier and key (inference: no).
- Euro price of the membership in Spain.
- MusicKit for Android SDK details (Javadoc unreachable; Apple Music app dependency unchecked).
- Terms for the embed itself beyond the "accommodation" notice; whether ads around an embed are allowed.
- Whether a paid or ad-funded game that never sells Apple Music access violates "indirectly monetize" (needs a lawyer or Apple's written answer; this is the key legal question for the business-model decision).
- Whether App Review accepts previews of submitted songs as non-"entertainment" use.
- Whether a new game is accepted by Performance Partners; amount per sign-up; Spain eligibility.
- Whether the iTunes Search API `previewUrl` may be used under the Search API terms by a product that also earns money (terms are from 2022 and name iTunes).
- Apple's In-App Purchase commission rate and any small-business rate (not looked up; out of ticket scope).
- Whether `embed.music.apple.com` also works in an iframe with sandbox restrictions, and what it does on mobile Safari without sign-in (not tested).

## Sources

Primary (Apple):
- https://developer.apple.com/documentation/applemusicapi (copyright 2026)
- https://developer.apple.com/documentation/applemusicapi/generating-developer-tokens
- https://developer.apple.com/documentation/applemusicapi/user-authentication-for-musickit
- https://developer.apple.com/documentation/applemusicapi/handling-requests-and-responses
- https://developer.apple.com/documentation/applemusicapi/search-for-catalog-resources-(by-type)
- https://developer.apple.com/documentation/applemusicapi/get-multiple-catalog-songs-by-isrc
- https://developer.apple.com/documentation/applemusicapi/get-a-catalog-song
- https://developer.apple.com/documentation/applemusicapi/preview
- https://developer.apple.com/documentation/applemusicapi/create-a-new-library-playlist
- https://developer.apple.com/documentation/applemusicapi/add-tracks-to-a-library-playlist
- https://developer.apple.com/documentation/musickit
- https://developer.apple.com/musickit/
- https://js-cdn.music.apple.com/musickit/v3/docs/index.html (MusicKit JS v3 docs; text read from `main.49f36b39.iframe.bundle.js`)
- https://developer.apple.com/videos/play/wwdc2026/254/
- https://developer.apple.com/programs/ , https://developer.apple.com/programs/enroll/
- https://developer.apple.com/help/account/membership/fee-waivers/
- https://developer.apple.com/help/account/services/musickit/
- https://developer.apple.com/help/account/capabilities/create-a-media-identifier-and-private-key/
- https://developer.apple.com/app-store/review/guidelines/ (Last Updated October 16, 2026)
- https://developer.apple.com/programs/apple-developer-program-license-agreement/ (last updated October 29, 2026)
- https://performance-partners.apple.com/search-api (iTunes Search API; footer copyright 2022)
- https://performance-partners.apple.com/ , /commissions-payments , /faq , /linking , /partners
- https://tools.applemediaservices.com/apple-music (copyright 2026)
- https://artists.apple.com/support/1117-apple-music-marketing-tools
- https://www.apple.com/itunes/marketing-on-music/identity-guidelines.html
- https://embed.music.apple.com/us/album/emotional-creature/1613600183?i=1613600188 (headers observed)
- https://itunes.apple.com/search?term=beach+bunny+oh+brother&media=music&entity=song&limit=2&country=ES and https://itunes.apple.com/lookup?isrc=USQE92100257 (observed)

Secondary (Apple forums, Apple staff posts; used only where flagged):
- https://developer.apple.com/forums/thread/704063
- https://developer.apple.com/forums/thread/654814
- https://developer.apple.com/forums/thread/724576
- https://developer.apple.com/forums/thread/761237 (via search summary)

Not opened directly (search summary only, flagged in text): Skimlinks Apple Services listing; older MusicKit JS v1 sample page.
