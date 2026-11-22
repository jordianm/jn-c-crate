---
id: 07
title: Which other music services are usable
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

Which music services besides Spotify, Apple Music and YouTube (Deezer, TIDAL, SoundCloud, Amazon Music, Bandcamp, Qobuz, others) can a small social music game integrate with, and how? Which services do the likely players actually use?

_Context:_ "Works with any service" is a candidate differentiator; a keyless catalog could be the shared search layer.

## Resolution

Resolved 2026-11-22 by crate-overnight #1 (research) and crate-session-2 (closing review). Findings: [research/other-services.md](research/other-services.md). Checked against its brief by the main session.

**Answer, in brief:**
- **Deezer:** the keyless API works technically but its terms (updated 2026-10-27) bar games, revenue and content databases, and new app registration is reported closed. Legally closed.
- **TIDAL:** open developer path with ISRC, search and playlists, but non-commercial only, bars games, no known route to production.
- **SoundCloud:** API keys only for Artist Pro (99 USD a year); terms bar game use without licences.
- **Amazon Music:** closed beta API; link-out only.
- **Bandcamp, Qobuz, Anghami, Boomplay, JioSaavn:** not options.
- **Net:** "works with any service" through APIs is not realistic; link-out by title or ISRC is.

**Still open:** Whether metadata-only use of Deezer's keyless API is allowed; TIDAL production approval; a primary Spain/LatAm platform split.
