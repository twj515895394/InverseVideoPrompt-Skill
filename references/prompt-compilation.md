# Prompt Compilation

Use this reference after the clip has been decomposed into shots/events, important temporal changes have been identified, and continuity has been extracted.

## Goal

Convert reverse-engineering analysis into a professional generation prompt that explains not only **what is visible**, but also **how it behaves, changes, and is presented over time**.

A strong reverse prompt can encode, when relevant:

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

Use flexibly, not as a rigid template:

```text
Subject / Performance / Action
→ Spatial & composition relationship
→ Camera behavior and visible frame effect
→ Environment
→ Lighting
→ Material & style
→ Temporal progression / edit grammar
→ Optional recommended audio
→ Continuity
```

The emphasis must follow the video. A facial-performance clip may spend most of its words on performance; an action clip may prioritize movement quality and camera response; a landscape shot may prioritize space, light, atmosphere and camera movement.

---

## Mandatory Three-Pass Professional Refinement

Before writing the final prompt, inspect every important Shot with these three questions. This is a quality pass, not a requirement to make every sentence longer.

### Pass 1 — Emotion → Visible Performance

Ask:

> Is the description still relying on emotional labels such as “tense,” “tired,” “alert,” “sad,” “intimate,” or “restrained” without showing how they appear?

When evidence permits, translate the label into visible behavior:

- gaze direction and gaze hold
- eye / brow / mouth / jaw changes
- breath or swallowing
- head and shoulder tension
- hand behavior
- reduction or increase in movement
- restraint, conflict, release

Weak:

```text
They remain tense and restrained.
```

Better:

```text
Neither character makes a broad emotional gesture. Their mouths stay relatively still, the body posture remains controlled, and attention is held forward or toward the mirror; the tension reads through reduced movement and sustained observation rather than exaggerated reaction.
```

Keep an emotion word if useful, but let it summarize visible evidence rather than replace it.

### Pass 2 — Action Event → Action Quality

Ask:

> Is an important action represented only by a verb?

When useful, add selected movement properties:

- starting state
- hesitation / anticipation
- path
- speed / acceleration
- force / weight
- body participation
- contact mode
- physical response
- follow-through
- ending state
- interaction initiation and response

Weak:

```text
She reaches out and holds his hand.
```

Better:

```text
She slowly extends one hand into the space between them, with a brief hesitation before contact. Without taking his attention off the road, he frees his other hand to respond; their hands overlap at the center of the frame and remain in contact rather than immediately separating.
```

Do not expand a simple movement into invented choreography.

### Pass 3 — Camera Term → Visible Camera Effect

Ask:

> Is the camera description only a technical label such as “handheld,” “tracking,” “slow push-in,” “rack focus,” or “stable shot”?

When evidence permits, explain what changes inside the frame:

- subject scale
- screen position
- foreground/background motion
- parallax
- perspective
- focus / depth allocation
- stability character
- start/stop behavior
- camera-action synchronization

Weak:

```text
Stable shot with slight vibration.
```

Better:

```text
The overall composition stays locked and readable while continuous low-amplitude road vibration causes subtle vertical and lateral drift in the faces, windshield edges and interior lines; the motion feels like vehicle feedback rather than free handheld shake.
```

Weak:

```text
Rack focus from the pursuit cars to the woman.
```

Better:

```text
The distant pursuit vehicles begin as the sharper information inside the mirror while the woman’s reflection remains slightly soft; focus then migrates toward her reflected face, allowing the vehicles to blur as attention shifts from the external threat to her reaction.
```

For the full rules and combined examples, read `professional-description-pillars.md`.

---

## General Description Enrichment

After the three high-priority passes, enrich other dimensions only where they matter.

### Lighting

Weak:

```text
Warm sunlight.
```

Better:

```text
Warm low-angle sunlight enters through the windshield and side windows, catching skin, sunglasses and aged upholstery; passing shadows periodically sweep across the faces and interior, causing the bright and dark areas to change as the car moves.
```

### Environment

Weak:

```text
A desert highway.
```

Better:

```text
A straight road cuts through an exposed, sparsely vegetated desert with a low horizon and light heat shimmer in the distance; pale ground and roadside detail move steadily backward, reinforcing speed and isolation.
```

### Material

Weak:

```text
An old red car with beige interior.
```

Better:

```text
The red paint is slightly sun-faded with uneven soft reflections, while the beige interior shows small creases and aged surface wear consistent with an older vehicle.
```

Enhancement must add observable behavior or surface character, not invented narrative.

---

## Single Continuous Shot

Express progression as a temporal chain:

```text
Start ...
→ then ...
→ gradually ...
→ while/as the camera ...
→ at the threshold/peak ...
→ finally ...
→ end on ...
```

Useful skeleton:

```text
A continuous [shot type] centered on [subject/performance] in [environment].
Start with [opening state + composition].
The subject [visible performance/action progression].
As this changes, the camera [movement + visible framing/parallax/focus effect].
Lighting/material/environment [important temporal behavior].
At the emotional/action peak, [threshold/reveal/impact].
End with [ending state].
Maintain [important continuity].
```

For a performance-heavy close-up, the performance progression may be the dominant part of the entire prompt.

## Performance Compilation

Avoid:

```text
happy → sad → crying
```

Prefer:

```text
The smile begins natural and relaxed. It does not disappear immediately; it first holds, then becomes smaller. Her gaze briefly drops and returns more fixed, the eyes gradually lose their earlier lightness, and moisture starts gathering along the lower eyelids. The lips tighten and the jaw becomes subtly tense as she continues trying to preserve a faint smile. Only near the end does the smile finally lose support and the face approach tears.
```

