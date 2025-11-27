# Roadmap – Thirty Birds Meeting Companion

## Phase 0 – Documentation & Design
- [x] Create repository and initial docs.
- [x] Finalize problem statement and scope with early users.
- [x] Decide on tech stack (frontend & backend).

## Phase 1 – Core Companion (No AI)
- **Goal**: Run a full 90-minute structured session in a room using only Thirty Birds for timing and agenda visibility.
- **Demo**: Screen recording of a simulated session walking through the 45-second roundtable and multi-item agenda.

- [ ] Implement meeting and agenda models (using the documented JSON shapes).
- [ ] Build facilitator UI for creating/editing meetings and agendas.
- [ ] Build full-screen companion display (timers + agenda) with clear color cues.
- [ ] Implement roundtable mode with per-speaker timers and automatic \"next speaker\" flow.
- [ ] Add basic configuration for colors and sounds suitable for a meeting room.

Suggested pilot target: a real peer-group or commission-style session (e.g. 90 minutes with a 45-second roundtable) within 1–2 months of starting implementation.

## Phase 2 – Persistence & Polish
- **Goal**: Make it practical for facilitators to reuse and iterate on agendas over many sessions.
- **Demo**: Short video showing creation of a meeting, duplication of a past agenda, and small adjustments before running a session.

- [ ] Add persistent storage (local DB or simple backend for exporting/importing JSON).
- [ ] Support multiple meetings, duplication of past agendas.
- [ ] Improve theming and readability in large rooms (font sizes, color themes).
- [ ] Add keyboard shortcuts / remote control for common actions (start/pause, next item, next speaker).

## Phase 3 – Audio & AI
- **Goal**: Offer an optional AI layer that helps the facilitator notice drift and overruns without depending on it for the core experience.
- **Demo**: Live or recorded session where the transcript is visible to the facilitator and subtle AI hints appear when the group drifts off-topic.

- [ ] Integrate a transcription provider (cloud or local).
- [ ] Add optional transcript panel for facilitator.
- [ ] Implement basic drift/overrun detection via LLM.
- [ ] Add configurable audio / TTS prompts.

## Phase 4 – Analytics & Iteration Support
- **Goal**: Help facilitators learn from past sessions and refine their agendas and facilitation patterns.
- **Demo**: Simple report for a past meeting showing planned vs. actual time per item and basic speaking-time distribution.

- [ ] Log planned vs. actual timing per agenda item.
- [ ] Simple visual reports for facilitators.
- [ ] (Optional) Session summary generation via AI.

This roadmap is indicative and will adapt as early prototypes are tested in real peer groups, commissions and agile teams.

## First Pilot & Feedback Loop

- **Target**: one concrete, upcoming session (e.g. a monthly commission or team retrospective).
- **Minimum tool capabilities for the pilot**:
  - Phase 1 features implemented and tested on a dry run.
  - Stable roundtable mode with visible timers and color cues.
- **Feedback collection**:
  - Short post-meeting survey for the facilitator (perceived load, ease of keeping time).
  - Short check-in with participants (clarity of timing, perceived fairness, impact on focus).
  - Notes on technical issues (screen visibility, controls, any confusion).

Insights from the first pilot will feed back into adjustments to the agenda flows, UI and roadmap priorities.
