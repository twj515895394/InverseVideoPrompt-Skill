# Prompt Compilation

Use this reference after the video has already been decomposed into shots/events and continuity has been extracted.

## Goal

Convert reverse-engineering analysis into instructions a video generator can execute over time.

A good reverse prompt is not a film review and not a static image prompt. It should encode:

- what is visible
- what changes
- when it changes
- how the subject moves
- how the camera responds
- which details must remain stable
- where cuts or transitions occur
- how the clip begins and ends
- which sound events are confirmed, inferred, or recommended when audio matters

## Canonical Prompt Order

Use this priority unless a target-model adapter overrides it:

```text
Subject / Action
→ Spatial relationship
→ Camera behavior
→ Environment
→ Lighting
→ Style
→ Temporal effects / edit grammar
→ Sound / audio intent
→ Continuity and negative constraints
```

## Single Continuous Shot

Express progression as a temporal chain:

```text
Start ...
→ then ...
→ while/as the camera ...
→ at the peak ...
→ finally ...
→ end on ...
```

Example skeleton:

```text
A continuous [shot type] of [subject] in [environment].
Start with [opening state/composition].
The subject [action phase 1], then [action phase 2].
As this happens, the camera [primary move], keeping [framing/spatial constraint].
At the peak, [impact/reveal/transformation].
The motion settles into [ending state].
Maintain [identity/wardrobe/scene/lighting/style continuity].
```

If sound is relevant and supported by the workflow, add synchronized events inside the same temporal chain rather than appending a disconnected sound list.

## Multi-Shot Sequence

Do not merge editing boundaries into fake continuous camera moves.

Recommended structure:

```text
GLOBAL CONTINUITY
...

SHOT 01 — [time or function]
...

HARD CUT / MATCH CUT / DISSOLVE / WHIP TRANSITION

SHOT 02 — ...
```

For each shot include only information that changes or matters specifically to that shot.

## Action Phase Compilation

When a shot contains strong physical action, preserve visible phases:

```text
anticipation → initiation → execution → peak/impact → follow-through → recovery
```

Do not force every phase when it is not visible.

Useful language:

- gathers weight before moving
- suddenly launches forward
- accelerates through frame
- twists mid-motion
- reaches the peak of the jump
- collides at the center of frame
- momentum carries both subjects laterally
- settles into a recovery stance

## Camera Compilation

Convert technical analysis into readable generation instructions.

Instead of:

```text
35 mm lens, dolly speed 1.3 m/s, 22-degree yaw
```

when those values are unsupported, write:

```text
The camera smoothly tracks backward at matching speed, holding a stable medium framing while the background shows strong forward parallax.
```

Prefer observable consequences over invented numerical precision.

## Continuity Compilation

Extract stable details once:

```text
GLOBAL CONTINUITY:
Same character identity and proportions, same black coat and silver pendant, same narrow rain-soaked alley, cool cyan practical lighting with warm shop-window accents, shallow mist, realistic cinematic texture and muted contrast throughout.
```

Then avoid re-describing this entire block in every shot.

## Audio Compilation

When audio matters, preserve the distinction between **source reconstruction** and **creative recommendation**.

### Confirmed / inferred source-audio block

Use only sounds directly audible or strongly supported by visible evidence:

```text
LIKELY SOURCE AUDIO:
Wet footsteps synchronized to the sprint; diffuse underground-garage room tone; a heavy metal door contact and slam with short concrete reverb.
```

### Recommended sound-design block

Add creative enhancement separately:

```text
RECOMMENDED SOUND DESIGN:
Add a restrained low-frequency tension drone, briefly thin the ambience before the door slam, then reinforce the slam with one subtle sub-bass accent. Avoid repeated whooshes.
```

### Audiovisual timeline

For high-fidelity reconstruction, align audio to the same timeline as visual events:

```text
0.0-1.8s — visual action ... | audio: ambience + footsteps
1.8-2.4s — visual action ... | audio: breath/cloth rise
2.4s — impact/cut | audio: synchronized contact hit
2.4-3.0s — recovery | audio: reverb tail + ambience return
```

### Native-audio vs separate-audio workflows

If the target workflow supports synchronized native audio generation, integrate only the necessary sound instructions into the main video prompt.

If native audio is absent, unknown, or handled by another tool/model, return:

```text
VIDEO PROMPT
...

AUDIO / SOUND DESIGN PROMPT
...
```

Do not overload a visual-only generator with a long audio specification that it cannot use.

## Style Compilation

Do not rely on generic words such as:

- cinematic
- beautiful
- epic
- high quality

Translate style into visible properties:

```text
cool desaturated palette, hard side lighting, slightly crushed blacks, fine film grain, restrained highlight bloom, realistic skin texture, damp reflective surfaces
```

## Narrative Rhythm

Encode pacing when it is visually important:

```text
brief anticipation hold → rapid acceleration → sharp impact → short recovery hold
```

For montage:

```text
fast 0.5–1 second cuts, progressively tighter framing, each cut advances the machine to a clearly more assembled state, then a longer final hold on activation
```

## Negative / Constraint Language

Use constraints only when they protect reconstruction fidelity.

Examples:

```text
Do not change the character's clothing between shots.
Do not reverse left/right screen direction across the cut.
Do not turn the hard cut into one continuous orbit.
Do not add new background characters.
Do not reveal the final state before the last shot.
Do not invent dialogue when none is confirmed.
```

Avoid huge generic negative-prompt lists unrelated to the reference.

## Output Density

Choose prompt density based on the task:

### Compact

Use when the user asks for a quick prompt or the clip is simple.

### Detailed

Use when the clip contains multiple shots, complex motion, important continuity, or meaningful audio design.

### Production

Use when the user wants close reproduction. Include:

- global continuity
- shot timeline
- action phases
- camera behavior
- lighting/style
- edit grammar
- source-audio inference
- recommended sound design
- audiovisual timing when useful
- final compiled model prompt

## Final Quality Check

Before returning the prompt, verify:

- It has a clear beginning and end.
- Important actions occur in the correct order.
- Cuts are explicit.
- Camera and subject motion are distinguishable.
- Stable details are protected.
- The prompt is chronological rather than a bag of adjectives.
- Unsupported technical precision has been removed.
- Confirmed/inferred sound is not mixed with recommended sound.
- Audio events align with visual timing where relevant.
- The target model can plausibly use the prompt format.