Keep restrained acting restrained. Read `performance-and-microexpression.md` when facial acting is a major part of the clip.

## Multi-Shot Sequence

Preserve real editing boundaries:

```text
GLOBAL CONTINUITY
...

SHOT 01 — [time/function]
...

HARD CUT / MATCH CUT / DISSOLVE / visible transition

SHOT 02 — ...
```

Each shot can include:

- composition
- performance/action
- action quality
- camera behavior and visible frame effect
- important lighting/environment/material behavior
- temporal progression
- transition out

Do not require every shot to contain every category.

## Action Phase Compilation

When physical action matters, preserve visible phases when useful:

```text
anticipation → initiation → execution → peak/impact → follow-through → recovery
```

Useful language:

- briefly pauses before initiating the movement
- shifts weight before moving
- launches forward with sudden acceleration
- keeps the movement compact and controlled
- contact produces a visible recoil or material response
- momentum carries the body laterally
- decelerates into a stable final pose

Describe speed, weight, force and inertia only when visible.

## Camera Compilation

Prefer observable consequences over invented precision.

Avoid unsupported:

```text
35 mm lens, dolly speed 1.3 m/s, 22-degree yaw
```

Prefer:

```text
The camera smoothly retreats at roughly matching pace, holding the subject at a nearly constant medium scale while the road and roadside environment travel rapidly through the background with strong forward parallax.
```

If the exact technical movement is uncertain, describe what the frame does.

## Composition Compilation

Express meaningful relationships rather than only coordinates.

Example:

```text
The woman occupies the foreground-left with slightly greater scale, while the driver remains in the right midground. The steering wheel and windshield create an interior frame around them, and the rear-view mirror forms a compact secondary visual field that can carry information from the road behind.
```

Do not automatically turn these observations into permanent global constraints.

## Lighting and Material Compilation

Lighting should describe interaction:

```text
Warm sun enters from the side-front direction, producing narrow highlights on faces and sunglasses while much of the cabin remains in dense shadow; passing exterior shadows intermittently move across the interior.
```

Material should describe surface character:

```text
The faded red paint has a sun-aged, slightly desaturated finish with uneven reflections; the beige interior carries fine creases, small scuffs and a dry aged texture.
```

Use qualifiers such as “appears,” “slightly,” or “leather-like” when material identity is uncertain.

## Temporal Change Compilation

Unpack vague words such as “gradually.”

Instead of:

```text
The pursuit cars get closer.
```

write:

```text
They begin as tiny colored flashes deep in the mirror, then slowly increase in scale; the red-blue pulses become more recognizable through the heat distortion until their presence occupies noticeably more of the reflected road.
```

Apply the same idea to:

- expression
- focus
- light
- smoke
- reflection
- distance
- speed
- particles
- object state

## Continuity Compilation

Extract stable details once:

```text
GLOBAL CONTINUITY:
Same character identities, hair and wardrobe; same vehicle and interior; same desert-road geography; consistent hot golden daylight, faded warm palette, realistic skin and aged-material texture across all shots.
```

Avoid repeating the entire block inside every shot.

## Recommended Audio Compilation

Audio is normally an optional **recommended reference** for the target video model or later sound design.

Example:

```text
RECOMMENDED AUDIO:
Consider continuous vintage engine, road and wind texture inside the moving car; subtle cabin vibration and material creaks; restrained low tension during the mirror shot; a small metallic lighter click and ignition texture during the cigar action; near the final hand contact, reduce musical presence and let engine/road ambience carry the moment.
```

Do not imply that these sounds are accurate source reconstruction unless reliable audio evidence exists.

## Style Compilation

Avoid relying on generic words such as:

- cinematic
- beautiful
- epic
- high quality

Translate style into visible properties:

```text
sun-baked gold and faded red palette, fine restrained film grain, realistic skin texture, subtle highlight bloom, sun-aged materials, dense warm daylight and controlled vehicle vibration
```

When combining historical art direction with modern image quality, separate them conceptually:

```text
1970s production design and color character, rendered with modern photorealistic skin and material detail.
```

## Narrative Rhythm

Encode pacing when it matters:

```text
quiet observation → subtle suspicion → rising pursuit pressure → restrained interpersonal reaction → held final beat
```

For montage:

```text
rapid state-changing cuts, progressively tighter detail, each cut advances the process, followed by a longer final hold on the completed state
```

## Constraint Language

Use constraints only when they protect important reconstruction fidelity.

Useful:

```text
Maintain the same character identities and vehicle interior across the sequence.
Preserve the visible hard cuts.
Do not invent specific dialogue when none is established.
```

Avoid huge generic negative-prompt lists or over-constraining every minor screen position.

## Output Density

### Compact

Use for simple clips or when the user wants only the prompt.

### Detailed

Use for multiple shots, meaningful performance, complex motion, visual continuity or rich style.

### Production

Use for close reconstruction with:

- global continuity
- shot timeline
- performance/action progression
- professional three-pass refinement
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
- Are important emotions translated into visible acting?
- Are important actions more than isolated verbs?
- Does camera language explain visible frame behavior?
- Are lighting/material/environment descriptions concrete and visual?
- Are important temporal changes explicit?
- Are cuts preserved?
- Are stable details consistent?
- Is unsupported technical precision removed?
- Is recommended audio clearly presented as reference rather than source fact?
- Is the result rich and professional without becoming rigid or over-constrained?

If a Shot already answers the three professional questions clearly, do not keep expanding it. **Professional quality comes from precise visible process, not maximum word count.**