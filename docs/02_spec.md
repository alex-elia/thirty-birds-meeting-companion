# Functional Specification – Thirty Birds Meeting Companion

_This is a living document; early versions focus on v0 / v1 MVP scope._

## 1. Personas

### 1.1 Facilitator (Primary User)
- Prepares the agenda and roundtables.
- Operates the companion during the meeting.
- Wants to keep time and structure without constantly watching the clock.

### 1.2 Participants
- Sit in the room and see the shared screen.
- Take turns speaking during roundtables.
- Benefit from clear signals about time and progression.

## 2. High-Level User Flows

### 2.1 Create a Meeting
1. Facilitator opens the app (on a laptop connected to the room screen).
2. Clicks **"New meeting"**.
3. Enters basic info: title, date, group name.
4. Defines participants (names, optional seating order).
5. Saves the meeting.

### 2.2 Configure Agenda
1. From a meeting, facilitator opens **"Agenda"**.
2. Adds agenda items with:
   - Title
   - Description / goal (short text)
   - Duration (minutes / seconds)
   - Type (e.g. intro, roundtable, discussion, break)
3. For **roundtable** items, optionally defines:
   - Per-person slot duration (e.g. 45 seconds)
   - Order of speakers
4. Reorders items via drag and drop.
5. Saves agenda.

### 2.3 Run a Session
1. Facilitator clicks **"Start session"** for a meeting.
2. App switches to **"Companion Display"** mode (full-screen UI):
   - Shows current agenda item, remaining time, and next items.
   - Displays a large central countdown.
3. Facilitator can:
   - Start/pause/reset current timer.
   - Skip to next/previous agenda item.
   - Toggle between **agenda mode** and **roundtable mode**.

Simple flow (textual wireframe):

```text
[Facilitator Control Panel]            [Companion Display – on big screen]

Left: Agenda list                      Big center: Remaining time
  - Intro (5 min)                      Top: Current agenda item title
  - Roundtable (20 min)                Bottom: Next item(s)
  - Discussion (40 min)

Right: Controls
  [Start] [Pause] [Next item]
  [Switch to Roundtable mode]
```

### 2.4 Roundtable Mode
1. For a roundtable agenda item, the screen shows:
   - List of participants, with the **current speaker** highlighted.
   - A big countdown for the current speaker's slot (e.g. 45 seconds).
2. Facilitator clicks **"Start roundtable"**.
3. System:
   - Starts countdown for Speaker 1.
   - At thresholds (e.g. 15s left, 0s), changes colors (green → yellow → red) and optionally plays a short sound.
   - When time is up, can automatically move to the next speaker after a configurable grace period.
4. Facilitator can:
   - Manually skip to next speaker.
   - Add or remove speakers on the fly.
   - Extend or shorten a slot in exceptional cases.

Textual wireframe for roundtable:

```text
[Facilitator Control Panel]            [Companion Display – Roundtable]

Left: Participant list                 Center: BIG TIMER (45 → 0)
  -> Alice (current)                   Below: Current speaker name
     Bob                               Bottom: Next up: Charlie, Dana
     Charlie
     Dana                              Background color:
                                        - Green (full time)
Controls:                               - Yellow (last 15s)
  [Start slot] [Pause] [Next speaker]   - Red (time over)
  [+ Add participant]
```

### 2.5 Session Wrap-Up (Later Phase)
- At the end of the meeting, the app can present a basic summary:
  - Planned vs. actual time per agenda item.
  - Number of speakers, average speaking time.
  - (Later) Lightweight AI summary of key topics.

## 3. MVP Feature Set – Phase 1 Core Companion (No AI)

Phase 1 focuses on a **fully usable, offline-capable companion** without any AI, transcription, or external APIs. It must be reliable enough to run a real CJD PARIS commission session end-to-end.

### 3.1 Must-Have (Phase 1)
- Meeting creation & basic metadata.
- Agenda creation with items (title, duration, type).
- Roundtable support:
  - Per-person slot duration
  - Fixed order of speakers
- Full-screen companion display:
  - Current agenda item and remaining time
  - Basic timeline of upcoming items
  - Large countdown for agenda items and for per-speaker slots
- Controls for facilitator:
  - Start / pause / reset timer
  - Next / previous agenda item
  - Next speaker in roundtable mode
- Configurable time cues:
  - Color thresholds (e.g. green/yellow/red)
  - Optional short sound when time is up

### 3.2 Nice-to-Have in Early Versions (Still Phase 1)
- Persistent storage of meetings & agendas (local or simple DB).
- Basic theming (light/dark, font sizes for readability in a room).
- Keyboard shortcuts / remote control support.

## 4. AI & Audio Features – Phase 3+

### 4.1 Live Transcription Integration
- Input: audio stream from a room microphone.
- Service: external STT API (e.g. Deepgram, Gladia) or local model (e.g. Whisper).
- UI: small transcript area for facilitator view (may be hidden from main display).

### 4.2 Agenda Alignment & Drift Detection
- For each agenda item, facilitator can define:
  - A short description (1–3 sentences).
  - A few keywords / themes.
- Periodically (e.g. every 30–60 seconds), the backend:
  - Sends recent transcript segment + current agenda description to an LLM.
  - Receives a simple assessment, e.g.:
    - `on_topic` (0–1)
    - `risk_of_drift` (0–1)
    - Short suggestion for facilitator.
- If drift or overrun is detected:
  - The facilitator view can show a subtle suggestion (e.g. "We are drifting from X; consider wrapping up").

### 4.3 Audio Prompts
- Use text-to-speech (TTS) or simple sounds to:
  - Announce start or end of a slot.
  - Gently say "30 seconds remaining" or "Time is up".
- Prompts should be configurable and optional.

## 5. Flagship Demo Scenarios

To guide product and UX decisions, the following demo scenarios should be explicitly supported by Phase 1:

1. **45-second roundtable for 16 entrepreneurs (CJD commission style)**
   - Setup: one meeting with 16 participants, a “tour de table” agenda item configured as a roundtable with 45-second slots.
   - Outcome: the facilitator can run the entire roundtable from the tool (start, next speaker, clear visual cues) without touching an external timer.

2. **90-minute commission meeting with 5 agenda items**
   - Setup: agenda with intro, roundtable, 2 thematic discussions, and a closing segment, each with clearly defined durations.
   - Outcome: the facilitator can see where they are in the agenda at all times, stay roughly on time, and adjust transitions using the controls.

3. **Ad-hoc adjustment during a live session**
   - Setup: while running a session, the group decides to shorten one upcoming item and lengthen another.
   - Outcome: the facilitator can adjust durations on the fly without breaking the timers or losing track of the flow.

These demo scenarios will also be used for early screen recordings and live pilots.

## 6. Non-Functional Requirements

- **Latency**: Visual timers must update smoothly (e.g. 60 FPS rendering target on the frontend).
- **Reliability**: The core timer/agenda features must work offline (no internet, no AI) – AI is additive.
- **Privacy**: Audio and transcripts should not be stored or sent externally without clear configuration and consent.
- **Simplicity**: UI should be readable from across a room (large fonts, high contrast, minimal clutter).

## 7. Open Questions

- Do we support multiple concurrent meetings (multi-facilitator usage) in the same instance?
- How much historical data should we keep for analytics?
- How configurable should roundtable patterns be (mixed-length slots, grouped speakers, etc.)?

These will be refined as the architecture (`03_architecture.md`) and early prototypes take shape.
