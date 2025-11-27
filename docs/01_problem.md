# Problem Statement – Thirty Birds Meeting Companion

## Context

Facilitators of peer groups, boards, commissions and agile teams (often 8–20 people) frequently run **time-boxed, structured sessions**:
- Quick “tour de table” moments with strictly limited speaking time per person (e.g. 30–60 seconds each).
- Several themed segments (e.g. deep dives, peer coaching, retrospectives, feedback rounds) with fixed durations.
- A closing phase with next actions and commitments.

Over the course of a year these groups may alternate between in-person and remote sessions, but the most intense facilitation challenges typically appear **in-room**, where:
- Energy is high and people are physically present.
- Side conversations and interruptions are more frequent.
- Time pressure is real because the room booking and members’ agendas are hard constraints.

## Core Pain Points

1. **Time overruns during roundtables**
   - Each participant is given a fixed slot (e.g. 45 seconds in many peer groups), but many exceed it.
   - The facilitator must constantly watch the clock and interrupt speakers, instead of listening deeply.
   - This creates stress for the facilitator and sometimes discomfort in the group (“you always have to cut me off”).

2. **Agenda drift**
   - Discussions naturally deviate from the planned topic.
   - The facilitator has limited cognitive bandwidth to both participate and steer.
   - Important items later in the agenda are rushed or skipped because earlier items went long.

3. **Manual, fragile tooling**
   - Timers on phones or generic countdown apps are not integrated with the agenda or speaker list.
   - There is no shared, always-visible view of time and agenda for all participants.
   - Notes, transcripts and timing logs are scattered and hard to reuse.

4. **Facilitator cognitive load and energy drain**
   - The facilitator is simultaneously:
     - Watching the clock
     - Tracking who spoke and who has not
     - Listening for content quality and topic relevance
     - Managing group energy and fairness
   - This reduces their capacity to contribute substantively to the discussion as a peer, coach, or leader.

Experienced facilitators and agile coaches know that **group focus and energy naturally drop over time**, especially in the second half of a session. Without strong visual structure and support, it becomes harder to keep the public engaged, concise and on-topic without becoming overly controlling.

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

## Desired Outcomes and Success Metrics (v1)

For a first usable version of Thirty Birds Meeting Companion, success can be measured along three axes:

1. **Time discipline**
   - A higher percentage of meetings finish within the planned end time.
   - A higher percentage of agenda items are completed within their timebox.
   - Roundtables with 45-second slots actually stay close to 45 seconds per person on average.

2. **Facilitator load**
   - The facilitator self-reports spending less attention on the clock and more on listening and synthesising.
   - Fewer moments where the facilitator feels forced to “police” time manually.

3. **Perceived fairness and clarity**
   - Participants report that speaking time feels fairer and more evenly distributed.
   - Participants can always tell “where we are” in the agenda and how much time remains.

These outcomes will guide the functional specification (`docs/02_spec.md`) and architecture discussions (`docs/03_architecture.md`), and will be refined after the first real-world pilots with CJD PARIS and similar groups.
