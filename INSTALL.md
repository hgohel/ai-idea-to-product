# Install before the workshop

Allow setup time before November 9. The live session is for the workflow, not downloading applications. A laptop and coding-agent access are sufficient to participate; a physical printer is not required. A real CYD board or verified measurement sheet greatly improves the mechanical exercise.

## Ubuntu 24.04

1. Extract the ZIP into a writable local folder. Open a terminal in `cyd-idea-to-print`.
2. Install Python and FreeCAD from Ubuntu's repositories:

   ```bash
   sudo apt update
   sudo apt install python3 freecad
   ```

   Ubuntu's FreeCAD package is in Universe. If unavailable, enable the Universe repository through Software & Updates, refresh package metadata, and retry. The distro version can lag upstream. An official stable FreeCAD distribution is another option; verify its command-line executable before configuring the wrapper. Do not use an unmaintained PPA simply to follow an old tutorial.

3. Install Blender. A distribution package is a convenient starting point:

   ```bash
   sudo apt install blender
   ```

   Or install a stable release from [Blender](https://www.blender.org/download/). Have the coding agent target your installed version; do not assume an online example uses the same STL importer API.

4. Install a slicer you already know, such as PrusaSlicer, OrcaSlicer, or your printer vendor's slicer. Use the official project/vendor distribution and configure the actual target printer/nozzle/material. There is no required slicer plugin in this kit.
5. Open FreeCAD, Blender and the slicer once. Record the versions from their About dialogs. Launch your coding agent and confirm it can work in this local project.
6. Check the supporting tools:

   ```bash
   python3 --version
   command -v freecadcmd
   command -v FreeCADCmd
   command -v blender
   python3 -m unittest discover -s tests -v
   python3 tools/demo.py
   ```

   Only one FreeCAD command name needs to exist. A GUI executable and a command executable are different. Use the actual command executable's path in the policy after generating your scripts. If your distribution exposes only a GUI workflow, use the reviewed console fallback in TOOLS.md; test it before the event.

Python 3.10+ is needed for the wrapper. It was tested with Python 3.12.14 on Ubuntu 24.04.3. There are no pip dependencies. FreeCAD uses its own Python environment; installing a package named `FreeCAD` with pip is not the setup route here.

## Windows

Install stable FreeCAD and Blender from their official distributions, Python 3.10+ from Python's official distribution, and your chosen slicer. Extract the project to a short writable path such as `C:\work\cyd-idea-to-print`.

Use `py -3` in place of `python3`. To copy the policy in PowerShell:

```powershell
Copy-Item config/policy.template.json config/policy.json
py -3 -m unittest discover -s tests -v
py -3 tools/demo.py
```

In `policy.json`, set the actual executable paths from your installation; for example, locate `FreeCADCmd.exe` in the FreeCAD installation and `blender.exe` in the Blender installation. Use forward slashes in JSON paths or escape backslashes. Do not copy a versioned path from somebody else's machine without checking it.

The wrapper's Windows subprocess path and the generated CAD/render scripts require local verification. On timeout it kills the immediate process, not a Windows process tree.

## macOS

Install the appropriate Intel or Apple Silicon versions of FreeCAD and Blender, Python 3.10+, and your slicer. Open each application normally once. Locate its bundled command executable and put its full path into the policy. Blender commonly exposes `/Applications/Blender.app/Contents/MacOS/Blender`; inspect your installation rather than assuming the FreeCAD bundle layout.

Use `python3` for the wrapper. If a bundled FreeCAD command executable is unavailable, use the FreeCAD Python-console fallback. macOS application execution and permissions require local verification; this kit was not tested on macOS.

## At the workshop

Begin with README.md and the participant journey—not with application setup or a ready-made CAD file. You configure `policy.json` only after your agent creates source for your chosen design.

## Common fixes

| Symptom | Check |
|---|---|
| `ModuleNotFoundError: FreeCAD` | Run the model in FreeCAD's Python environment |
| `ModuleNotFoundError: bpy` | Run rendering through Blender's Python environment |
| Command not found | Locate installed executable; update the human-owned policy |
| FreeCAD command hangs / does not execute `.py` as expected | Verify the distribution's CLI behavior; use the reviewed console fallback and record it |
| Script hash changed | Inspect the change, then fingerprint the accepted version |
| Missing STEP/STL after exit code 0 | Check actual script error/output; output existence checks deliberately fail |
| Blender import operator missing | Give the agent the installed Blender version and traceback |
| Wrong size in Blender or slicer | Verify millimeters, import scaling, and assembly transforms |
| Model looks correct but cannot assemble | Revisit measurements, insertion paths, fasteners and keepouts |

Official references are linked in docs/SOURCES.md. No FreeCAD, Blender, slicer, or model provider is bundled with this package.
