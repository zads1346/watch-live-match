---
name: watch-live-match
description: Observe a user-selected live sports or esports broadcast, including Bilibili rooms, using real browser screenshots; verify team, map, and match scores; report meaningful score changes; capture requested screenshots; and keep watching until the user's stopping condition. Use for requests such as “盯着直播比分”, “每次比分变化告诉我”, “看到半场”, “继续看到比赛结束”, or “截一张现在的画面”. Do not use page metadata, comments, or a stored score as evidence of the current video score.
---

# Watch Live Match

## Establish the watch

- Use the exact room or broadcast supplied by the user. If it is missing, resolve it from the conversation or ask for the link; do not silently choose another broadcast.
- Record the game, teams, desired updates, source, and stopping condition. Distinguish “this map ends”, “halftime”, and “the match/series ends”. Treat a later “keep watching until the match ends” as replacing an earlier halftime stop.
- Confirm whether the requested “score” means rounds/points in the current map or maps/games in the series. If the context establishes both, label both rather than asking unnecessarily.
- Inspect actual available tools and the browser's connection state. Follow the active environment, browser, permission, and messaging instructions. Say whose browser is being used. Route work on the user's computer through the supported delegated task flow.
- Do not assume AgentReach, a browser extension, a video downloader, or any named tool is installed. A skill provides a workflow, not new live-video access. Never claim a tool invocation, continuous video vision, or automatic OCR that did not occur.
- Keep room IDs, account details, credentials, cookies, one-time codes, and private user data out of this reusable skill. Supply the current source and watch state only for the active task.

## Make the real player readable

1. Open the selected source through the supported browser tools and wait for the player to actually render.
2. Inspect the current screenshot before scrolling. Scroll the player into view so the scoreboard and both team names are visible. A page may reset an early scroll while loading; if that happens, wait for loading to settle and scroll again. A Page Down may help, but use the observed layout instead of fixed coordinates or a universal key sequence.
3. If a page banner persistently crowds out the player, inspect supported page/accessibility information for an already exposed embedded-player URL. Opening that verified same-site, same-room player page can simplify the viewport. Do not guess hidden addresses or use this to bypass a login, DRM, access restriction, or denied action. Confirm the match identity and actual playback again after navigation.
4. Dismiss only non-binding overlays when permitted, such as a closeable promotion. Handle sign-in, permissions, security warnings, paid access, and acceptance dialogs under the active confirmation policy.
5. Capture and inspect a fresh screenshot after layout changes. Confirm that the visible numbers belong to the broadcast HUD, not a page title, room description, comment, betting widget, or unrelated match panel.
6. Verify that the player is running: compare separated frames and look for changing game motion, timer, round state, or another reliable progression cue. A room's “live” label alone does not establish a live, advancing match frame.

Do not reconstruct a screenshot from text, generate a plausible image, invent unseen digits, or describe an unobserved frame as captured.

## Establish the baseline from pixels

Read the broadcast HUD and maintain this small task-local record:

- Source: exact verified URL, browser/task, and active match identity
- Observed time: wall-clock timestamp with timezone; keep any on-screen game clock separate
- Team mapping: each team's visible name/logo, screen side, and side/color if relevant
- Current map/game: name or ordinal, and current round/point score by team identity
- Series: map/game score and best-of format, if actually confirmed
- Phase: live play, freeze time, halftime, overtime, replay, intermission, final, or uncertain
- Evidence: screenshot or frame reference, legibility, liveness cues, and known stream delay
- Notification state: last confirmed and last reported scores, phase, and screenshot request
- Watch state: current stopping condition, next observation, and any unresolved blocker

Use two separated, readable observations to establish the baseline and to confirm ambiguous or consequential changes. Do not treat two captures of the same frozen frame as independent confirmation. For an unambiguous ordinary increment on an advancing HUD, report promptly; verify again if a label, number, phase, or orientation is unclear.

Preserve team identity across side swaps. For example, if Team A moves from left to right at halftime, keep its score attached to Team A. Never copy “left score–right score” into a team-named update without rechecking the labels. Re-verify team and map identity at halftime, new maps, overtime, scene changes, and unexpected jumps.

Mark illegible digits as uncertain and get another frame. Do not fill them from comments, expected round outcomes, previous reports, or an external score site. External sources can corroborate identity or format; label them separately and do not substitute them for the requested live picture.

## Decide what a score means

- Separate current-map rounds/points from the series score. “Team A 8–6 Team B on the current map; series 1–0” is different from “Team A leads the match 8–6”.
- Establish the tournament's actual format before deriving halftime or completion from numbers. For a confirmed CS2 MR12 regulation half, twelve completed rounds mark halftime; a 6–6 score can therefore be halftime. Do not apply this rule to another game, an MR15 event, or overtime.
- Verify overtime rules for the event. Do not infer a winner simply because a team reaches 13 or takes a one-round lead after 12–12. Use the final/winner screen or another clear broadcast confirmation, and distinguish a completed map from a completed best-of series.
- Treat a replay banner, highlight montage, old map label, inconsistent timer, or sudden score reversal as a reason to suspend score updates. Keep the last confirmed live score while checking the current scene. If a genuine correction is confirmed, label it as a correction.
- Describe the observed broadcast state, not an assumed real-world instant. Say “observed at 21:07:32 UTC+8”; do not say “right now on the server” unless the delay is actually known. Mention stream delay when material; do not invent its duration.

