# Install before the workshop

**AI Tinkerers Manchester • November 9, 2026 • 5:30–7:30 p.m. Eastern**

Please finish this before you arrive. The two hours are for the workflow, not for downloading apps. You need a laptop and access to a coding agent. You don't need a 3D printer.

## 1. Get this project

```bash
git clone https://github.com/shyamyadati/ai-idea-to-product.git
cd ai-idea-to-product
```

Or download the ZIP from GitHub and unzip it into a short, writable folder (on Windows, something like `C:\work\ai-idea-to-product`).

## 2. Install the tools

You need **Python 3.10+**, **FreeCAD**, **Blender**, a **slicer**, and a **coding agent**.

### Ubuntu 24.04

```bash
sudo apt update
sudo apt install python3 freecad blender
```

FreeCAD is in the Universe repository. If `apt` can't find it, enable Universe in Software & Updates and try again. Distribution packages can lag behind upstream. The official [FreeCAD](https://www.freecad.org/downloads.php) and [Blender](https://www.blender.org/download/) releases also work. Avoid unmaintained PPAs.

### macOS

Install the Apple Silicon or Intel builds of [FreeCAD](https://www.freecad.org/downloads.php) and [Blender](https://www.blender.org/download/), plus Python 3.10+ (e.g. from [python.org](https://www.python.org/downloads/) or Homebrew). Open each app once so macOS approves it. The command-line executables are inside the app bundles. For Blender, this is usually `/Applications/Blender.app/Contents/MacOS/Blender`. Check your own FreeCAD bundle rather than assuming a path.

### Windows

Install [FreeCAD](https://www.freecad.org/downloads.php), [Blender](https://www.blender.org/download/), and [Python 3.10+](https://www.python.org/downloads/) from their official sites or use the [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/) command below. Use `py -3` wherever this kit says `python3`. Note where `FreeCADCmd.exe` and `blender.exe` were installed.

```powershell
winget install Python.Python.3.14 FreeCAD.FreeCAD BlenderFoundation.Blender
```

### Slicer (all platforms)

Install a slicer you already know: PrusaSlicer, OrcaSlicer, Bambu Studio, Cura, or your printer vendor's slicer. Set up a real printer profile (printer, nozzle, material), even if you're not printing tonight.

### Coding agent

Use Claude Code, Codex, Cursor, or another agent that can read and write files and run commands in a local folder. Sign in before you arrive. An agent that can generate images helps with the first stage, but it isn't required. Sketching works too.

## 3. Pre-flight check

Do this at least a day before the workshop:

- [ ] FreeCAD, Blender, and your slicer each open. Note their versions from the About dialog.
- [ ] `python3 --version` reports 3.10 or later.
- [ ] You can find FreeCAD's **command-line** executable. One of these should work: `command -v freecadcmd` or `command -v FreeCADCmd`. On macOS/Windows, find it inside the install folder. The GUI executable is a different thing.
- [ ] You can find Blender's executable: `command -v blender`, or the macOS/Windows path above.
- [ ] Your coding agent opens this folder and can read `AGENTS.md`.

Write the versions and executable paths down. Your agent will ask for them.

**Optional but very useful:** bring a CYD 2.8 board (ESP32-2432S028R or similar) and calipers. Real measurements make the mechanical design much better. Without a board, your design is a provisional study, and that's fine.

## Common fixes

| Symptom | Check |
|---|---|
| `ModuleNotFoundError: FreeCAD` | The script must run inside FreeCAD's Python, not system Python. Don't `pip install FreeCAD`. |
| `ModuleNotFoundError: bpy` | The script must run inside Blender (`blender --background --python script.py`) |
| FreeCAD command not found | Locate the command-line executable in your install and give the agent its full path |
| FreeCAD CLI hangs or ignores the `.py` | Run the script from FreeCAD's Python console instead |
| Blender STL import operator missing | Tell the agent your exact Blender version and paste the traceback |
| Wrong size in Blender or the slicer | Check millimetres vs metres and import scaling |

## Useful references

- [CYD community repository](https://github.com/witnessmenow/ESP32-Cheap-Yellow-Display): board variants and resources
- [FreeCAD on Linux](https://github.com/FreeCAD/FreeCAD-documentation/blob/main/wiki/Installing_on_Linux.md)
- [Blender command-line arguments](https://docs.blender.org/manual/en/latest/advanced/command_line/arguments.html)
