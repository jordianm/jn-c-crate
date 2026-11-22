---
id: 04
title: What a new game can do with Spotify
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

What can a new, small third-party social music game do with Spotify in late 2026, legally and technically (Web API in each quota mode, embeds, oEmbed, links), and what does it lose by not integrating the Web API at all?

_Context:_ Feeds the music-platform strategy.

## Resolution

Resolved 2026-11-22 by crate-overnight #1. Findings: [research/spotify-access.md](research/spotify-access.md). The main session re-checked on the live pages the Developer Policy line "Do not create a game, including trivia quizzes" (effective 15 May 2025) and the Widget Terms clause IV.2.d (Version 2.0, effective 27 May 2014); both matched word for word.

**Answer, in brief:**
- **Games are banned in the Web API** (Developer Policy III, no approval route) **and in embeds** unless Spotify gives written approval (Widget Terms IV.2.d: "you may not use the Spotify Platform to incorporate Spotify Content into any game functionality (including trivia quizzes)"). Study 01 missed the Widget Terms.
- **Development Mode cannot carry a product:** personal, non-commercial use, owner needs Premium, 5 users per Client ID. **Extended quota** needs a registered organization, a launched service and 250k MAU, and its review checks Developer Policy compliance, so the game ban applies there too.
- **Keyless pieces work technically:** embeds, the oEmbed endpoint (title and cover, no artist), `open.spotify.com` links. Embeds play full tracks only for logged-in Premium listeners; others get a preview. No documented limit on embeds per page.
- **Other clauses that bite a multi-service league:** "Do not create any product or service which is integrated with streams or content from another service"; limits on storing Spotify metadata ("Do not store Spotify Content indefinitely").
- **Competitors:** DJ League runs search and playlists through one operator-owned Spotify account; BandJam holds Spotify tokens; none shows a quota status or an agreement with Spotify.
- **Net (inference):** Spotify cannot be a dependency. The API route is closed to a commercial game; the link-and-embed route has no technical block but an unresolved legal risk. The cleanest option is an outbound link only ("open in Spotify"), which needs a lawyer's view before relying on it.

**Still open (needs a lawyer or Spotify):** whether a league that only links to or embeds Spotify tracks is "game functionality"; whether outbound links alone fall under any Spotify terms; `preview_url` status for new apps; what Free listeners hear in an embed.
