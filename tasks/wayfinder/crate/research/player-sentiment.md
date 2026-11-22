# What players love, hate and ask for

Access date for all sources: 2026-11-22. Ticket: [What players love, hate and ask for](../03-player-sentiment.md)

## Answer

- **The loudest complaint is the mobile ad experience, and it is the only theme that is overwhelming.** 283 of 458 App Store reviews mention ads (62%), 234 of the 277 one- and two-star reviews do, and the share rose from 29% of 2023 reviews to 86% of 2026 reviews. The harm is to the game, not just to taste: "My latest league fell apart after one round and had less than 10% participation because the friction to use it is so high" (App Store US, 2026-06-23). Music League itself calls its old ad setup "an unpleasant advertising experience" ([news post, 2026-11-12](https://next.musicleague.com/news/why-we-rebuilt-music-league)).
- **What players love is social, not mechanical.** Friends, family and colleagues keeping in touch (keyword hits in about 124 reviews) and discovering music (about 45) lead; competition and banter come third (about 35). Nobody in the sample praised the points system as such.
- **The Spotify-only lock-in is the most persistent feature gap, and the longest-running.** About 30 reviews ask for another service (Apple Music about 15, YouTube or SoundCloud 5, Amazon and Qobuz 1 each), spread evenly from 2022 to 2026. Two blog reviewers (2025, 2026) call it the main drawback. Study 01 shows 2.0 now supports Apple Music; YouTube Music is still missing.
- **Reliability and sign-in failures hurt more than annoyance, because deadlines turn a bug into a missed round.** About 95 reviews mention crashes, errors or login loops, peaking in 2025 (46 of 123 reviews). Quote: "I’m about to miss a voting deadline and two submission deadlines just because Music League hasn’t allowed me to perform ANY actions in over 24hrs" (App Store GB, 2025-04-03).
- **Rules complaints are few and, in 2.0, mostly already answered.** Forced downvotes or forced point spending (4 reviews, 2022-2025), repeat-artist "orange boxing" (2, 2026), waiting for the deadline when everyone has voted (about 5) are all addressed by the 2.0 settings in study 01. Players want opposite things on some of them (one asks for negative points, another for optional downvotes), so admin-set rules look right.
- **Guess-who-submitted-it is a real but small ask, and the best-evidenced feature Music League lacks.** Six reviews across 2022-2026 ask for it unprompted, several say they already play it by hand; BandJam and DJ League ship it. Count is small, so treat as moderate.
- **Social features are wanted beyond the league: chat reactions and replies, a friends list or follow, easier invites, finding leagues.** About 15 reviews. Music League's own interview says "Comments and Chat became much more important than we anticipated" ([Nitro, 2026-09-28](https://blog.nitropay.com/publisher-showcase-music-league/)).
- **Accessibility is a small count with a severe effect.** Three reviews over three years (2023, 2025, 2026) from or for blind VoiceOver users who cannot submit or vote.
- **I found no player evidence at all on the 2.0 beta, on Reddit, or for live or daily formats.** Reddit could not be reached (section 2). In 458 reviews nobody asks for a synchronous or daily game. That is absence in a mobile-store sample of existing Music League users, not proof of no demand.
- **The alternatives have almost no independent player data.** BandJam has 5 US store reviews, YapZap 2, DJ League and Cut Club none with text, songbattle.io none. Their own pages are marketing. The only recurring signal: "needs more users".

## Method and sample

**Main sample: App Store written reviews of Music League.** I pulled the public customer-reviews feed (`itunes.apple.com/<country>/rss/customerreviews/page=1..10/id=1589815321/sortBy=mostRecent/json`) for 12 storefronts and got 458 unique written reviews: US 361, CA 36, GB 29, AU 10, DE 10, IT 4, FR 3, ES 3, NL 2. Dates run 2022-02-12 to 2026-11-17 (2022: 32, 2023: 56, 2024: 62, 2025: 123, 2026: 185). 210 are from the last 12 months. Stars: 1★ 196, 2★ 81, 3★ 62, 4★ 44, 5★ 75. An independent aggregator shows nearly the same split for 481 reviews (1★ 203, 2★ 85, 3★ 64, 4★ 47, 5★ 82) ([mwm.ai](https://mwm.ai/apps/music-league/1589815321)), so the feed appears close to complete for written reviews. Not verified: whether the feed hides any.

**Counting.** Themes are keyword counts over title plus text, then spot-checked by reading about 290 reviews in full (all 147 that do not mention ads, the 141 most recent). Counts are therefore approximate and one review can sit in several themes. Where a keyword over-matches I give a hand count instead ("about", or "N reviews" listed by date).

**Known biases, in order of size.**
1. **Written reviews skew negative.** The store's overall rating is 4.65 from 6,586 ratings (US; 4.63 GB, 4.58 CA, 4.69 AU, from the [iTunes lookup API](https://itunes.apple.com/lookup?id=1589815321&country=us)), yet 42% of written reviews are 1★. Google Play shows about 3.2-3.3 from about 2.6K ratings, via a search summary and [AppBrain](https://www.appbrain.com/app/music-league/com.musicleague.app) which I could not open (HTTP 403): not verified.
2. **Mobile only, iOS only in practice.** Everyone writes about the legacy 1.x app (latest reviews are on 1.4.11). Web-only players, who say the web is fine, are under-represented. The 2.0 beta and its TestFlight app are not in the sample.
3. **The ad wave dominates the window.** Ads started in late 2022 (earliest mention 2022-12-19) and escalated in 2026, so recent reviews are mostly about ads and push other themes down. Older reviews (2022-2023) are the cleanest view of feature wishes.
4. **US-heavy** (79%). The 3 Spanish, 3 French and 10 German reviews are too few to say anything about those markets.
5. **Players who left do not review.** Churned groups are visible only through the few reviews that describe it.

**Other sources.** Blog and press reviews (Vice, a Substack, Headphonesty, Hofstra Chronicle) and a 2021 Hacker News thread; Music League's own news post and a publisher interview; competitor stores and marketing pages. Competitor pages are claims by vendors, not player evidence, and I label them so.

**What I could not reach.**
- **Reddit (r/musicleague and others): not reached.** The JSON, RSS and HTML endpoints from this machine returned HTTP 403 or 429; the fetch tool and the search tool refuse reddit.com. I did not try to get around the block. The ticket's main non-store source is therefore missing; its likely effect is under-counting feature requests and 2.0 beta talk, since Reddit threads tend to be longer and more specific than store reviews.
- Google Play review text (page does not render for the fetch tool; AppBrain 403), Hofstra Chronicle (proxy refused), ILX and Headphonesty (403), Product Hunt and similar not tried. All claims from those come through search-engine summaries and are marked not verified.
- Music League's own feedback inbox, roadmap or voting board: none found.
- Discord servers, Twitch chats, TikTok and Instagram comments: not reachable.

## Themes

Strength key: **very strong** = 100+ independent mentions, several sources; **strong** = 20-99; **moderate** = 6-19; **weak** = 2-5; **single** = 1. "Independent" means separate reviews or articles; they are not coordinated, but the ads theme shares one cause.

### 1. Mobile ads and monetisation friction

**Hate. Strength: very strong.**
- 283 of 458 reviews mention ads; 84 describe ads that cannot be closed or freeze the app; about 100 complain about length (30 seconds to several minutes); about 118 say ads gate basic actions (results, standings, switching rounds). By year: 2023 16 of 56, 2024 42 of 62, 2025 65 of 123, 2026 159 of 185. Spread: all 9 storefronts, Google Play per secondary summaries, one aggregator, and an admission by the maker.
- Where it bites is specific: results and standings. "You have to watch ads to look at the standings. To look at votes. To submit. To breathe." (US, 2026-11-01). "the actual use of the app involves opening it up to check scores or vote… which only takes around 45 seconds. But you’ll be stuck watching ads for probably a good minute and a half" (CA, 2026-06-18).
- Ads that do not close: "full-screen takeover ads with no close button, freezing you out of doing anything else in the app" (GB, 2026-10-19). 18 reviews call the ad content itself bad (scam-like, mini-game, "AI slop").
- The paid workaround is unpopular: the ad-free timer. "Most recent update made it so you only get 2 hours of ad-free time after watching an ad instead of 48 hours after 2-3 ads" (US, 2026-03-01). "an option to watch “two” back-to-back ads (really four…) just to get access to just SIX HOURS of no ads… my league doesn’t complete a round until a few days later" (US, 2026-06-10).
- Effect on play: "My music league groups now fail because people are unwilling to watch multiple LONG back to back ads" (US, 2026-06-23); "everyone in our leagues quit halfway through because we can’t even check the score" (US, 2026-03-16). Also "Music League is only making money through the ads that must be viewed in order to see the results" (US, 2024-07-02).
- The coping behaviour is evidence of a gap: about 50 reviews (keyword) recommend the browser or desktop instead of the app ("Don’t use the app- use website instead", US, 2026-06-28). Most of these are ad-driven.

**Price. Strength: moderate (about 37 reviews).** The subscription is called too expensive or the wrong model. "I would consider paying to support them if it was a one time fee instead of a predatory subscription" (CA, 2026-03-07). "Would consider a one off payment to switch them off but 3 quid a month / 25 a year is laughable for what it is" (GB, 2024-07-11). Only 8 reviews say they would pay under some condition; one pays: "So good I pay for a subscription" (GB, 2026-05-15). Another reviewer says it only links one service and "there is nothing proprietary here" (AU, 2026-04-19).

**Love: free.** Press and blogs praise that it is free and needs no Spotify Premium ([Vice](https://www.vice.com/en/article/music-league-spotify/): "you don’t have to pay a dime for Music League"; date shown by the fetch tool as 2026-02-04, not verified).

**Maker's position.** The 2.0 post promises "fewer, less disruptive ads" ([news post](https://next.musicleague.com/news/why-we-rebuilt-music-league)). No 2.0 player verdict exists yet.

### 2. Reliability, sign-in and Spotify connection

**Hate. Strength: strong (about 95 keyword hits; 46 of 123 in 2025).**
- Missed deadlines because of errors: see the GB 2025-04-03 quote above. "Every weekend the app gives me an error and I can’t participate in the round if I haven’t done it beforehand… the error lasts a week even if I uninstall the app several times" (ES, 2025-04-20).
- Playlist generation fails: "none of my playlists are generating even when I try to force it" (US, 2025-11-08); "Always unable to generate playlists without it bugging out. Constantly have to make new leagues" (GB, 2026-06-08).
- Login loops (16 reviews, 9 in 2025): "it will sporadically log me out and then be completely unable to log me back in" (US, 2025-10-20). "Authentication - failed to retrieve user" (GB, 2025-06-12).
- Spotify link breaks: "Spotify integration no longer works with iOS 18.1.1" (US, 2024-11-29); notification problems because "the Spotify connection breaks when the app is closed" (US, 2024-07-22).
- Round overran its own deadline, three rounds in a row, with no manual start of voting (US, 2025-11-10).
- Startup crashes after updates: v1.2.3 (US and CA, 2025-09-28).

**Reading.** In a game built on deadlines, a bug converts to a lost round and lost social standing. The 2.0 post says reliability was a reason for the rebuild; no beta evidence exists.

### 3. Music-service lock-in (Spotify only, free-tier friction)

**Hate / ask for. Strength: strong (about 30 reviews).** Apple Music about 15, YouTube or SoundCloud 5, Amazon 1, Qobuz 1, "other platforms" general about 8. Every year from 2022 to 2026 has at least 2.
- "This app is useless if your friends don’t have Spotify" (US, 2025-09-18, 3★).
- "half of us use Apple Music so we have to remake the playlist there" (US, 2023-07-13).
- Drop-out: "this app not supporting Apple Music users is what made me decide to stop playing and delete the app" (US, 2026-02-16); "this app is the only reason I have Spotify installed" (US, 2023-06-10).
- YouTube: "this needs to start accepting links from Youtube and Soundcloud!" (US, 2024-07-23). A blogger: "I maintain that its biggest crime is being tied to Spotify" and "YouTube has fucking _everything_" ([Affectionate Discourse, 2025-11-29](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)). A separate Google Play reviewer is reported to say a league would move to any cross-platform alternative (via search summary, not verified).
- Free Spotify friction, 4 reviews: "Now you cant even listen to the song previews on the playlist. Must log in and the playlist is on shuffle only" (US, 2025-07-25); extra songs added to playlists that nobody picked (US, 2022-03-27 and 2024-02-21).
- Press: "The downside is that Music League only works with Spotify" (Vice, as above); Hofstra Chronicle (2026-11-03, via search summary, not verified) says login now works via Spotify or Apple Music.

**Alternatives respond.** BandJam, DJ League and Aux Battles advertise Spotify plus Apple Music or YouTube. A BandJam reviewer: "Also a YT music user, thank you !!" ([App Store US, 2026-02-07](https://itunes.apple.com/us/rss/customerreviews/page=1/id=6756460555/sortBy=mostRecent/json)).

### 4. What players love

**Love. Strength: very strong (as a theme), but broad.**
- **Connection with friends, family, colleagues, long-distance friends (about 124 keyword hits).** "this has been such a good way for our long distance friendship group to stay in touch each week" (AU, 2023-03-17). "This is a great way to learn more about your coworkers without using forced fun" (US, 2024-02-23). Also, per the blog press, play-in-your-own-time: Lancaster Online columnist liked it (via search summary, not verified).
- **Discovery (about 45).** "Got roped into this with my friends and it’s got me to explore new music" (US, 2026-10-29). "super helpful to combat the Spotify algorithm sheep disease" (US, 2026-11-12). [Vice](https://www.vice.com/en/article/music-league-spotify/): "it has me listening to all kinds of music I never would’ve heard of, all thanks to my friends."
- **Competition and banter (about 35).** "the voting can be brutal but fun, and the banter between friends in the rounds is great" (US, 2023-08-20). The Substack reviewer: "The real metagame of Music League is in the commenting and the forum side-discussion."
- **Flexibility of rules (about 14).** "If you want something more competitive, alter the rules to do that. If you want something chill, you can do that too" (US, 2023-07-13). Customisation was praised in the Spanish review of a family Eurovision-style league (ES, 2022-05-14).
- **Simplicity.** "i like that the app is simple and there’s no extra bells and whistles" (US, 2025-04-27).
- **Counter-voice, single.** "The average person has a horrible taste in music… Only discovered like 4 great songs after seeing way over 200" (US, 2025-06-23).

### 5. Voting and scoring rules

**Strength: moderate in count (16 keyword hits, about 8 real), mostly 2022-2025.**
- Forced downvotes: "downvotes are optional… loads of games now where songs in a round don’t deserve any downvotes, but are forced into being downvoted" (GB, 2023-11-08); same ask in CA 2022-05-15. Forced to spend all points: "you’re forced to use all the points when rating a song. In my opinion, this distorts the final result" (DE, 2025-05-24).
- The opposite request, single: "PLEASE let us give negative points" (CA, 2025-02-25). A blogger found one-up-one-down "a maddeningly limiting scoring method" and advises "high vote allotments" with optional downvoting.
- Repeat artist ("orange boxing"): "Please make it an option to disallow orange boxing when creating the league" (AU, 2026-05-10); also US 2026-10-21. 2 reviews, both 2026, the term is community slang.
- See comments before voting, 2 reviews (CA 2023-01-29, US 2023-01-10): "There’s been times I may have voted for the song knowing what it meant to the person submitting it."
- Duplicate filters at admin level (US, 2023-01-10); standardised points per round (US, 2022-04-12), single each.
- Reading: no player asks for a different scoring model. The asks are about optionality and admin control, which 2.0 now has (study 01).

### 6. Guess who submitted it (a bonus mode)

**Ask for. Strength: moderate (6 asks in ML reviews, 2022-2026; plus 2 positive mentions of guessing).**
- "the ability to earn points by correctly guessing who submitted which song! That’s half the fun tbh" (US, 2023-02-27).
- "we like to try to guess who submitted which song. It would be nice if there was a built in feature that tracked correct guesses!" (US, 2022-02-17).
- Same ask: US 2022-04-12, 2023-01-27, AU 2023-03-17, US 2026-06-01. Evidence people already play it by hand.
- Competitors ship it: BandJam ("Right guesses score bonus points"), DJ League ("Earn extra points for guessing who submitted each song!") on their own pages, and a BandJam reviewer: "Guessing who is submitted is so fun" (US, 2026-02-07).

### 7. Pace and deadlines

**Hate / ask for. Strength: moderate (about 8 real mentions of 24 keyword hits).**
- Dead time after everyone has acted: "if everyone has submitted a few hours before the deadline, it should go straight to the voting phase" (CA, 2023-01-29); "now rounds won’t skip early when everyone votes. This ruined the app" (US, 2026-06-09); "the countdown for rounds needs to be like hours not days" (CA, 2026-02-27).
- Cannot shorten or change pace after creation: "Not being able to shorten them is a fatal flaw" (US, 2025-02-21); "I wish they’d let you update the pace once you’ve set up a league" (US, 2024-01-09).
- Counter-view: a blogger advises "Stick to rigid timings," since flexible deadlines were hard for players.
- Reading: pacing is a per-group preference, so admin-chosen. Study 01 shows 2.0 offers Steady, Accelerated and Speedy.

### 8. Social features, invites and discovering leagues

**Ask for. Strength: moderate (about 15 reviews, 2022-2026).**
- Chat: "Chat needs a reply and reaction features" (US, 2026-04-13); "a more robust in-league chat that allows pictures, gifs, or videos" (US, 2026-07-13); "@all function in the chat" (2023-11-08). Several leagues already run a side group-text: "We created a group text chat on our phones and send massages back and forth all day about it" (US, 2023-06-09).
- Friends list, follow, profile: "Being able to follow/connect/friend other players would be cool" (US, 2026-07-13); "A social media element would kick it up a notch, like a friends list" (US, 2023-01-19); show completed leagues on profile (US, 2025-04-27); different name per league (US, 2022-04-14).
- Invite friction: "I want to EASILY invite my friends to play but there isn’t a share/invite button that is obvious" (US, 2025-02-27); "open a league invitation in an unrelated browser AND be prompted to sign-in" (US, 2025-06-28). 4 reviews.
- Finding leagues: "being able to search all open leagues" (GB, 2025-08-26); follow a league without joining (US, 2022-10-23 and 2025-11-05).
- Where public leagues are weak: "The open (public) leagues are primarily comprised of AI bots and fake profiles" (US, 2024-07-02). Single claim, not verified.
- Music League's side: chat and follow/block exist in 2.0, direct messages and friending are "not available yet" (study 01).

### 9. League admin tools and customisation

**Ask for. Strength: weak to moderate (about 8 reviews).**
- Scheduling is the sore spot: "The admin side of things has a terrible user interface. Scheduling rounds specifically… if an admin wanted to swap the order of rounds, it’s very difficult" (US, 2026-02-21); "I tried to add an extra round to my league and it extended my current round by 2 days" (US, 2025-02-21).
- Custom banner or cover image: US 2024-06-15, ES 2024-12-29, US 2026-02-21. 2.0 adds custom league artwork.
- Others, single each: hide upcoming rounds (DE 2025-01-04), a "literalness" meter for prompts (US 2025-01-22), more than 100 rounds (US 2025-03-06), clearer onboarding (US 2026-05-21), a better theme set (FR 2025-02-14: "Le thèmes par défaut sont globalement mal formulés").
- The mobile app lacks admin functions the website has: a reviewer could change deadlines "only… by accessing the website" ([Vice](https://www.vice.com/en/article/music-league-spotify/)); "Lots of discrepancies between things you are able to do on the desktop site vs the app" (CA, 2026-10-14).

### 10. Accessibility (screen readers)

**Hate. Strength: weak in count (3 reviews, 3 years), severe in effect.**
- "I am a blind user with voiceover… multiple voiceover users who are using the app and the website, And they have to rely on a sighted person to enter each league prompt" (US, 2025-04-21).
- "I can not double tap to activate each round in order to submit my song, vote or open playlists" (US, 2026-09-26). Also US 2023-08-15.
- Not verified for 2.0.

### 11. In-app listening, UI and dark mode

**Strength: weak (about 6 listening, about 3 dark mode, about 8 on look and feel).**
- Preview inside the app: "the ability to play previews of songs in-app. As of right now, submitting an unpopular song is kind of a 'death wish' points-wise. I think people would be more motivated to actually listen to all the songs" (CA, 2023-07-26); "sería genial poder escuchar las canciones directamente sin abrir Spotify" (ES, 2024-12-29). The web has sample streaming, the app does not (DE, 2026-02-09).
- Dark mode: "Features desperately needed 1. Dark Mode 2. Apple Music Support…" (US, 2026-04-13); also 2022-04-19, 2026-02-26.
- Mixed on design: "This app is ugly. The clipart is cheap" (US, 2022-04-19) versus "Whomever your UX designers are, please give them a huge kuddos" (US, 2025-01-20). No stable pattern.

### 12. Recaps, stats and notifications

**Strength: weak (about 9 and about 4).**
- "after a season you break down what genre someone used most, or how long their average song was… Give everyone a neat little recap of their season to share" (US, 2023-05-11). Music League 2.0 has Year in Review (study 01).
- Notifications: irrelevant ones, unreliable push, hard to stop emails (GB 2023-04-28, US 2024-07-22, CA 2026-07-14).

### 13. Privacy and data

**Hate. Strength: weak (about 6).** "Fun app, but will scan your contacts and spam them" (AU, 2025-03-12); "They sell your data to thousands of companies" (US, 2025-10-22). Both are reviewers' claims, not verified.

### 14. The alternatives: what the little evidence says

All counts are tiny; read as hints, not evidence.
- **BandJam** (iOS, Android, web; 16 US ratings, 4.75): 5 US written reviews. Praise: "having no ads is a plus"; "FAR better than the competition"; asks: "a way to cap the rounds of a Crew Bucket-based league". Both of two reviewers who say anything on adoption write "Just needs more users" / "Pls need more users" ([feed](https://itunes.apple.com/us/rss/customerreviews/page=1/id=6756460555/sortBy=mostRecent/json)). Page claims: free, no ads, Spotify/Apple/YouTube, guess-who bonus, chat replies/reactions/GIFs ([bandjam.app](https://bandjam.app/)).
- **YapZap** (2 reviews): "has been a great way for us to recommend music to each other", but "the app is very clearly coded with AI, and could really use a professional designer… Things can be hard to find, unclear, or just ugly" ([feed](https://itunes.apple.com/us/rss/customerreviews/page=1/id=6748430650/sortBy=mostRecent/json), US, 2026-08-03).
- **DJ League** (2 ratings, no text), **Cut Club** (6 ratings, no text), **AuxBattle** (2 ratings; I could not confirm it is the same product as auxbattles.app), **songbattle.io** (Giant Bomb 0 user reviews; RAWG one comment: "Liked before it became a hit"): no player voice. Their own sites make claims: Aux Battles "free with no paid tier", "None" accounts, "About 4 minutes a round" ([compare page](https://auxbattles.app/compare)); Cut Club "every round contributes to a season" ([blog](https://www.playcutclub.com/blog/music-league-vs-cut-club-which-music-game-is-better-in-2026)). Vendor marketing, not player evidence. songbattle.io's own page claims 349,645 games played (not verified; search summary).
- **Cold start is the shared theme.** Alongside the two BandJam comments: "hay pocos usuarios" about Music League itself (ES, 2024-12-29) and "Need more people to join and start leagues stat!" (US, 2026-05-21).

## Evidenced vs guessed gaps

"Music League today" is taken from [study 01](music-league-today.md) (2.0 help center, read 2026-11-22), not re-verified here. "Evidence" is this study's.

| Gap or idea | Music League today | Evidence in this study | Verdict |
|---|---|---|---|
| Mobile experience without punishing ads, results visible at once | Free with ads, Premium $2.99/month or $14.99/year; 2.0 promises "fewer, less disruptive ads" | very strong: 283 reviews, escalating complaints since late 2022, admitted by the maker | **Evidenced.** Whether 2.0 closes it is open |
| Reliable submit and vote near deadlines | 2.0 says it fixes reliability; beta unrated | strong, 95 reviews, peak 2025 | **Evidenced for 1.0**, unknown for 2.0 |
| More than Spotify and Apple (YouTube Music, others) | Spotify and Apple Music only | strong for "other services" (about 30); YouTube alone about 5 | **Evidenced** for Apple (now fixed), moderate for YouTube |
| One-time price instead of subscription | Subscription only | moderate: about 37 price mentions, 8 conditional | **Partly evidenced**; no proof anyone would pay |
| Optional downvotes, no forced spending, no repeat artists, early close | 2.0 has these settings | moderate, 2022-2026 | **Evidenced and already answered** in 2.0 |
| Guess-who-submitted bonus | Not in the 2.0 docs I read | moderate: 6 unprompted asks plus 2 competitors ship it | **Evidenced, small** |
| Chat reactions and replies, friends or follow, easier invites, find leagues | Chat, follow and block exist; DMs and friending "not available yet" | moderate: about 15 | **Evidenced, partly answered** |
| Accessible app (screen reader) | Not stated for 2.0 | weak count, severe effect, 3 reviews | **Evidenced, small, unverified in 2.0** |
| Admin scheduling UI, cover images, round reordering | Artwork and breaks added in 2.0 | weak to moderate, about 8 | **Partly evidenced** |
| In-app song preview | Not stated for 2.0 | weak, about 6 | **Weakly evidenced** |
| Dark mode | Not verified for 2.0 | weak, 3 | **Weak** |
| Season recaps, stats, mega playlists | Year in Review; The Charts | weak, 1-2 asks | **Weak or guessed** |
| Cold start: help new groups find enough players | Public leagues and Discover; public leagues reported as thin or bot-filled (1 claim) | weak: 3 mentions of "needs more users" for small apps, 1 for ML | **Guessed for ML**, plausible for any new entrant |
| Live, daily or synchronous formats | Asynchronous, deadline-based | none in 458 reviews | **Guessed**: no player of the existing game asks for it; people who want it would not be in this sample |
| Season-long standings and rivalries (Cut Club pitch) | Not a league-level feature in the docs I read | none from players | **Guessed**: vendor claim only |
| No account, browser-only, Twitch (Aux Battles, songbattle.io) | Accounts required | none from players | **Guessed**: vendor claim only |
| Video, movie or album variants | Songs only | 1 ("You should do a movie one too") | **Guessed** |

## Open questions

1. What does r/musicleague say? This is the largest missing source: it would test every row above, especially the 2.0 beta, bots in public leagues, and rule fights. It needs a method that works from this setup or a human with a browser.
2. How does the 2.0 beta land? The apps and the web reviews in this sample are all about 1.x. Check Feedback emails and TestFlight comments, or revisit after the beta.
3. Does the ad wave drive churn, or only noise? The sample shows people finishing leagues, then leaving. A cohort view (league starts per month) is not public.
4. Is the 4.65 or the 2.4 the truer picture? Ratings (4.65, 6,586) and written reviews (about 2.4 average, 481) disagree; Google Play sits about 3.2-3.3. A product bet that rests on "people are fed up with Music League" should use the ratings with care.
5. Would a second service really bring players, or only keep existing ones? Apple Music asks are from people already in leagues; no evidence on people who never joined because of it.
6. Do players want more rules or fewer? Both directions appear (optional downvotes versus negative points; rigid versus flexible deadlines), which points to admin-set rules, not a single best default.

## Sources

App Store (the feed is the only per-review URL; reviews have no individual links). Reviews cited as "(country, date)" in the text are from these feeds, page 1 to 10 of each:
- Music League: [US](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), [GB](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), [CA](https://itunes.apple.com/ca/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), [AU](https://itunes.apple.com/au/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), [DE](https://itunes.apple.com/de/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), [ES](https://itunes.apple.com/es/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), [FR](https://itunes.apple.com/fr/rss/customerreviews/page=1/id=1589815321/sortBy=mostRecent/json), IT, NL (same pattern)
- Ratings and version: [iTunes lookup](https://itunes.apple.com/lookup?id=1589815321&country=us)
- Review aggregator: [mwm.ai](https://mwm.ai/apps/music-league/1589815321) (rating 2.4, 481 reviews; star split)
- Alternatives: [BandJam feed](https://itunes.apple.com/us/rss/customerreviews/page=1/id=6756460555/sortBy=mostRecent/json), [YapZap feed](https://itunes.apple.com/us/rss/customerreviews/page=1/id=6748430650/sortBy=mostRecent/json); app search ids via the [iTunes search API](https://itunes.apple.com/search?term=BandJam&entity=software&country=us)

Music League itself:
- [Why We Rebuilt Music League, 2026-11-12](https://next.musicleague.com/news/why-we-rebuilt-music-league)
- [Publisher Showcase: Music League (Nitro), 2026-09-28](https://blog.nitropay.com/publisher-showcase-music-league/)
- [Study 01, Music League today, verified](music-league-today.md)

Press, blogs, forums:
- [Vice, Music League Is Wreaking Havoc on My Spotify Reccs](https://www.vice.com/en/article/music-league-spotify/) (publication date shown 2026-02-04, not verified)
- [Affectionate Discourse (Substack), Music League: The Definitive Review, 2025-11-29](https://affectionatediscourse.substack.com/p/music-league-the-definitive-review)
- [Hacker News thread, 2021-05](https://news.ycombinator.com/item?id=27186064) (landing page critique; maker replied; old, pre-app)
- [GuitarNutz 2 forum thread, 2023-03](https://guitarnuts2.proboards.com/thread/10254/music-league)
- Not opened by me, claims taken from search summaries: [Hofstra Chronicle, 2026-11-03](https://thehofstrachronicle.com/115848/features/app-review-music-league/), [Headphonesty, 2024-04](https://www.headphonesty.com/2024/04/tired-music-streaming-try-music-league/), [Lancaster Online](https://lancasteronline.com/features/entertainment/music-league-connects-friends-across-the-country-with-song-prompts-unscripted/article_78635ece-1c45-11ee-b819-bbe7e1669a55.html), [Google Play listing](https://play.google.com/store/apps/details?id=com.musicleague.app&hl=en_US), [AppBrain](https://www.appbrain.com/app/music-league/com.musicleague.app), [ILX thread](https://www.ilxor.com/ILX/ThreadSelectedControllerServlet?boardid=41&threadid=115341)

Competitors (vendor pages, claims only):
- [BandJam](https://bandjam.app/), [DJ League](https://djleague.app/), [Aux Battles compare](https://auxbattles.app/compare), [Cut Club blog](https://www.playcutclub.com/blog/music-league-vs-cut-club-which-music-game-is-better-in-2026), [songbattle.io](https://songbattle.io/)
- Third-party listings for songbattle.io: [Giant Bomb](https://www.giantbomb.com/songbattleio/3030-90559/), [RAWG](https://rawg.io/games/songbattleio) (search summary, not verified)

Not reached: Reddit (all endpoints), Google Play review text, Discord, Twitch, social media comments.
