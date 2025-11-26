# Problem Statement – Thirty Birds Meeting Companion

## Context

Facilitators of peer groups and commissions (e.g. groups of ~16 entrepreneurs meeting monthly in a physical room) often run **time-boxed, structured sessions**:
- Roundtables with strict speaking time per person (e.g. 45 seconds each)
- Sequences of agenda items with fixed durations
- The need to balance rich discussion with hard time constraints

These sessions are usually **hybrid in nature over the year** (sometimes remote, sometimes in-person), but the most intense facilitation problems tend to appear **in-room**, where energy, interruptions and group dynamics are highest.

## Core Pain Points

1. **Time overruns during roundtables**
   - Each participant is given a fixed slot (e.g. 45 seconds), but many exceed it.
   - The facilitator must constantly watch the clock and interrupt speakers.
   - This creates stress for the facilitator and sometimes discomfort in the group.

2. **Agenda drift**
   - Discussions naturally deviate from the planned topic.
   - The facilitator has limited cognitive bandwidth to both participate and steer.
   - Important items later in the agenda are rushed or skipped because earlier items went long.

3. **Manual, fragile tooling**
   - Timers on phones or generic countdown apps are not integrated with the agenda or speaker list.
   - There is no shared, always-visible view of time and agenda for all participants.
   - Notes, transcripts and timing logs are scattered and hard to reuse.

4. **Facilitator cognitive load**
   - The facilitator is simultaneously:
     - Watching the clock
     - Tracking who spoke and who has not
     - Listening for content quality and topic relevance
     - Managing group energy and fairness
   - This reduces their capacity to contribute substantively to the discussion.

## Why Existing Tools Fall Short

- **Remote-first meeting tools** (e.g. advanced Zoom/Meet add-ons, async meeting SaaS) focus on online/hybrid flows and are tightly coupled to video platforms.
- **AI note-takers** (e.g. Otter.ai, Fireflies) produce transcripts and summaries, but they are **passive**: they do not actively manage timeboxes or agenda adherence.
- **Generic countdown or speaker timers** provide visual time, but:
  - They are not agenda-aware.
  - They do not integrate with transcription or AI to detect drift.
  - They rely entirely on the facilitator to drive transitions and enforcement.

There appears to be a gap for a dedicated **in-room, agenda-aware, AI-augmented meeting companion**.

## Problem Definition

> Build an in-room "meeting companion" that acts as a **co-facilitator** for structured, time-boxed meetings. It should make time visible and fair, help enforce speaking slots, and gently nudge the group back to the agenda when discussions drift.

Specifically, the system should:

1. **Make time and structure visible to everyone in the room**
   - Show the current agenda item, remaining time, and next steps on a shared screen.
   - Provide clear visual cues (green/yellow/red) for time usage.

2. **Support strict roundtable slots**
   - Configure per-person time (e.g. 45 seconds) and order.
   - Automatically advance the timer and highlight the next speaker.
   - Provide soft but clear end-of-time signals (sound, TTS prompt, visual change).

3. **Reduce facilitator micro-management**
   - The system runs the timers and transitions; the facilitator focuses on people and content.
   - AI assistance can warn when a segment is overrunning or off-topic compared to the agenda.

4. **Preserve useful traces of the discussion** (later phases)
   - Optionally log timing, basic transcript segments and agenda coverage to help facilitators iterate on session design.

## Constraints and Assumptions

- **In-room first**: Initial versions assume one physical room with:
  - A dedicated computer (laptop, mini PC, etc.).
  - A shared display (screen or projector).
  - A good-quality conference microphone.
- **Privacy-conscious**: Where possible, audio and transcripts should be processed locally or with clear, explicit consent if using external APIs.
- **Facilitator-in-control**: AI features provide suggestions and cues; they do not replace human judgment.

This problem statement will guide the functional specification (`docs/02_spec.md`) and architecture discussions (`docs/03_architecture.md`).
