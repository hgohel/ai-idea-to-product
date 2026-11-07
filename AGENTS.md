# Participant project instructions

This project starts from an idea. Do not substitute a pre-existing enclosure for the participant's choices.

1. Read the participant's brief, concepts, decisions, measurements and BOM before designing. Ask for missing high-impact constraints one at a time. Label unknowns; never invent measured values.
2. Follow `docs/GENERATION_CONTRACT.md`. Propose a small implementation, then generate participant-specific code under `generated/`. Preserve earlier accepted versions through the participant's chosen version control.
3. Keep CAD units explicit in millimeters. Distinguish physical parts, electronics envelopes, connector insertion space, and keepouts. Parameter-driven regeneration is acceptable; do not claim a live editable feature tree unless implemented.
4. Use simple geometry to complete the workflow before cosmetic refinement. Do not add a firmware build, battery circuit, or printing dependency to the core session.
5. Expose only declared bounded numeric parameters through `tools/agent_tool.py`. Do not accept arbitrary Python, shell commands, or paths as tool arguments. Do not edit the wrapper to bypass validation.
6. Human-owned `config/policy.json` selects scripts/executables and records reviewed script hashes. Present generated source for inspection before the participant enables execution. Imported modules and the whole project remain trusted code; hashing the entrypoint is not a sandbox.
7. Write generated artifacts only into the run directory supplied by the host. Use fixed filenames agreed with the participant. Avoid network calls, secrets, filesystem scanning, and deleting unrelated files.
8. Report real executions, failures, application versions and paths. Never create placeholder files with STEP/STL/PNG extensions to satisfy output checks. Add geometric verification inside the generated CAD script.
9. Produce assembled and exploded views from the actual CAD exports. Name major components and explain assembly order. Keep electronics reference models out of print exports.
10. Help prepare a slicer project for an explicitly selected machine, nozzle and material. Never send a print job automatically. Mark provisional fit as provisional.
11. Do not publish, message organizers, or upload the participant's project without their instruction.
