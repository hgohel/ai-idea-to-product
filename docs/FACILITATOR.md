# Facilitation: everyone experiences the complete workflow

## Learning objective

Participants learn how to move between creative intent, physical evidence, executable design, assembly review, and production preparation with an AI agent. The MP3 player is a common project brief. Success is an experienced and documented loop—not reproducing the facilitator's design.

## Before November 9

- Send INSTALL.md in advance. Ask each person to open all applications once and sign into their chosen agent before arriving.
- Bring one or more actual CYD 2.8 boards, a caliper, a ruler, and representative cables. Record exact board revision and measured connector/hole positions. If unavailable, tell participants they are doing a provisional design study.
- If exploring batteries, bring datasheets and measured envelopes for selected parts; do not present a generic battery block as a completed power system.
- Rehearse the workflow on the laptop/application versions you will use. Run the local verification checklist in VALIDATION.md. A successful test of this kit's Python wrapper does not establish FreeCAD or Blender compatibility.
- Have a familiar slicer with the real workshop printer profile installed. Participants without a printer may prepare for that agreed printer, explicitly recording it.
- Keep any facilitator example out of the opening materials. Start with the idea. If someone gets stuck, help them repair their own project; show a reference implementation only after they have attempted that stage.
- Avoid introducing a new firmware stack, soldering, or a complete audio electronics bring-up inside these two hours.

## Run of show

| Eastern time | Activity | Evidence from every participant |
|---|---|---|
| 5:30–5:45 | Idea, user, three visual alternatives | Brief + alternatives |
| 5:45–6:00 | Down-select, physical constraints, BOM | Choice + revised concept + constraint record |
| 6:00–6:25 | Coding-agent handoff and tool wiring | Source + bounded request + trace |
| 6:25–6:55 | FreeCAD build, one revision, exports | Native file + STEP/STL + checks |
| 6:55–7:10 | Assembled/exploded visualization | Views + assembly critique |
| 7:10–7:22 | Printer preparation | Slicer project + layer inspection |
| 7:22–7:30 | Handoff and reflection | Complete evidence folder + next action |

This retains the advertised 25-minute wiring and 30-minute generation blocks. It reallocates five minutes from the advertised final 40-minute block to ideation and selection: 30 minutes up front and 35 minutes at the end. The full session remains 120 minutes. The opening explanation is included in ideation.

## Keep the whole journey intact

Use visible timers. When a stage runs long, reduce detail rather than dropping later stages. One enclosure assembly, a few printable parts, one meaningful parameter revision, and two views are enough. No mandatory image count beyond three initial alternatives; no photorealism contest.

At each checkpoint ask: **What did you decide? What evidence supports it? What did the agent assume?** Let people help one another, but do not split the room into specialists who each experience only one stage.

## Recovery paths

| Problem | Keep the participant moving |
|---|---|
| Image tool unavailable/slow | Draw three rough silhouettes; have the agent critique them |
| No hardware measurement | Mark assumptions; model envelopes; keep production status blocked |
| CAD syntax/API problem | Give the agent the actual traceback and installed version; simplify one operation |
| Tool adapter consumes >10 minutes | Run the reviewed script manually; preserve parameters, command, output, and error in a run record |
| CAD application cannot run | Pair on a working laptop, running the participant's own design; record fallback |
| Blender slow | Low samples/resolution; inspect assembly in FreeCAD; retain Blender script and failure evidence |
| Slicer unavailable | Pair at a slicer workstation with that participant's files; do not call a written plan a sliced job |

Do not fabricate successful artifacts to make every handoff look complete. A well-diagnosed blockage is a legitimate learning outcome, but distinguish it from a completed run.

## Closing discussion

1. Which design decision remained yours?
2. What did the agent invent or misunderstand?
3. Which check changed your design?
4. Could somebody else reproduce the latest model from your project?
5. What must happen before your first fit-check print or electronics assembly?

Each participant may share their project repository or gist after removing credentials, local machine paths, private prompts, and irrelevant traces. A gist suits small code samples; a repository or ZIP is better for the complete project. No automatic publishing is part of this kit.
