# Sources and provenance

Checked November 7, 2026. These references support the workflow and optional follow-on research. They are not a substitute for measurements of the participant's own hardware.

## Event context

- [Published event](https://manchester-nh.aitinkerers.org/p/ai-tinkerers-november-build-night-building-physical-products-with-ai-manchester-nh): shared project context supplied by the organizer.
- The organizer discussion was reviewed to confirm the emphasis on getting participants running and keeping printing optional. No reusable code was present in the reviewed thread. A search of accessible Drive materials for FreeCAD returned no files. This does not establish that organizers have no code elsewhere.
- This kit contains newly authored workflow materials and supporting Python code. It does not include a pre-existing product design, earlier concept art, private correspondence, or third-party firmware.

## CAD and automation

- [FreeCAD Linux installation](https://github.com/FreeCAD/FreeCAD-documentation/blob/main/wiki/Installing_on_Linux.md): Ubuntu repository installation and packaging caveats.
- [FreeCAD macros](https://github.com/FreeCAD/FreeCAD-documentation/blob/main/wiki/How_to_install_macros.md): Python macro workflow.
- [FreeCAD command-line manual](https://manpages.ubuntu.com/manpages/jammy/man1/freecad.1.html): distinction between GUI and command-line interpreter. Package-specific behavior must be verified locally; this reference is not a test of Ubuntu 24.04's installed binary.
- [Blender command-line arguments, 4.2](https://docs.blender.org/manual/en/4.2/advanced/command_line/arguments.html): background Python execution and Python exception exit behavior.
- [Blender 4.2 API index](https://docs.blender.org/api/4.2/genindex-S.html): STL import operator reference.
- [Python subprocess documentation](https://docs.python.org/3/library/subprocess.html): argument-list execution, environment and process handling. Application boundaries in this kit are not a security sandbox.

## Electronics and optional firmware inspiration

- [CYD community repository](https://github.com/witnessmenow/ESP32-Cheap-Yellow-Display): board resources and starting point for verifying variants.
- [ESP32-2432S028R manufacturer specification](https://www.guition.com/icms/upload/fb081940d6fc11f09850077a33e1404f/FTPData/UEditor/file/2026121/1768961091633/ESP32-2432S028%20Specifications-EN.pdf): one common resistive-touch variant lists a 50 × 86 mm module, 43.2 × 57.6 mm active display area, and 320 × 240 pixels. These headline values are not a mechanical drawing for every CYD 2.8 variant and are deliberately not inserted into a predesigned enclosure.
- [Cheap Yellow MP3 Player project](https://github.com/Sparkadium/Cheap-Yellow-MP3-Player/): possible follow-on firmware inspiration. Discovered during research; not cloned, copied, compiled, or tested for this workshop. Verify its license, exact hardware, dependencies, and audio assumptions before adopting it. Keep it out of the opening ideation stage if it would anchor participants to somebody else's design.
- [Adafruit lithium battery guidance](https://learn.adafruit.com/li-ion-and-lipoly-batteries/conclusion) and [protection circuitry](https://learn.adafruit.com/li-ion-and-lipoly-batteries/protection-circuitry): use appropriate protection, compatible charging and component-specific limits. No wiring design is provided by this kit.

## Production preparation

- [PrusaSlicer first-print workflow](https://help.prusa3d.com/article/first-print-with-prusaslicer-2-9_1753): orientation, support needs, printer and material selection. Apply the same questions in the participant's chosen slicer using its actual printer profile.

URLs are references, not bundled dependencies. External software retains its own licensing and behavior.
