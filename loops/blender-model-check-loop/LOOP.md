---
name: blender-modeling
title: Blender Modeling skill
repo: roble3/cc-blender-skill
license: MIT
url: https://gethabit.dev/skills/roble3/blender-modeling
---

# Blender Modeling skill

The blender modeling skill helps 3D artists and developers create meshes in Blender through MCP: primitives, hard-surface stacks, booleans, mirror and array modifiers, and clean topology.

- Install the skill: `npx skills add roble3/cc-blender-skill --skill blender-modeling`
- Source: https://github.com/roble3/cc-blender-skill/tree/HEAD/plugin/skills/blender-modeling
- Licence: MIT (Habit links to this skill and does not host or change it)

Use it when: You ask an agent to model a prop; You add bevel or boolean modifiers; You block out a scene from primitives.
Skip it when: You need sculpting strokes; You convert a wireframe drawing to 3D.

# Make it a habit: Clean meshes built step by step.

For each modeling request your agent reads the MCP backend guide, picks a recipe from the decision tree, builds geometry in small code calls with GEO- names, keeps the modifier stack order, cleans up the mesh and renders a viewport check.

Install the skill first (command above), then the habit:

## The three decisions

- **Trigger:** new object to model (manual; Claude Code routine with Blender MCP; `run when you ask for a new 3D object or mesh edit`)
- **Verification:** names, stack order, render. Hard checks: every new object name starts with GEO-; modifier order follows Mirror, Array, Solidify, Bevel, Subdivision Surface; render_viewport_to_path writes a viewport image; each code call prints its structured result. On fail: retry, max 2 retries.
- **Memory:** modeling steps log at `loops/blender-model-check-loop/run-log.md`. Read first: objects built and the backend in use.

## Steps

1. **Pick the backend.** Read ../text-to-blender/references/mcp-backends.md and keep one backend for the task.
2. **Choose a recipe.** Use the decision tree for hard-surface, organic, repeating, cylindrical or boolean work.
3. **Build in chunks.** Run short execute_blender_code calls, naming every object with GEO-.
4. **Stack modifiers.** Add Bevel before SubSurf and Mirror first, per the stack order.
5. **Clean up.** Remove doubles, fix normals and smooth rounded parts.
6. **Check visually.** Render the viewport with render_viewport_to_path and inspect it.

Stop rule: Stops after one object, with at most 2 fix rounds.

## Permissions

- Writes: loops/blender-model-check-loop/**
- Network: none
- Sends: nothing
- Human approval before anything ships: no

## Install the habit

1. Show the user the files you will create and the schedule you will set. Ask once.
2. Create the memory file first (`loops/blender-model-check-loop/run-log.md`), then the trigger.
3. Run the hard checks once by hand so the user sees them pass.
4. End with: `↻ Habit installed. Trigger: new object to model. Verification: names, stack order, render. Memory: loops/blender-model-check-loop/run-log.md. Test it: run it once by hand. Undo: delete the files you created and the trigger.`
