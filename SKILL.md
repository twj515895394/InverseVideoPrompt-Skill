---
name: inverse-video-prompt
description: "将参考视频、视频片段、时间戳截图或连续帧序列逆向分析为忠实、完整、可直接用于 AI 视频生成的视频提示词。用于反推视频 Prompt、分析参考视频、复刻镜头语言、主体动作、运镜、场景空间、光影、视觉风格、时间连续性、叙事节奏，以及推测原视频声音并推荐环境声、动作拟音、电影化音效、音乐与动态留白；可输出适用于 Seedance、MiniMax/Hailuo、Kling、Veo、Wan 等视频模型的提示词。"
metadata:
  short-description: "反推视频的镜头、动作、运镜、光影、声音与节奏，生成可直接使用的视频提示词"
---

# 视频提示词反推（Inverse Video Prompt）

> **角色定位：** 从参考视频的时间连续视觉与音频证据中，逆向还原其可能的生成意图、镜头设计与声音设计。目标不是简单描述“画面里有什么”，而是重建“这个视频是如何被拍摄、运动、剪辑、发声和组织出来的”。

## Core Principles

1. **Analyze shots before prompts.** Segment the clip into shots or coherent visual events before writing the final prompt.
2. **Prefer temporal evidence over isolated frames.** Describe what changes from start to middle to end, not only what individual frames contain.
3. **Separate observation from inference.** State uncertain camera motion, hidden actions, lens choices, transitions, or sounds conservatively instead of inventing precision.
4. **Separate subject motion from camera motion.** A subject growing larger may be subject approach, camera push-in, zoom, or a combination; infer from background parallax and framing changes.
5. **Preserve stable continuity separately from changing action.** Identity, wardrobe, environment, art direction, color palette, lighting continuity, and recurring ambience should not be repeatedly rediscovered per shot.
6. **Separate heard, inferred, and recommended audio.** Distinguish what is actually audible from what the visuals imply and what would improve generation or post-production.
7. **Compile for generation.** The final result should tell a video model what to generate over time, not read like a film-review paragraph.
8. **Match the requested fidelity.** Reconstruct the reference faithfully by default. Adapt or redesign only when the user explicitly asks for variation.

## Workflow

### 1. Establish the Evidence

Determine what evidence is actually available:

- Full video with direct visual/audio inspection
- Video file that can be sampled or decoded with tools
- Timestamped screenshots or extracted frames
- Untimestamped frame sequence
- Storyboard or contact sheet only

If the full video is available, scan the complete clip before detailed analysis. Record duration, aspect ratio, obvious cuts, scene changes, speed changes, major action beats, and the presence or absence of usable source audio.

If frames must be extracted, do **not** use uniform sampling as the only evidence when the clip may contain cuts or fast actions. Use shot-aware and event-aware sampling. Read [references/shot-analysis-and-sampling.md](references/shot-analysis-and-sampling.md).

If only sparse screenshots are available, infer temporal behavior and sound conservatively and mark important uncertainty.

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

Analyze each shot using these eight visual/temporal dimensions:

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
- Recurring ambience or acoustic-space character when supported

Keep these in a **Global Continuity** block. Put only changing information into individual shot instructions.

### 6. Reverse-Engineer and Recommend Sound

Analyze sound as a first-class temporal layer rather than an optional afterthought.

When source audio is available, first identify what is actually audible. When audio is missing, muted, incomplete, or unreliable, infer conservatively from visible events.

Always distinguish three categories:

- **已确认 / Observed** — directly audible or explicitly provided by the user.
- **高概率推测 / Inferred** — strongly supported by visible action, material interaction, environment, or edit rhythm.
- **创作推荐 / Recommended** — not asserted as original audio; proposed to improve realism, rhythm, impact, atmosphere, or generation quality.

Analyze or recommend these sound layers:

1. **Dialogue / Vocal** — dialogue, narration, shouts, breath, laughter, vocal effort, lip-sync requirement
2. **Foley / Action SFX** — footsteps, cloth, object handling, impacts, doors, mechanical interactions, material feedback
3. **Environmental Ambience** — room tone, wind, traffic, crowd, machinery, rain, forest, spatial background
4. **Cinematic / Designed SFX** — whoosh, riser, sub-hit, reverse swell, transition sweep, tonal drone, energy charge
5. **Music** — genre character, instrumentation, pulse, pacing, emotional role, build/drop/stop behavior
6. **Silence / Dynamic Contrast** — intentional pauses, pre-impact silence, post-reveal hold, ambience removal and return

Bind sound events to the shot timeline and action phases. For example:

`anticipation → breath/cloth movement → execution → motion whoosh → impact → contact hit + low-frequency accent → recovery → debris/room tail + ambience return`

Do not invent exact dialogue from lip movement alone. Do not add whooshes to every camera move. Do not describe a Recommended sound as if it were confirmed in the source.

