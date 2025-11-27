# Architecture – Thirty Birds Meeting Companion

_This document will evolve alongside implementation. Initial ideas and options only._

## Draft Principles

- **In-room first**: Optimize for a single physical room with a shared display and microphone.
- **Offline-capable core**: Timers, agenda, and roundtable logic must work without network.
- **Pluggable AI**: Transcription and LLM-based features are optional modules.

## Chosen Tech Stack (Initial)

For **Phase 1 – Core Companion (no AI)** the goal is a simple, reliable setup that can run on a laptop connected to a screen in the meeting room.

### Frontend

- **Framework**: React + TypeScript
- **Bundler/Dev tooling**: Vite
- **State management**: React context + hooks (no heavy global state library initially)
- **Styling**: CSS modules or a lightweight utility framework (e.g. Tailwind CSS) with a focus on high-contrast, large-text layouts.

The frontend will provide:
- A **facilitator UI** (meeting + agenda configuration, controls).
- A **full-screen companion view** (timers, agenda, speakers) that can run in a separate browser window or tab.

### Runtime Model

For Phase 1, the application will be a **pure web app** served locally:
- Option A: `npm run dev` / `npm run build` served via a simple static file server.
- Later Option: wrap the same web app in a desktop shell (e.g. Tauri/Electron) if needed for nicer full-screen control and local file access.

### Persistence

For Phase 1:
- **Local persistence only**, using browser storage:
  - IndexedDB (via a small helper library) or localStorage for simpler prototypes.
  - Meeting and agenda data is stored on the facilitator’s machine and can be exported/imported as JSON.
- No separate backend service is required for the core timer/agenda experience.

This keeps installation and operation simple: open the app in a browser on the room laptop and go.

## Future Backend / AI Integration

For **Phase 3+** (audio + AI), we anticipate introducing a small backend that can:
- Connect to speech-to-text APIs or run a local transcription model.
- Call LLMs for agenda alignment / drift detection.
- Optionally provide a central store for session logs and analytics.

Tentative direction:
- **Runtime**: Node.js with a minimal HTTP API (e.g. Express or Fastify).
- **Role**: strictly optional module that the frontend can talk to when AI features are enabled.

The core UI must continue to function without this backend.

### AI Integration Layers (Draft)

- `TranscriptionService`
  - Responsibility: stream audio from the room microphone to either:
    - A cloud STT provider (e.g. Deepgram, Gladia), or
    - A local model (e.g. Whisper) running on the same machine.
  - Guarantees: provides a simple text stream (chunks of transcript with timestamps) to the rest of the system.

- `AgendaAlignmentService`
  - Responsibility: periodically take:
    - Recent transcript text.
    - Current `AgendaItem` description and keywords.
  - Then call an LLM to compute a small, structured result (e.g. `on_topic`, `risk_of_drift`, `suggestion`).
  - This result is surfaced only in the facilitator view as a hint, never as a hard rule.

- `Prompting / TTS Layer`
  - Responsibility: convert simple text prompts (\"30 seconds remaining\", \"Time is up\") into:
    - Short sounds, or
    - Local or cloud-based text-to-speech.
  - Must be easily configurable or disabled, to respect different group cultures.

### Privacy and Cost Constraints

- Audio and transcripts should be:
  - Processed locally where feasible, or
  - Sent to external services only with explicit configuration and consent.
- The system should remain usable without any AI keys configured.
- Any cloud-based AI usage should be:
  - Bounded and predictable in cost (e.g. short context windows, low call frequency).
  - Transparent to the facilitator (what is being sent, and why).

## High-Level Components (Phase 1)

- `MeetingManager`
  - Handles list of meetings, creation, duplication and selection.
- `AgendaEditor`
  - CRUD interface for agenda items and roundtable configuration.
- `SessionController`
  - Runs the current session: controls timers and transitions.
- `CompanionDisplay`
  - Full-screen view with current agenda item, timers, and speakers.
- `StorageService`
  - Abstracts saving/loading meetings to/from browser storage or JSON files.

More detailed diagrams will be added as implementation starts.

## Domain Model (Initial JSON Shapes)

These shapes are intentionally simple and designed to be serializable as JSON and stored locally.

```json
{
  "id": "meeting_1",
  "title": "Commission IA – March Session",
  "date": "2025-03-15",
  "groupName": "Entrepreneurs Peer Group",
  "participants": [
    { "id": "p1", "name": "Alice" },
    { "id": "p2", "name": "Bob" }
  ],
  "agenda": [
    {
      "id": "a1",
      "title": "Check-in roundtable",
      "description": "45-second check-in per person.",
      "durationMinutes": 20,
      "type": "roundtable",
      "roundtableConfig": {
        "slotSeconds": 45,
        "speakerOrder": ["p1", "p2"]
      }
    }
  ]
}
```

- `Meeting`
  - `id: string`
  - `title: string`
  - `date: string` (ISO date)
  - `groupName?: string`
  - `participants: Participant[]`
  - `agenda: AgendaItem[]`

- `Participant`
  - `id: string`
  - `name: string`

- `AgendaItem`
  - `id: string`
  - `title: string`
  - `description?: string`
  - `durationMinutes: number`
  - `type: "intro" | "roundtable" | "discussion" | "break" | "closing"`
  - `roundtableConfig?: RoundtableConfig`

- `RoundtableConfig`
  - `slotSeconds: number`
  - `speakerOrder: string[]` (array of `Participant.id`)

- `SessionRun` (runtime-only)
  - `meetingId: string`
  - `startedAt: string`
  - `currentAgendaItemId: string`
  - `currentSpeakerId?: string`
  - `timerState: TimerState`

- `TimerState`
  - `mode: "stopped" | "running" | "paused"`
  - `remainingSeconds: number`

These definitions will be mirrored in the frontend TypeScript types and can later be extended (e.g. for analytics or AI metadata) without breaking the core Phase 1 experience.
