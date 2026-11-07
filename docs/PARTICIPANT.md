# Your idea-to-print journey

Start with a new project folder and one sentence:

> I want to make a touch-first MP3 player using an ESP32 and a CYD 2.8 display.

Choose who it is for and where it is used. Everything else is a decision you will make. Use the agent as a collaborator: ask it to show alternatives, state assumptions, challenge a choice, implement a decision, and explain failures.

## 1. Imagine alternatives • 5:30–5:45

Spend the first three minutes on the user and use case. Then ask for three visibly different product concepts. Explore a calm minimal player, a rugged field device, a playful object, or your own directions. Compare at the same scale and viewing angle. Ask for both hand-held context and a front view.

Do not start by asking for CAD. Ask what each direction makes easier or harder: carrying, touch use, assembly, battery space, and printing. Generated pictures express intent; their dimensions and internal arrangements are not evidence.

**Your decision:** who is this for, and which directions deserve consideration?

**Save:** a one-sentence brief and three sketches/images with short descriptions. If image generation is slow, sketch three silhouettes and annotate them with the agent. Each participant still makes alternatives.

## 2. Choose and make the concept physically plausible • 5:45–6:00

Score the alternatives in `templates/DESIGN_RECORD.md`. Pick one and revise it around the real board. Identify the display opening, touch access, cable entry, microSD access, speaker/headphone choice, board supports, enclosure joint, fasteners, and assembly order.

Measure a board or use an organizer's verified measurement sheet. If neither is available, explicitly label the affected dimensions **provisional**. A published board outline is not a connector or mounting drawing.

Choose the power approach. USB power can simplify the first prototype. A battery-powered direction requires a selected battery and compatible charging/power arrangement, space for wires and connectors, and a retention approach. You can study an envelope during the session, but cannot claim a verified battery assembly from a generic box.

**Your decision:** selected concept, one revision for producibility, and a feasible first-prototype scope.

**Save:** selected visual, dimensions/keepouts, a preliminary BOM, and unresolved questions. Freeze the essential mechanical interfaces before coding.

## 3. Hand off to a coding agent and wire the tool • 6:00–6:25

Open your project folder in Codex or your chosen coding agent. Supply your brief, measured constraints, concept, BOM, `AGENTS.md`, and `docs/GENERATION_CONTRACT.md`. Ask the agent to propose the smallest implementation that preserves your decisions. Review that plan, then have it generate the scripts.

You own the design. A flat two-part enclosure may fit one concept; another may use a cradle or sandwich assembly. Avoid spending the session on cosmetic detail. Complete the pipeline with simple geometry first, then refine if time remains.

Try `python3 tools/demo.py` to see the parameter-to-tool-to-trace pattern. Inspect the script your agent produced before configuring it in `config/policy.json`. The tool schema accepts only declared numeric parameters; paths, executable selection, and script fingerprints are host-owned. Run one invalid parameter request and inspect the rejection trace.

**Your decision:** what the agent may vary, and which measured constraints stay fixed.

**Save:** generated source, reviewed tool configuration, a request JSON, and the first validation trace. Do not let tool setup consume the rest of your session: see the manual-run fallback in TOOLS.md.

## 4. Generate, inspect, and export your design • 6:25–6:55

Run the generated FreeCAD script. Inspect the first result in FreeCAD. Compare its dimensions to your record; check board clearance, touch opening, walls, supports, and accessible connectors.

Ask for one meaningful revision—such as changing wall thickness or increasing connector access—and regenerate. Confirm the intended change actually occurred without breaking interfaces.

Export a native `.FCStd` document, STEP solids, and **separate STL meshes for the printable components**. Keep electronics reference geometry separate and clearly labeled. Require the agent to check for valid non-empty solids and report export failures. Reopen the STEP and STL files; exporting without error is not enough.

**Your decision:** accept this version for assembly review, or fix the largest issue first.

**Save:** code, parameters, native model, exported parts, dimensions, and trace. A participant who hits a failure records the cause and correction rather than claiming an export was produced.

## 5. See how the product goes together • 6:55–7:10

Have the agent use Blender to produce an assembled view and an exploded view from the exported geometry. Ask it to label the major components and preserve millimeter-to-meter scale. The exploded view should reveal assembly order, not just scatter objects.

Review the design yourself: Can the board enter the case? Can screws be reached? Can a USB plug be inserted? Does a wire cross a screw boss? Can the battery be retained and serviced? Does the enclosure obstruct touch near the screen edges?

Rendered views help you notice problems; they do not prove fit. Use CAD section views and interference checks for dimensions and intersections. Simplified electronic envelopes cannot establish component-level clearance.

**Your decision:** one assembly issue to fix, or the evidence supporting this arrangement.

**Save:** assembled and exploded PNGs, a `.blend` scene, optionally GLB, and a short assembly sequence. If rendering fails, create an exploded arrangement in FreeCAD and capture it; still document the attempted Blender step.

## 6. Prepare for a printer, then show your evidence • 7:10–7:30

Use 7:10–7:22 for slicing. Import only your printable STLs into your chosen slicer. Select the **actual printer, nozzle, and material**. Verify units, overall size, orientation, bed contact, overhangs, supports, thin walls, and layer preview. Compare time/material estimates for two orientations and choose deliberately.

Save the slicer project (`.3mf` where supported) and fill in `templates/PRODUCTION.md`. Export machine-specific G-code only after the correct printer profile and model have been verified. Printing does not need to start tonight.

At 7:22, stop making improvements and assemble your handoff. Show your idea, rejected alternative, selected concept, BOM, code, assembly view, and slicer result. State one agent mistake you caught and one remaining unknown. Use the final eight minutes for brief shares or paired reviews; everyone completes their own handoff.

**Your decision:** ready for a fit-check print, or blocked pending a named measurement/test.

**Save:** slicer project, preview screenshot, estimated time/material, and a clear next step. “Ready for a fit-check print” is different from “ready to manufacture a finished electronic product.”
