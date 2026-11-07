# From idea to a physical product—with an AI agent

**AI Tinkerers Manchester • November 9, 2026 • 5:30–7:30 p.m. Eastern**

The shared idea: **a touch-first MP3 player built around an ESP32 and a CYD 2.8 display.**

Everyone starts with that idea, explores alternatives, makes a choice, works through real constraints, builds a BOM, asks a coding agent to create their own CAD/render project, inspects an assembly, and prepares a print job. Each person experiences the whole process. There is no supplied enclosure, finished CAD model, prescribed visual style, or firmware implementation.

## Start here

1. Before arriving, follow [INSTALL.md](INSTALL.md). Install and open FreeCAD, Blender, a slicer, and your preferred coding agent. Tool installation is prework.
2. At the workshop, follow [the participant journey](docs/PARTICIPANT.md).
3. Copy the blank [project brief](templates/BRIEF.md), [design record](templates/DESIGN_RECORD.md), [BOM](templates/BOM.md), and [production checklist](templates/PRODUCTION.md) into your own project notes.
4. Use the [stage-by-stage prompts](prompts/WORKFLOW.md). Make your own decisions; do not let the agent silently invent measurements.
5. At the coding stage, open this folder in Codex or another coding agent. Give it [the generation contract](docs/GENERATION_CONTRACT.md) and your decisions. Your generated source belongs in `generated/`.

**Workshop finish line:** a documented design direction, honest BOM, reproducible code, CAD exports, an assembly inspection, and a saved slicer project or a documented blocker at that step. Printing, a completed circuit, and working embedded audio firmware are follow-on work. The product idea is the vehicle for learning the workflow.

## What is provided

| Material | Purpose |
|---|---|
| `docs/PARTICIPANT.md` | Two-hour journey with a decision and evidence at every stage |
| `docs/FACILITATOR.md` | Run of show, timeboxes, checkpoints, fallback paths |
| `prompts/WORKFLOW.md` | Ideation, critique, down-selection, BOM, coding, assembly, production prompts |
| `templates/` | Blank brief, dimensions, BOM, decisions, production handoff |
| `AGENTS.md` | Instructions for the coding agent inside this project |
| `docs/GENERATION_CONTRACT.md` | Expected FreeCAD/Blender script inputs, outputs and checks |
| `tools/agent_tool.py` | Provider-neutral Python tool interface with bounded numeric arguments and execution traces |
| `config/policy.template.json` | Human-owned executable/script configuration, initially disabled |
| `examples/` | A metadata-only demonstration of the tool interface—no product design |
| `tests/` | Tests for the wrapper's actual behavior and boundaries |
| `VALIDATION.md` | What was tested here, and what still needs a real workstation |

The wrapper uses Python's standard library. No API key, paid model, MCP server, or firmware toolchain is required to test it. A coding agent is needed for the live experience of developing each participant's design. An image-capable agent is useful during ideation; sketching alternatives is a workable fallback.

## Try the tool interface without CAD software

From this folder:

```bash
python3 -m unittest discover -s tests -v
python3 tools/demo.py
```

The demo creates a disposable local project under `outputs/`, runs a reviewed metadata writer, and produces a trace plus a JSON receipt. It does **not** generate CAD, render an image, or simulate a successful CAD run. Read [TOOLS.md](docs/TOOLS.md) before connecting your generated scripts.

## Scope and status

This is a **workflow kit with tested supporting Python tools**, not a completed MP3 player or a verified manufacturing design. The participant's actual design and generated FreeCAD/Blender scripts do not exist at the start. Exact board revision, connectors, mounting locations, battery system, audio output, assembly tolerances, and printer settings must be resolved or marked provisional in that participant's record.

Research and optional external inspiration are listed in [SOURCES.md](docs/SOURCES.md). No organizer code or third-party firmware is bundled. No private organizer email content is included.
