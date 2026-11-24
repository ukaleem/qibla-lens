---
status: draft
---

# Design brief: Qibla Lens

<!-- Filled in by plan-lens from the learner's interview. Use the learner's words. Mark any value they didn't choose as (default). -->
<!-- Drafted 2026-11-24 by Muse from Kaleem's standing rule: pick the best defaults, don't ask open questions. Awaits his yes/no sign-off before the build. -->

## The one spatial moment
You stand in your room, about to pray. You put on the glasses and a soft glowing arrow lies on the floor in front of you, pointing the way to Makkah, with today's prayer times floating beside it at a glance. No phone in your hand, no guessing the direction — you face the arrow, and you pray.

## Why it belongs on glasses
- Uses: shares your view, draws in the world, leaves your body free
- Why it's better than the phone or laptop version: a phone compass makes you look down at a screen and hold the phone flat while you turn; the Lens puts the direction in the room itself, at real scale, so your eyes stay up and your hands stay free. The arrow lives on your floor, not on a screen.

## Product or overlay
- Type: overlay: it responds to a real place (Makkah) and real times (today's prayers)
- What the real version would sense: compass heading plus GPS position, to compute the true Qibla bearing; live prayer times for the user's city
- Stand-in for the preview: a "Set my direction" button. Pressing it places the arrow using a hard-coded bearing (267.7° from Karachi, the default location) and hard-coded sample prayer times for Karachi. A compass rose drawn on the floor shows which way is north in the preview room. Build what happens after the direction is set for real.

## Where things live
- Where the user is looking during the main task: down and ahead, at the floor about 1 m in front of them, where the arrow lies
- Qibla arrow: lies flat on the floor, starting about 60 cm ahead and running about 1.2 m long toward Makkah; glowing light-green chevron, wide enough to read at a glance (about 25 cm wide), with a small Kaaba marker at its far end
- Compass rose: flat on the floor under the arrow's start, about 40 cm across, showing N/E/S/W so the direction is verifiable
- Prayer-times panel: floats about 1.1 m ahead, a little below eye level, about 50 cm wide; five rows (Fajr, Dhuhr, Asr, Maghrib, Isha) with the next prayer highlighted; light text on a dark panel (additive display: no black backgrounds relied on for visibility)
- Next-prayer chip: small, next to the arrow's start, showing the next prayer name and time in large text

## Hands and input
- Find Qibla (big button, centre of view at start): pinch to place the arrow and compass rose
- Prayer-time rows: pinch a row to expand it into a small countdown ("Maghrib in 1 h 24 m")
- Prayer mode (big button on the panel): pinch to hide everything except a small direction marker at the floor's edge, so nothing distracts during prayer; pinch again to bring the panel back
- Targets are big and highlight when aimed at.
- Voice (if any) and the button that does the same job: none — every action has a pinch button, since voice may not work in the preview

## When things show
- Find Qibla button: shows at start, hides once the direction is set
- Arrow, compass rose, prayer panel: show once direction is set, stay while you prepare
- Prayer mode: hides the panel and shrinks the arrow to a small floor marker; the marker stays until you pinch it to exit prayer mode
- If something needs attention out of view: not needed — everything the Lens shows sits where the user is already looking (the floor ahead)

## Done criteria
Each one can be checked in Lens Studio's preview.
1. Pinching "Find Qibla" places a glowing arrow on the floor pointing 267.7° (west, slightly south) with a compass rose beneath it, and the prayer-times panel appears ahead.
2. The next prayer row is highlighted and pinching any row expands a countdown to that prayer.
3. Pinching "Prayer mode" hides the panel and shrinks the arrow to a small floor marker; pinching the marker brings everything back.
4. Walking around the arrow (WASD + mouse in preview) keeps it anchored to the floor at real scale, readable from where a person stands to pray.
5. All text stays light and readable from 1 m away; nothing relies on black to be seen.

## Out of scope
- Live GPS/compass sensing on real glasses (preview uses the hard-coded Karachi bearing)
- Live prayer-times API (preview uses hard-coded sample Karachi times; real data is a post-hackathon step)
- Qibla for other cities, multiple locations, or a settings screen
- Voice commands, two-hand gestures, or anything needing a second person

## Risks and open questions
- Real bearing accuracy depends on the glasses' compass, which only real hardware can answer — labelled "feel unproven"
- Prayer times in the demo are sample data for Karachi; the video must not claim they are live
- None of the learner's choices were kept against a design concern

## Build notes for CLAD
- Build for SPECS so it runs and can be demonstrated in Lens Studio's preview. No SPECS device is available.
- Use Spectacles Interaction Kit (SIK) and UI Kit for all interactions, so they work with the mouse in Interactive Preview and with LEAF.
- Build any stand-in exactly as described above, and keep it obvious in the scene.
- Use real-world scale in centimeters. Keep content inside the user's view during the main task.
- The display is additive: black renders as transparent. Don't rely on black or very dark content to be seen; keep text light and readable from where the user stands.
- Get the basic flow working first, then add detail.
- Write LEAF scenarios for each done criterion, run them in preview, and report which pass. Say which criteria have no test.
- Don't record, identify, or follow people.

## After the build: judge it
This part is for you, after CLAD finishes.

1. **Does it work?** Ask your agent which LEAF tests passed and which done criteria have no test.
2. **Walk around it.** Open the preview in Interactive Preview. Use WASD to move, Q and E to go down and up, and right-drag (or hold Shift) to look around. Clicking acts as a pinch. Stand where a user would and look at the task.
3. **Ask the three questions.**
   - Does it use what I'm looking at?
   - Does it put something in my space, where it belongs?
   - Does it free my hands or let me keep my eyes up?
   - Would it be just as good on a phone? If so, what would make it need the glasses?
4. **Check comfort.**
   - Everything I need is in view while I do the task. Nothing sits at the edges, behind me, or stuck to my face.
   - Every control is within reach of someone standing there.
   - Text reads easily from where I stand. No dark UI disappearing.
   - Things show when needed and get out of the way.
5. **Label what you know.** Write "logic proven" next to anything the tests and preview show working, and "feel unproven" next to anything only real glasses could tell you (comfort over time, real hand tracking, real recognition).
6. **Fix with design notes, not code.** Tell your agent what to change in design terms, for example: "Move the step card 15 cm lower and next to the pan. Make the Next button twice as big. Re-run the tests." If a fix takes under a minute, like nudging a panel, do it yourself in the scene.
7. **Submit.** Record a video under 3 minutes of your Lens in the preview, public on YouTube. Make your repo public with your Lens Studio project and this `devpost/` folder. Details are on the hackathon site: https://learn-specs.devpost.com/resources
