# Participant project instructions

This project starts from an idea. Do not substitute a pre-existing enclosure for the participant's choices.

## How to work

1. Read the participant's brief, concepts, decisions, measurements, and BOM before designing. Ask about missing high-impact constraints one at a time. Label unknowns. Never invent measured values.
2. Propose a small implementation first, then generate participant-specific code under `generated/`. Keep earlier accepted versions using the participant's version control.
3. Use simple geometry to finish the whole workflow before any cosmetic refinement. Do not add a firmware build, a battery circuit, or a printing dependency to the session.
4. Avoid network calls, secrets, filesystem scanning, and deleting unrelated files. Show generated source to the participant before running it.
5. Report what actually ran: commands, failures, application versions, and paths. Never create placeholder STEP/STL/PNG files to make outputs look complete.
6. Do not publish, message anyone, upload the project, or send a print job without the participant's instruction.

## Source layout

- `generated/params.json`: a few named numeric design parameters (e.g. `wall_mm`) that the participant can change and rerun.
- `generated/measurements.json`: authoritative measured dimensions, with provisional values clearly marked. Keep these separate from tunable parameters.
- `generated/build_cad.py`: the FreeCAD model.
- `generated/render_scene.py`: the Blender visualization.
- `generated/out/`: all exports and renders.

Prefer self-contained scripts. Agree on output filenames with the participant.

## FreeCAD (`build_cad.py`)

- Run inside FreeCAD's Python (its command-line executable or Python console), not system Python.
- All CAD units are millimetres. Generate geometry deterministically from `measurements.json` and `params.json`.
- Keep printable parts, electronics reference envelopes, connector insertion space, and keepouts separate, and give them descriptive names.
- Export `assembly.FCStd`, `assembly.step`, and **one STL per printable part**. Keep electronics references out of the print STLs.
- Before export, check that each printable shape is valid, has nonzero volume, and has the expected solid count. Fail visibly if a check fails.
- Write `geometry-report.json` with the FreeCAD version, parameter values, part names, bounding dimensions, volumes, check results, and unresolved interfaces.
- Call this "parameter-driven regeneration," not a live feature tree. Changing `params.json` and rerunning must actually change the geometry.
- If print STLs are reoriented for the bed, also export assembly-position geometry for Blender.

## Blender (`render_scene.py`)

- Use the installed Blender's API. Recent versions use `bpy.ops.wm.stl_import`, and older ones use the legacy importer. Detect which one is available and fail clearly if neither is.
- Load only the specific exported files. Do not search for whichever STL is newest.
- Convert millimetres to metres exactly once. Check the resulting dimensions.
- Produce `assembled.png`, `exploded.png`, and `assembly.blend`. GLB is optional. Use CPU rendering with low samples and resolution.
- Label the major components. The exploded view should show the assembly order. Visually mark electronics envelopes as unverified references.
- A render is not proof of fit. Use CAD checks for clearances and interference.

## Slicing

The participant slices the parts themselves, for an explicitly chosen printer, nozzle, and material. Help them compare orientations and save the slicer project. Mark provisional fit as provisional.
