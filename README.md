# Thirty Birds Meeting Companion

An open-source, in-room AI meeting companion that helps facilitators keep structured, time-boxed discussions on track.

## Vision

Modern working groups (like CJD commissions, boards, and peer circles) often have:
- Strict timeboxes (e.g. 45-second roundtable slots)
- Rich discussions that easily drift off agenda
- A single facilitator who must manage time, energy, and focus

**Thirty Birds Meeting Companion** aims to act as a co-facilitator:
- Clear visual timers and agenda display for everyone in the room
- Per-speaker countdowns (e.g. 45 seconds each) with gentle, configurable cues
- Live transcription of the room (via external APIs or local models)
- AI logic that detects overruns and topic drift relative to the planned agenda
- Visual and/or audio prompts to help the human facilitator keep the group on track

The first versions will focus on **in-room** usage (one physical room with a shared screen and room microphone), not remote video conferencing.

## High-level Features (Road to v1)

- Agenda editor for the facilitator (segments, durations, goals, speaker order)
- Full-screen "companion" display:
  - Current agenda item and next items
  - Speaker name / slot
  - Large, high-contrast countdown timer
  - Color-coded cues (green / yellow / red)
- Roundtable mode (e.g. 45 seconds per person, auto-advancing)
- Local or cloud-based speech-to-text integration
- Optional AI layer for:
  - Topic alignment vs. agenda item
  - Drift / overrun alerts
  - Suggested prompts for facilitator

## Project Structure

Planned structure (may evolve):

```text
thirty-birds-meeting-companion/
├─ README.md
├─ docs/
│  ├─ 01_problem.md
│  ├─ 02_spec.md
│  ├─ 03_architecture.md
│  └─ roadmap.md
├─ packages/
│  ├─ dashboard/   # Frontend UI (e.g. React)
│  └─ backend/     # API + real-time coordination
├─ scripts/
├─ .github/
└─ CONTRIBUTING.md
```

## Status

Early design stage. The repository currently focuses on:
- Documenting the problem
- Rough functional specification
- Early architectural options

Implementation will follow once the first design iterations are stable.

## License

This project is open source under the MIT License. See `LICENSE` for details.
