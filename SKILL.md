---
name: inverse-video-prompt
description: "Reverse-engineer reference videos, clips, or timestamped frame sequences into faithful, generation-ready AI video prompts. Use when the user asks to 反推视频提示词, 逆向视频 Prompt, 分析参考视频, 复刻视频的镜头/动作/运镜/光影/风格/节奏, extract a prompt from a video, or turn a reference clip into prompts for Seedance, MiniMax/Hailuo, Kling, Veo, Wan, or a generic video model."
metadata:
  short-description: "Reverse-engineer videos into generation prompts"
---

# Inverse Video Prompt

> **ROLE:** Reconstruct the likely generative intent of a reference video from temporal visual evidence. Do not merely summarize what appears on screen.

## Core Principles

1. **Analyze shots before prompts.** Segment the clip into shots or coherent visual events before writing the final prompt.
2. **Prefer temporal evidence over isolated frames.** Describe what changes from start to middle to end, not only what individual frames contain.
3. **Separate observation from inference.** State uncertain camera motion, hidden actions, lens choices, or transitions conservatively instead of inventing precision.
4. **Separate subject motion from camera motion.** A subject growing larger may be subject approach, camera push-in, zoom, or a combination; infer from background parallax and framing changes.
5. **Preserve stable continuity separately from changing action.** Identity, wardrobe, environment, art direction, color palette, and lighting continuity should not be repeatedly rediscovered per shot.
6. **Compile for generation.** The final result should tell a video model what to generate over time, not read like a film-review paragraph.
7. **Match the requested fidelity.** Reconstruct the reference faithfully by default. Adapt or redesign only when the user explicitly asks for variation.

## Workflow

### 1. Establish the Evidence

Determine what evidence is actually available:

- Full video with direct visual inspection
- Video file that can be sampled or decoded with tools
- Timestamped screenshots or extracted frames
- Untimestamped frame sequence
- Storyboard or contact sheet only

If the full video is available, scan the complete clip before detailed analysis. Record duration, aspect ratio, obvious cuts, scene changes, speed changes, and major action beats.

If frames must be extracted, do **not** use uniform sampling as the only evidence when the clip may contain cuts or fast actions. Use shot-aware and event-aware sampling. Read [references/shot-analysis-and-sampling.md](references/shot-analysis-and-sampling.md).

If only sparse screenshots are available, infer temporal behavior conservatively and mark important uncertainty.

### 2. Segment into Shots or Visual Events

Create a timeline before prompt writing.

Start a new shot when there is strong evidence of one or more of these changes:

- Hard cut, dissolve, wipe, flash transition, or edit boundary
- Camera angle or viewpoint discontinuity
- Large shot-size discontinuity not explainable by continuous movement
- Scene/location discontinuity
- Major subject/state discontinuity

Do not split a continuous push, pan, orbit, tracking move, or long take merely because framing changes gradually.

For action-heavy continuous shots, divide the shot internally into **action phases** such as anticipation → execution → impact → recovery instead of pretending they are separate edits.

### 3. Reverse-Engineer Each Shot

Analyze each shot using these eight dimensions:

1. **Subject** — identity-relevant appearance, pose, wardrobe, props, relative placement
2. **Action** — action phases, direction, speed, interaction, cause and effect
3. **Environment** — location, foreground/midground/background, spatial anchors, weather, atmosphere
4. **Camera** — shot size, angle, camera position, movement, framing, focus/depth cues
5. **Lighting** — source, direction, softness, contrast, color temperature, practical lights
6. **Style** — realism/stylization, color system, materials, texture, grading, image character
7. **Temporal Continuity** — what remains stable and what visibly changes through time
8. **Narrative Rhythm** — pacing, holds, acceleration, impact beats, reveal timing, edit rhythm

Use [references/video-analysis-framework.md](references/video-analysis-framework.md) when a detailed reconstruction is required.

### 4. Infer Camera Motion Carefully

Identify camera motion from evidence such as:

- Background parallax
- Subject scale change relative to background
- Perspective change
- Horizon/vanishing-point movement
- Occlusion changes
- Stable subject framing while the environment translates

