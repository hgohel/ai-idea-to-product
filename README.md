# From idea to a physical product—with an AI agent

**AI Tinkerers Manchester • November 9, 2026 • 5:30–7:30 p.m. Eastern**

The shared idea: **a touch-first MP3 player built around an ESP32 and a CYD 2.8 display.**

Everyone starts from that one sentence. Over two hours, you work with an AI agent to explore alternatives, choose a direction, deal with real constraints, write a BOM, generate CAD and renders, review the assembly, and prepare a print job. There's no supplied enclosure, finished CAD model, or prescribed style. The design is yours.

## Before you arrive

Follow **[INSTALL.md](INSTALL.md)**. Install and open FreeCAD, Blender, a slicer, and your coding agent, then run the pre-flight check.

## At the workshop

Open this folder in your coding agent. We'll walk through **[the stage prompts](prompts/WORKFLOW.md)** together, one at a time. Fill in the bracketed parts with your own decisions. Don't let the agent quietly invent measurements.

[AGENTS.md](AGENTS.md) tells your coding agent how to behave in this project. Your generated scripts and outputs go in `generated/`.

## Finish line

By 7:30 you should have:

- a design direction you chose, with a rejected alternative
- an honest BOM, with unknowns marked TBD
- CAD code you can rerun, with STEP/STL exports
- assembled and exploded views
- a saved slicer project, or a clearly documented blocker

Printing, wiring the circuit, and audio firmware are follow-on work. The MP3 player is the vehicle for learning the workflow.

## License

[MIT](LICENSE)
