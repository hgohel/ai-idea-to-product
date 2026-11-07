# Agent prompts: use one stage at a time

Replace bracketed fields with your own decisions. Treat an agent's plausible claim as a hypothesis until supported by a measurement, datasheet, or executed check.

## 1 — Begin with the idea

- [1a: Develop the idea](1a_develop_idea.md) — Propose three product directions for the player.
- [1b: Visualize concepts](1b_visualize_concepts.md) — Generate comparable concept images, if image generation is available.

## 2 — Down-select and revise for reality

- [2a: Score and revise](2a_score_and_revise.md) — Score the concepts, then revise the chosen one around the real hardware.
- [2b: Commit to a direction](2b_commit_direction.md) — Record the choice and the measurements that matter most.

## 3 — BOM and implementation brief

- [3a: Populate the BOM](3a_populate_bom.md) — Write the BOM, marking unverified parts as TBD.
- [3b: Coding-agent brief](3b_coding_agent_brief.md) — Turn the decisions into a brief for the coding agent.

## 4 — Generate the CAD project

- [4a: Generate CAD](4a_generate_cad.md) — Generate the FreeCAD model and Blender visualization scripts.
- [4b: Expose parameters](4b_expose_parameters.md) — Move a few numeric parameters into a file you can change and rerun.

## 5 — Run, inspect, change one thing

- [5a: Run and verify](5a_run_and_verify.md) — Run the reviewed build and verify the exported files.
- [5b: Change one parameter](5b_change_one_parameter.md) — Change one parameter and compare the outputs.

## 6 — Understand assembly

- [6a: Assembly views](6a_assembly_views.md) — Create assembled and exploded views from the CAD exports.
- [6b: Critique the assembly](6b_critique_assembly.md) — Check the assembly and suggest the smallest fix for the top issue.

## 7 — Prepare for production

- [7a: Prepare the print](7a_prepare_print.md) — Prepare a fit-check print and slicer project for a specific machine.
- [7b: Package the project](7b_package_project.md) — Package the project so another participant can reproduce it.
