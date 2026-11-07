# Connect your generated scripts to an agent

This is an example Python tool interface, not an MCP server or a preconfigured connection to a particular model provider. A host can register the function schemas and route model tool calls to `invoke`. A coding agent with a terminal can also use the CLI.

## 1. Understand the interface first

```bash
python3 tools/demo.py
```

This uses the real wrapper with a tiny metadata worker in a new demo folder. Inspect `trace.jsonl`, `parameters.json`, `receipt.json`, and `manifest.json` in the printed run directory. The `build_cad` tool name in this isolated demo exercises routing only; the worker explicitly reports metadata-only output.

## 2. Configure your own reviewed source

After generating and inspecting your design scripts:

```bash
cp config/policy.template.json config/policy.json
python3 tools/agent_tool.py fingerprint generated/build_cad.py
python3 tools/agent_tool.py fingerprint generated/render_scene.py
```

Edit the **human-owned** `config/policy.json`:

- Set each tool's `script` to its project-relative source path and `sha256` to the printed fingerprint.
- Set `executable` to the installed FreeCAD command executable or Blender executable. Do not put flags into this field.
- Declare the numeric parameters your design actually supports. Example only: `"parameter_limits": {"wall_mm": [1.6, 3.2]}`. Limits must reflect your design and manufacturing approach; this is not a universal wall-thickness recommendation.
- Add every expected printable STL and report to `required_outputs`. These must be plain filenames.
- Declare measured constraints and render inputs as project-relative file paths in `inputs`. Example: `"inputs": {"constraints": "notes/measured.json"}` for CAD, or `"inputs": {"case_mesh": "outputs/EXACT_RUN_ID/case.stl"}` for rendering. Use the actual run ID and filenames.
- Review changed source and update its fingerprint before rerunning. Do not let an agent treat the hash update as a substitute for review.

Generate `notes/measured.json` and the scripts from your own decisions; no measured product data is supplied by this template.

## 3. Submit one bounded request

For the example `wall_mm` parameter, save this as `examples/my-build.json`:

```json
{"name":"build_cad","arguments":{"wall_mm":2.0}}
```

Then:

```bash
python3 tools/agent_tool.py schema
python3 tools/agent_tool.py run --request examples/my-build.json --dry-run
python3 tools/agent_tool.py run --request examples/my-build.json
```

Use the parameter names and values your own script defines. An empty parameter map is valid if the first build uses only a fixed measured input file. After CAD succeeds, update the host-owned render inputs to the precise artifacts, and submit `{"name":"render","arguments":{}}` if your renderer has no exposed numeric parameters.

Python host integration:

```python
from tools.agent_tool import invoke, schema, load_json
from pathlib import Path
project = Path('/absolute/path/to/my-project')  # host controlled
definitions = schema(load_json(project / 'config/policy.json'))
# Register definitions using your model provider's tool-registration format.
# Route a returned name + parsed arguments; never exec the model response:
result = invoke(project, {"name": "build_cad", "arguments": {"wall_mm": 2.0}})
# Return result (or the caught error) to the agent for its next turn.
```

The host snippet is provider-neutral integration guidance. The kit does not call an LLM or claim that a live provider connection was tested.

## Boundaries and logging

The wrapper accepts only the two declared tool names and the numeric arguments configured for that tool. It rejects unknown arguments, non-finite values, booleans used as numbers, path escapes and symlinks. It uses an argument list with no shell, a reviewed entrypoint fingerprint, unique run directories, a deadline, and a process-log size check. It verifies required outputs exist and are nonempty and hashes them. It records requests, input hashes, script hash, timestamps, command, failure/success, and duration.

Malformed JSON rejected before dispatch produces a CLI error rather than a run trace. Invalid calls reaching `invoke` get a failure trace if the output directory can be safely created. Dry-run success means numeric request validation only; it does not validate CAD geometry, installed tools, or whether scripts exist.

**These are basic application boundaries, not an OS sandbox.** Reviewed scripts and their imported modules execute with your user's permissions and can read/write elsewhere or access the network. A fingerprint does not restrict their behavior. Do not run untrusted generated code merely because it is in this project. Do not grant an agent unrestricted shell access and assume this wrapper confines that separate access. For stronger isolation use a dedicated OS account, container/VM, or your agent host's execution controls.

The wrapper omits most ambient environment variables, but this is not secret isolation. Output-size monitoring is polled, so a process can briefly exceed the limit. It kills a process group on POSIX; Windows timeout handling terminates only the immediate process. Multi-file imports, child-process escape, concurrent filesystem mutation, network denial, disk quotas and OS-level permission containment are outside this example's guarantees.

## Manual-run fallback

If wrapper integration stalls, preserve the workflow by executing your reviewed script directly in the intended application's Python console. First run a dry-run request to get a directory with validated `parameters.json`. Create `inputs.json` there with the exact input mapping. Then set the four `WORKSHOP_*` environment variables in that console and execute the reviewed entrypoint with:

```python
import os
from pathlib import Path
root = Path('/absolute/path/to/your/project')
run = root / 'outputs' / 'YOUR_DRY_RUN_ID'
os.environ['WORKSHOP_PROJECT'] = str(root)
os.environ['WORKSHOP_RUN'] = str(run)
os.environ['WORKSHOP_PARAMETERS'] = str(run / 'parameters.json')
os.environ['WORKSHOP_INPUTS'] = str(run / 'inputs.json')
script = root / 'generated' / 'build_cad.py'  # render_scene.py in Blender
exec(compile(script.read_text(), str(script), 'exec'))
```

This executes a **reviewed local file**, not model-supplied code strings. Record the manual command, version, outputs and errors in a run note. The wrapper's dry-run trace remains a dry-run trace; do not relabel it as a successfully supervised process. These GUI fallbacks require local verification with your generated scripts.
