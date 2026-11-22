---
id: 11
title: Whether the game can live inside group chats
type: research
status: closed
blocked_by: []
claimed_by: crate-overnight #1
---

## Question

Can the game live where groups already gather (Discord, Telegram, WhatsApp, Slack, iMessage), or at least reach them there with invites and reminders, and on what technical and commercial terms?

_Context:_ Drop-outs and late voters are a known pain; one candidate product form is a chat-platform app.

## Resolution

Resolved 2026-11-22 by crate-overnight #1. Findings: [research/group-channels.md](research/group-channels.md). The main session re-checked on the live pages the WhatsApp Groups API limit ("Max group participants: 8", Official Business Account required) and Discord's payout rule (US, EU or UK teams, after the first $100); both matched.

**Answer, in brief:**
- **Discord** is the only chat where the whole game can run inside it: Activities (web apps in an iframe) are open to all developers since 2024-09-26 on desktop, mobile and web; a slash-command bot is the cheaper route, and two open-source Music League bots already exist. Premium Apps pays out to EU developers. Whether YouTube or Spotify players work inside an Activity is not verified.
- **Telegram** is the best free second option: free Bot API; Mini Apps open from a link in a group and know which chat opened them; digital goods must be sold in Telegram Stars.
- **WhatsApp cannot host the game:** the Groups API needs an Official Business Account and caps groups at 8 participants; Cloud API messages are paid (Spain, from 2026-10-01: utility 0.0166 EUR, marketing 0.0585 EUR). The free route is a `wa.me` share link that a person sends.
- **Slack** is a notification channel only (Cut Club posts reminders and results there; free workspaces allow 10 apps). **iMessage** apps need a native iOS app and miss Android members.
- **Net (inference):** for a Spain-based group, a web app with a good share link (Open Graph previews work in WhatsApp, iMessage, Telegram and Discord), reminders sent by the app itself (push, email), a "nudge on WhatsApp" button a person taps, and an optional Discord or Telegram bot for groups that live there.

**Still open:** audio or third-party players inside a Discord Activity; Discord revenue share and DM rules (support pages returned 403); WhatsApp Official Business Account requirements; link-preview rules per app (third-party guides only).