Distinguish among pan, tilt, truck/track, pedestal, dolly in/out, orbit/arc, crane/jib, handheld, zoom, roll, POV/body-mounted motion, and compound moves.

Do not label a move with a technically specific term unless the evidence supports it. Read [references/camera-motion-and-language.md](references/camera-motion-and-language.md) for the inference rules and vocabulary.

### 5. Build the Continuity Block

Extract attributes that should remain stable across the clip:

- Character identity and proportions
- Hair, wardrobe, accessories, props
- Location geometry and recurring background anchors
- Time of day and weather
- Art direction and rendering style
- Lighting logic and color palette
- Texture, lens/image character, grading

Keep these in a **Global Continuity** block. Put only changing information into individual shot instructions.

### 6. Compile the Reverse Prompt

Convert analysis into a generation-oriented prompt with this priority:

**subject/action → spatial relationship → camera → environment → lighting → style → temporal effects → constraints**

For multiple shots, write an explicit time or shot sequence. Preserve edit boundaries rather than merging all shots into one impossible continuous camera move.

For a single continuous shot, express progression as a temporal chain, for example:

`Start ... → then ... → as the camera ... → at the peak ... → end on ...`

If the user names a target generator, apply the relevant adapter in [references/model-adapters.md](references/model-adapters.md). Otherwise return a model-neutral prompt.

Read [references/prompt-compilation.md](references/prompt-compilation.md) when producing a high-fidelity or model-ready final prompt.

### 7. Validate Before Returning

Check the reconstruction against the evidence:

- Every important shot/action beat is represented.
- Shot boundaries are not accidentally rewritten as continuous camera motion.
- Camera motion and subject motion are not conflated.
- Stable character/environment details do not drift between shots.
- Start state, transformation/action, impact/reveal, and end state are temporally coherent.
- The final prompt does not contain unsupported exact lens values, speeds, angles, or hidden details.
- The prompt is usable by a video generator without requiring the model to infer the entire edit structure itself.

If evidence is insufficient, prefer a useful approximate reconstruction plus a short uncertainty note over fabricated certainty.

## Default Output

Unless the user requests another format, return:

1. **Reverse-engineering summary** — one compact paragraph describing the clip's visual strategy.
2. **Shot timeline** — shot/time range, composition, subject action, camera behavior, key transition.
3. **Global continuity** — stable identity, scene, lighting, color, and style constraints.
4. **Final reverse prompt** — generation-ready prompt preserving temporal order and shot structure.
5. **Material uncertainties** — only items that could meaningfully change the reconstruction.

If the user asks for only the prompt, omit the analysis sections and return only the compiled prompt.

## Fidelity Modes

Use the user's requested mode when explicit; otherwise use **faithful**.

- **faithful** — reproduce composition, timing logic, actions, camera language, lighting, and style as closely as evidence allows.
- **structural** — preserve shot grammar, pacing, and motion design while allowing subjects or settings to change.
- **style-only** — extract visual style, lighting, color, texture, and camera character without copying the scene content.
- **prompt-only** — perform the analysis internally and return only the generation prompt.

## Reference Loading

Load only what the task needs:

- Detailed visual/temporal decomposition: [references/video-analysis-framework.md](references/video-analysis-framework.md)
- Shot detection and frame selection: [references/shot-analysis-and-sampling.md](references/shot-analysis-and-sampling.md)
- Camera vocabulary and inference: [references/camera-motion-and-language.md](references/camera-motion-and-language.md)
- Prompt synthesis and output patterns: [references/prompt-compilation.md](references/prompt-compilation.md)
- Generator-specific adaptation: [references/model-adapters.md](references/model-adapters.md)

## Guardrails Against Weak Reconstructions

Do not:

- Treat evenly spaced screenshots as equivalent to true video understanding.
- Describe only the prettiest frame and ignore temporal change.
- Invent actions that occur between sparse frames without indicating uncertainty.
- Confuse a hard cut with a whip pan or fast camera move.
- Confuse digital zoom/crop with physical dolly motion when evidence is weak.
- Add generic cinematic adjectives that are not visible in the reference.
- Repeat long static descriptions inside every shot when they belong in Global Continuity.
- Produce a beautiful prose description that lacks timing, movement, shot grammar, or an executable generation sequence.
