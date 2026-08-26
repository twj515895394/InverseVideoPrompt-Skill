# Prompt Compilation

Use this reference after the video has been decomposed into shots/events, important changes have been identified, and continuity has been extracted.

## Goal

Convert reverse-engineering analysis into a professional generation prompt that explains not only **what is visible**, but also **how it behaves and changes over time**.

A strong reverse prompt should encode, when relevant:

- subject identity and state
- visible performance and micro-expression
- action process and physical quality
- spatial/compositional relationships
- camera behavior and its visible effect
- environment depth and atmosphere
- lighting behavior
- materials and image character
- temporal progression
- edit grammar
- stable continuity
- optional recommended sound reference

## Canonical Prompt Order

Use flexibly rather than as a rigid template:

```text
Subject / Performance / Action
→ Spatial & composition relationship
→ Camera behavior
→ Environment
→ Lighting
→ Material & style
→ Temporal progression / edit grammar
→ Optional recommended audio
→ Continuity
```

The emphasis should follow the video. A facial-performance clip should spend more words on performance; a landscape shot should spend more on camera, light, atmosphere and space.

## Description Enrichment Before Compilation

Before writing the final prompt, check whether important observations are still too generic.

### Emotion

Weak:

```text
She becomes sad.
```

Better:

```text
Her smile first pauses rather than disappearing; her gaze briefly drops, the eyes lose their earlier lightness, the lips slowly tighten, and moisture begins to gather in the eyes while she tries to hold the expression together.
```

### Action

Weak:

```text
She pushes his arm away.
```

Better:

```text
After a short hesitation, she uses her forearm and shoulder to slowly guide his arm away, the movement restrained but deliberate, then subtly shifts her body farther toward the door.
```

### Camera

Weak:

```text
Slight handheld movement.
```

Better:

```text
The framing remains generally stable but carries continuous low-amplitude irregular vibration, causing subtle drift in the faces and interior lines rather than exaggerated shake.
```

### Lighting

Weak:

```text
Warm sunlight.
```

Better:

```text
Hard warm sunlight enters diagonally through the windshield, catching skin, sunglasses and beige upholstery; alternating road shadows repeatedly cut across the faces, creating moving bands of bright heat and dense shadow.
```

### Environment

Weak:

```text
A desert highway.
```

Better:

```text
A straight highway runs through an exposed, nearly empty desert with a low horizon and visible heat shimmer in the distance; pale sand and sparse roadside detail streak backward, reinforcing speed and isolation.
```

Enhancement should add observable behavior, not invented narrative.

## Single Continuous Shot

Express the visible progression as a temporal chain:

```text
Start ...
→ then ...
→ gradually ...
→ while/as the camera ...
→ at the threshold/peak ...
→ finally ...
→ end on ...
```

Example skeleton:

```text
A continuous [shot type] centered on [subject/performance] in [environment].
Start with [opening state + composition].
The subject [visible performance/action progression].
As this changes, the camera [movement + visible framing/parallax effect].
Lighting/material/environment [important temporal behavior].
At the emotional/action peak, [threshold/reveal/impact].
End with [ending state].
Maintain [important continuity].
```

For a performance-heavy close-up, the “performance progression” may be the dominant part of the entire prompt.

## Performance Compilation

When acting is central, prefer a **Performance Timeline** or continuous emotional progression.

Avoid:

```text
happy → sad → crying
```

Prefer:

```text
The smile begins natural and relaxed. It does not vanish immediately; it first holds a little too long, then becomes smaller. Her gaze briefly drops and returns, now more fixed and less playful. Moisture slowly gathers along the eyes while the lips tighten and the jaw becomes subtly tense. She continues trying to maintain a faint smile even after the eyes have become visibly emotional. Only near the end does the smile finally collapse and the face approach tears.
```

Keep the intensity faithful to the reference: restrained acting should remain restrained.

Read `performance-and-microexpression.md` when facial acting is a major part of the clip.

## Multi-Shot Sequence

Do not merge editing boundaries into fake continuous camera moves.

Recommended structure:

```text
GLOBAL CONTINUITY
...

SHOT 01 — [time/function]
...

HARD CUT / MATCH CUT / DISSOLVE / other visible transition

SHOT 02 — ...
```

Each shot can include:

- composition
- subject performance/action
- camera behavior
- important lighting/environment/material change
- temporal progression inside the shot
- transition out

Do not require every shot to contain every category.

## Action Phase Compilation

When physical action matters, preserve visible phases:

```text
anticipation → initiation → execution → peak/impact → follow-through → recovery
```

Useful language:

- briefly shifts weight before moving
- launches forward with a sudden acceleration
- movement stays compact and controlled
- momentum carries the body laterally
- the motion decelerates into a stable end pose

Describe speed, weight, force and inertia only when visible.