## Watch and report changes

1. Sample the advancing player at a cadence suited to the game, user request, and available tools. For round-based play, a short interval such as 15–30 seconds can be a starting point; shorten near likely round endings and lengthen during clearly confirmed breaks. Respect service and tool limits.
2. Recheck source identity, liveness, team mapping, and phase before comparing the new observation with the last confirmed one.
3. Compare normalized scores by team identity and by map. Suppress duplicate updates, including visual side swaps and repeated captures. Do not suppress an important phase change merely because the numbers stayed the same.
4. Notify only about requested events: confirmed score changes, halftime/map/series completion, requested screenshots, and material uncertainty or loss of coverage. Do not send a routine “still watching” message on every check.
5. Keep messages brief. Name the teams, map where relevant, and observed score. Include observed time/timezone and the verified source when useful. Clearly label series scores, replay uncertainty, stale evidence, and corrections.
6. After reporting an intermediate result, continue until the user's current stopping condition is positively verified. A halftime update does not finish an instruction to watch until match end. A map winner does not by itself finish a series watch.
7. At the verified stopping event, send the result with the last observed time and stop. Honor explicit cancellation immediately.

Do not promise every round will be caught. Periodic screenshots, broadcast delays, hidden scoreboards, and tool latency can skip intermediate states. If the score jumps from 5–4 to 7–4, report the confirmed latest score and the coverage gap if relevant; do not fabricate two individually observed rounds or their timestamps.

Keep the ongoing watch active across available waits. Use supported waiting/status tools instead of busy polling. Do not invent a time limit that ends an explicit “until the match ends” watch. If the environment cannot continue, report the blocker promptly rather than claiming monitoring remains active. Do not create a recurring scheduled job merely to finish an already-running watch.

## Capture a requested screenshot

- Take a new screenshot from the actual browser when the user asks for “now”. Save that captured frame promptly; do not delay delivery just to obtain a perfect crop.
- Inspect the saved image before sending it. Prefer a frame that contains the HUD and both team labels, while avoiding unrelated private content. If it is partial, obscured, or captured during a replay, state that plainly. Do not call an earlier saved frame current.
- Preserve the original captured pixels. Use a browser-native crop/region capture when available; if a permitted local crop is used, keep the original and label the delivered image as cropped. Do not cosmetically alter scores or use image generation to create screenshot evidence.
- Record capture time with timezone and source. The capture time is not necessarily the time of the underlying match action.
- Follow the host application's supported file-delivery tools. Deliver the real image as a native attachment when supported. Do not replace delivery with a private download URL or a local sandbox path. Verify preparation succeeded before saying the image was sent.
- If capture succeeds but attachment preparation fails, preserve the frame, report the delivery problem, and retry only through a supported authorized path. Do not silently generate a substitute.

## Recover without inventing coverage

Distinguish transient timeouts from access or authorization denials.

- For a transient failure, make bounded, documented recovery attempts using allowed actions, such as checking the current tab once, waiting for the player to settle, or reloading the same source when appropriate. Avoid endless rapid retries and repeated navigation that destroys context.
- If no advancing frame is available, mark the feed stale and retain the last confirmed observation with its timestamp. Repeated identical frames or an unchanged score alone do not prove a frozen feed; assess the motion/timer cues and scene.
- Once recovered, reconfirm match, map, team mapping, and current score. State any material blind interval. Do not claim continuous coverage of the gap.
- Respect access and permission denials. Do not switch tools, origins, network routes, hidden endpoints, or identities to bypass a denied action. Follow the current policy for any evidence-backed retry; never assume blanket approval or prescribe a universal permission workaround.
- If a tool, login, connection, or service blocker persists after the supported recovery paths, report what failed, the last verified score/time, and the smallest necessary next step. Pause only the dependent work; do not call the match finished. Resume only when access or playback is actually restored.

## Short examples

- Score change: “Team A 8–6 Team B on the current map. Observed at 21:07:32 UTC+8 in the linked broadcast; series still 1–0.”
- Halftime: “Halftime: Team A 7–5 Team B. I’ll keep watching until the series ends.” Use the second sentence only when that is the active instruction.
- Screenshot: “Captured at 21:08:05 UTC+8. The lower edge is cropped, but both team names and the score are visible.” Attach the actual image.
- Coverage gap: “The player stopped advancing. Last verified: Team A 9–7 Team B at 21:10:12 UTC+8. I can’t confirm a newer score yet.”
