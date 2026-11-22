---
id: 08
title: How to match a song across services
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

How can a song submitted from any service be resolved to the same recording on the other services, reliably, for free and within each provider's terms (ISRC, Odesli/song.link, MusicBrainz, provider lookups)?

_Context:_ Decides whether a mixed-service league is feasible.

## Resolution

Resolved 2026-11-22 by crate-overnight #1 (research) and crate-session-2 (closing review). Findings: [research/song-matching.md](research/song-matching.md). Checked against its brief by the main session.

**Answer, in brief:**
- **The free Odesli/song.link API is gone** (retired 2026-07-31; keyless calls return 401). The web pages still work.
- **ISRC identifies a recording, not a song:** expect several ISRCs and several service IDs per song.
- **Keyless ISRC lookup:** Deezer (but see ticket 07: its terms bar this use) and MusicBrainz (CC0 data, 1 request a second, links to services sparse: 5 of 8 sampled; the web service is free for non-commercial use only).
- **YouTube has no ISRC;** matching is by title and channel, with "Artist - Topic" channels the one reliable signal.
- **Least risky design:** human-assisted matching: resolve what keyless, terms-compatible sources allow, show a confidence level, let the submitter confirm or paste the missing link.
- **Main-session correction:** the study's suggested resolver lists Deezer among the keyless sources; tickets 07 and 09 show Deezer's terms bar games and content databases, so Deezer drops out of any production design.

**Still open:** Odesli allowlist and terms; MusicBrainz terms for a product with any revenue; whether iTunes Search may be used to build Apple links in a game.
