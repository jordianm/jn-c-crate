---
id: 06
title: What a new game can do with YouTube
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

What can a new social music game do with YouTube and YouTube Music (search, playback, playlists), within which quota, at what cost and under which terms?

_Context:_ YouTube is the candidate universal, free playback layer.

## Resolution

Resolved 2026-11-22 by crate-overnight #1. Findings: [research/youtube-access.md](research/youtube-access.md). The main session re-checked on the live pages the default quota wording ("100 search.list calls, 100 videos.insert calls, and 10,000 units per day", Quota Calculator, updated 2026-11-12) and that the IFrame Player "does not require authorization" (Developer Policies); both matched.

**Answer, in brief:**
- **Playback is free and keyless:** the embedded IFrame player needs no API key and spends no quota, and `loadPlaylist([ids])` or `playlist=` plays an ad-hoc list of video IDs. It is still bound by the API terms: visible player of at least 200×200 px, no overlays, no background or audio-only play, a privacy policy naming YouTube, a Made For Kids check per video.
- **Search is the bottleneck:** 100 `search.list` calls per day for the whole project, shared by all users; no sanctioned search exists outside the Data API.
- **Playlist export is costly:** 50 units per insert, so a 10-song round playlist costs 550 units, about 18 per day on default quota.
- **More quota needs a compliance audit** with no published size, fee or timeline.
- **YouTube Music has no official API;** its links carry the same video ID. Unofficial libraries conflict with the terms (inference).
- **Workable design (inference):** players paste YouTube or YouTube Music links, resolved by the keyless oEmbed endpoint; search, if any, runs on another catalog or on the rationed 100/day.

**Supersedes in study 01:** the June 2026 change was not a search cut; search moved into its own bucket of 100 calls (it already cost 100 of the 10,000 units).

**Still open:** maximum `playlist=` length; how often official music videos block embedding; audit timeline; whether the `youtube` OAuth scope triggers Google's unverified-app user cap.