Read [references/audio-inference-and-design.md](references/audio-inference-and-design.md) whenever the user wants sound inference, audio recommendations, audiovisual reconstruction, or a production-ready prompt.

### 7. Compile the Reverse Prompt

Convert analysis into a generation-oriented prompt with this priority:

**subject/action → spatial relationship → camera → environment → lighting → style → temporal effects → sound/audio intent → constraints**

For multiple shots, write an explicit time or shot sequence. Preserve edit boundaries rather than merging all shots into one impossible continuous camera move.

For a single continuous shot, express progression as a temporal chain, for example:

`Start ... → then ... → as the camera ... → at the peak ... → end on ...`

If the target model supports native audio generation, integrate only the necessary sound instructions into the video prompt while preserving audiovisual timing. If the target model is primarily visual or audio support is uncertain, output a separate **Audio / Sound Design Prompt** instead of overloading the visual prompt.

If the user names a target generator, apply the relevant adapter in [references/model-adapters.md](references/model-adapters.md). Otherwise return a model-neutral prompt.

Read [references/prompt-compilation.md](references/prompt-compilation.md) when producing a high-fidelity or model-ready final prompt.

### 8. Validate Before Returning

Check the reconstruction against the evidence:

- Every important shot/action beat is represented.
- Shot boundaries are not accidentally rewritten as continuous camera motion.
- Camera motion and subject motion are not conflated.
- Stable character/environment details do not drift between shots.
- Start state, transformation/action, impact/reveal, and end state are temporally coherent.
- The final prompt does not contain unsupported exact lens values, speeds, angles, hidden details, or invented dialogue.
- Confirmed sound, inferred sound, and recommended sound are clearly separated.
- Important sound events align with visible actions, edit points, spatial materials, and rhythm.
- The prompt is usable by a video generator without requiring the model to infer the entire edit structure itself.

If evidence is insufficient, prefer a useful approximate reconstruction plus a short uncertainty note over fabricated certainty.

## Default Output

Unless the user requests another format, return:

1. **反推摘要** — one compact paragraph describing the clip's visual and audiovisual strategy.
2. **镜头时间线** — shot/time range, composition, subject action, camera behavior, key transition.
3. **全局连续性** — stable identity, scene, lighting, color, style, and recurring ambience constraints.
4. **声音反推与推荐** — separate confirmed/inferred source audio from recommended ambience, Foley, designed SFX, music, and silence.
5. **最终反推视频提示词** — generation-ready prompt preserving temporal order and shot structure.
6. **Audio / Sound Design Prompt** — include separately when useful or when the target video model does not natively handle audio.
7. **关键不确定项** — only items that could meaningfully change the reconstruction.

If the user asks for only the prompt, perform the analysis internally and return the compiled video prompt; include a compact audio block only when sound materially affects the requested result.

## Fidelity Modes

Use the user's requested mode when explicit; otherwise use **faithful**.

- **faithful** — reproduce composition, timing logic, actions, camera language, lighting, style, and likely sound behavior as closely as evidence allows.
- **structural** — preserve shot grammar, pacing, motion design, and audiovisual rhythm while allowing subjects or settings to change.
- **style-only** — extract visual style, lighting, color, texture, camera character, and optionally sound character without copying the scene content.
- **prompt-only** — perform the analysis internally and return only the generation prompt.

## Reference Loading

Load only what the task needs:

- Detailed visual/temporal decomposition: [references/video-analysis-framework.md](references/video-analysis-framework.md)
- Shot detection and frame selection: [references/shot-analysis-and-sampling.md](references/shot-analysis-and-sampling.md)
- Camera vocabulary and inference: [references/camera-motion-and-language.md](references/camera-motion-and-language.md)
- Sound inference and recommended sound design: [references/audio-inference-and-design.md](references/audio-inference-and-design.md)
- Prompt synthesis and output patterns: [references/prompt-compilation.md](references/prompt-compilation.md)
- Generator-specific adaptation: [references/model-adapters.md](references/model-adapters.md)
- Calibration examples for continuous shots, multi-shot action, montage, and sparse frames: [references/examples.md](references/examples.md)

## Guardrails Against Weak Reconstructions

Do not:

- Treat evenly spaced screenshots as equivalent to true video understanding.
- Describe only the prettiest frame and ignore temporal change.
- Invent actions that occur between sparse frames without indicating uncertainty.
- Confuse a hard cut with a whip pan or fast camera move.
- Confuse digital zoom/crop with physical dolly motion when evidence is weak.
- Add generic cinematic adjectives that are not visible in the reference.
- Invent exact dialogue, lyrics, or specific source sounds without evidence.
- Turn every camera move into a whoosh or every cut into an impact.
- Mix confirmed source audio with creative sound recommendations without labeling them.
- Repeat long static descriptions inside every shot when they belong in Global Continuity.
- Produce a beautiful prose description that lacks timing, movement, shot grammar, sound logic, or an executable generation sequence.