## Camera Compilation

Prefer observable consequences over invented precision.

Avoid unsupported:

```text
35 mm lens, dolly speed 1.3 m/s, 22-degree yaw
```

Prefer:

```text
The camera smoothly tracks backward at matching speed, keeping the subject at a nearly constant medium scale while the road and roadside environment move rapidly through the background with strong forward parallax.
```

If the exact technical movement is uncertain, describe what the frame does.

## Composition Compilation

When composition is meaningful, express relationships rather than only coordinates.

Example:

```text
The woman carries slightly less visual weight on the left side of the frame, while the driver sits closer to camera on the right. The steering wheel and windshield create a lower/front frame, and the central rear-view mirror becomes a visual anchor between them, later carrying the pursuit information.
```

Do not turn this into a hard global constraint unless the reference truly depends on it.

## Lighting and Material Compilation

Lighting should describe visible interaction:

```text
Hard sun enters from front-left, producing warm facial highlights and dense interior shadows; passing roadside shadows move rapidly across the skin and sunglasses.
```

Material should describe surface character:

```text
The faded red paint has a sun-aged, slightly desaturated finish with uneven reflections; the beige interior shows small creases and wear consistent with an older vehicle.
```

Use qualifiers such as “appears,” “slightly,” or “leather-like” when material identity is uncertain.

## Temporal Change Compilation

Video prompts become stronger when “gradually” is unpacked.

Instead of:

```text
The pursuit cars get closer.
```

write:

```text
They begin as tiny colored flashes deep in the mirror, then slowly grow in scale; the red-blue pulses become clearer through the heat distortion until the pursuit feels visibly closer and more threatening.
```

Apply the same idea to:

- expression
- focus
- light
- smoke
- reflections
- distance
- speed
- particles
- object state

## Continuity Compilation

Extract stable details once:

```text
GLOBAL CONTINUITY:
Same character identities, wardrobe and hair; same vehicle interior and desert-road geography; consistent hot golden daylight, faded warm color palette, realistic skin and aged-material texture throughout.
```

Avoid repeating the entire block inside every shot.

## Recommended Audio Compilation

Audio is normally an optional **recommended reference**, especially when source audio cannot be reliably verified.

Example:

```text
RECOMMENDED AUDIO:
Continuous engine, road and wind texture inside the moving car; subtle cabin vibration and fabric movement; distant pursuit sirens can gradually become more noticeable; restrained low tension in the score; tire/sand texture grows when the car leaves the paved road.
```

Use language such as “recommended,” “suitable,” “consider,” or “can include” when appropriate.

If the target model supports native audio, integrate compact audio cues into the relevant timeline. Otherwise return them as a separate optional sound-design block.

Read `audio-inference-and-design.md` for details.

## Style Compilation

Do not rely on generic words such as:

- cinematic
- beautiful
- epic
- high quality

Translate them into visible properties:

```text
sun-baked gold and faded red palette, fine restrained film grain, realistic skin texture, subtle highlight bloom, slightly aged surfaces, dense warm daylight and controlled handheld/vehicle vibration
```

If mixing historical art direction with modern image quality, separate them conceptually:

```text
1970s production design and color character, rendered with modern photorealistic skin/material detail.
```

## Narrative Rhythm

Encode pacing when it matters:

```text
quiet observation → subtle suspicion → rising pursuit pressure → restrained interpersonal reaction → decisive final beat
```

For montage:

```text
rapid state-changing cuts, progressively tighter detail, each cut advances the process, followed by a longer final hold on the completed result
```

## Constraint Language

Use constraints only when they protect important reconstruction fidelity.

Useful:

```text
Maintain the same character identities and vehicle interior across the sequence.
Do not turn visible hard cuts into one continuous camera move.
Do not invent dialogue when none is established.
```

Avoid huge generic negative-prompt lists or over-constraining every minor screen position.

## Output Density

### Compact

Simple clip or user only wants a prompt.

### Detailed

Multiple shots, meaningful performance, complex motion, visual continuity or rich style.

### Production

Close reconstruction with:

- global continuity
- shot timeline
- performance/action progression
- camera and composition
- lighting/material/environment
- temporal changes
- edit grammar
- optional recommended audio
- final compiled prompt

## Final Quality Check

Before returning:

- Is the prompt chronological?
- Does it explain important changes rather than only list properties?
- Are emotions translated into visible acting when possible?
- Are actions described with useful movement quality?
- Does camera language include visible frame behavior?
- Are lighting/material/environment descriptions concrete and visual?
- Are important temporal changes explicit?
- Are cuts preserved?
- Are stable details consistent?
- Is unsupported technical precision removed?
- Is recommended audio clearly presented as reference rather than fact?
- Is the result rich and professional without becoming rigid or over-constrained?
