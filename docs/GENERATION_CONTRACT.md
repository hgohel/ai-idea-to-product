# Contract for the participant-generated CAD and Blender code

The participant's brief and measured constraints define the product. This document specifies execution and evidence; it does not prescribe the enclosure geometry.

## Source structure

Create `generated/build_cad.py` and `generated/render_scene.py`. Prefer self-contained entrypoints for this short workshop. If you split modules, record and review all dependencies; the wrapper fingerprints only the entrypoint. Do not modify the supporting tool to bypass a failed check.

## Inputs

The wrapper supplies these environment variables to each reviewed script:

| Variable | Contents |
|---|---|
| `WORKSHOP_PROJECT` | Absolute project root |
| `WORKSHOP_RUN` | New output directory allocated by the host |
| `WORKSHOP_PARAMETERS` | JSON file containing the validated numeric arguments |
| `WORKSHOP_INPUTS` | JSON mapping of logical input names to host-configured paths |

Read them with `os.environ` and `pathlib.Path`. Never take output paths, code strings, shell commands, or executable names from model arguments. Use a measured constraints file in the project for fixed interfaces; if it is an input, declare it in `policy.json` so its hash is recorded. Do not mix user-tunable dimensions and authoritative measurements without explanation.

Minimal input pattern for the agent to use:

```python
import json, os
from pathlib import Path
run_dir = Path(os.environ['WORKSHOP_RUN'])
params = json.loads(Path(os.environ['WORKSHOP_PARAMETERS']).read_text())
inputs = json.loads(Path(os.environ['WORKSHOP_INPUTS']).read_text())
```

## FreeCAD deliverables

- Run inside FreeCAD's Python environment, not ordinary system Python. Import `FreeCAD`, `Part`, and the needed mesh/export modules there.
- Generate the participant's design deterministically from measured constraints and named parameters. All CAD coordinates are millimeters.
- Separate printable components, electronics references and keepouts. Mark references with descriptive names.
- Export `assembly.FCStd`, `assembly.step`, and one STL per printable component; agree the filenames with the participant and add them to `required_outputs`.
- Include a small `geometry-report.json`: FreeCAD version, parameter values, part names, dimensions, volume, solid count, validity checks, and any unresolved interfaces.
- Check each printable shape for nonzero volume, expected solid count, and validity before export. Fail visibly if checks fail. Reopen STEP and STL and compare expected dimensions; validate mesh closure where the installed API supports it. Report the checks actually implemented.
- If the model uses a generated CSG shape rather than editable parametric features, describe it as parameter-driven regeneration. Changing the JSON and rerunning must actually change the intended geometry.
- Supply assembly-position meshes or transforms for visualization. If print STLs are reoriented for the bed, do not import them into Blender as though they retained assembly coordinates.
- Catch errors only to record them; do not convert failures into a success report.

## Blender deliverables

- Use the installed Blender API. On recent versions the STL import operator is `bpy.ops.wm.stl_import`; older installations may require the legacy importer. Detect the version/capability and fail clearly if unsupported.
- Load only the CAD artifacts declared in `WORKSHOP_INPUTS`. Do not scan the filesystem for whichever STL happens to be newest.
- Convert CAD millimeters to meters exactly once for Blender/GLB. Check the resulting bounding dimensions. Preserve object names and assembly transforms.
- Produce `assembled.png`, `exploded.png`, and `assembly.blend`. GLB is an optional additional output.
- Create a simple camera, lights, materials, and readable labels. Use CPU rendering with modest samples/resolution as a portable first attempt; optimize for the participant's laptop after it works.
- Keep assembled and exploded states distinct in the saved scene. The exploded offsets communicate a plausible assembly order and must not overwrite the underlying geometry.
- Identify electronic references and unverified envelopes visually. A pretty render is not evidence of manufacturability.

## Production handoff

The slicer is a separate human-reviewed stage. Use the actual printer/nozzle/material profile. Save its project and estimates. Do not make a generic STL export stand in for slicing, or label a generated G-code file machine-compatible without checking its target.

## Completion evidence

Provide exact commands, installed versions, output paths and the real trace. Explain any manually executed fallback. Separate successful checks, failures, untested steps and provisional physical assumptions.
