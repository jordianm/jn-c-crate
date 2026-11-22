---
id: 05
title: What a new game can do with Apple Music
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

What can a new social music game do with Apple Music (MusicKit on web, iOS and Android, the Apple Music API, embeds, the iTunes Search API), at what cost, and under which monetisation rules?

_Context:_ Feeds the music-platform strategy and the business model.

## Resolution

Resolved 2026-11-22 by crate-overnight #1 (research) and crate-session-2 (closing review). Findings: [research/apple-music-access.md](research/apple-music-access.md). Checked against its brief by the main session.

**Answer, in brief:**
- **The Apple Music API and MusicKit need the paid Apple Developer Program (99 USD a year);** no fee waiver applies.
- **Free paths:** the keyless iTunes Search API (30 s preview URL, artwork, about 20 calls a minute, no ISRC) and the Apple Music embed (30 s for non-subscribers, full tracks for subscribers).
- **Monetisation ban is contractual:** DPLA 3.3.6(D) forbids monetising Apple Music access "in any way", including ads, for anything built on MusicKit or the API, web included.
- **Previews may not be a game's soundtrack** (guideline 5.2.5) and must show a link to Apple Music; iTunes Search terms bar using it to promote other goods.
- **Only sanctioned revenue:** Apple's affiliate programme (amount unpublished, Spain eligibility not verified).
- **Practical line (inference):** start with embeds and iTunes Search at zero cost; MusicKit JS later if ever.

**Still open:** Euro price of the membership; embed terms beyond the marketing-tools notice; whether ads around an embed are allowed.
