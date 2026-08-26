# Video Analysis Framework

Use this reference when the task needs detailed reconstruction rather than a short prompt-only answer.

## Analysis Goal

Reverse engineering asks a different question from ordinary video captioning:

- Captioning: **What is visible?**
- Reverse engineering: **What sequence of visual instructions could plausibly generate this clip?**

The analysis therefore needs both spatial description and temporal causality.

## Evidence Levels

Classify conclusions implicitly or explicitly by evidence strength:

- **Observed** — directly visible in one or more frames or clearly audible.
- **Strongly inferred** — supported by temporal changes, parallax, continuity, or edit structure.
- **Weakly inferred** — plausible but not distinguishable from alternatives with the available evidence.

Do not turn weak inference into exact technical claims.

Examples:

- A character moves from screen-left to screen-right across consecutive frames: observed.
- Background parallax while subject size remains nearly stable: strong evidence of lateral camera tracking.
- Exact 35 mm focal length from a single frame: weak and usually unnecessary.

## Shot Record

For each shot, reconstruct the following fields.

### 1. Temporal Position

- Start time
- End time
- Approximate duration
- Entry transition
- Exit transition
- Speed treatment: real-time, slow motion, accelerated, freeze/hold, speed ramp

### 2. Subject

Describe identity-relevant and generation-relevant attributes only:

- Subject type and count
- Approximate age/presentation where visually relevant
- Silhouette and body proportions
- Hair and visible facial traits
- Wardrobe, accessories, props
- Initial position and orientation
- Relationships among subjects

Separate attributes that stay stable across the clip from shot-local pose/action.

### 3. Action

Describe motion as a sequence, not a noun.

Prefer:

`leans back → plants right foot → launches forward → rotates torso → strikes target → recoils`

Over:

`fighting dramatically`

Track:

- Direction
- Speed and acceleration
- Contact/interaction
- Cause and effect
- Start state
- Peak action
- End state

For complex actions, use phases:

1. Anticipation
2. Initiation
3. Execution
4. Peak/impact
5. Follow-through
6. Recovery/hold

Not every action needs every phase.

### 4. Environment

Reconstruct spatial organization:

- Location type
- Foreground anchors
- Midground subjects/props
- Background architecture/terrain
- Ground plane and horizon
- Entrances, exits, doors, windows, bridges, roads, furniture, landmarks
- Atmosphere: fog, smoke, dust, rain, snow, particles
- Time of day and weather

Spatial anchors matter because they make camera movement and continuity reproducible.

### 5. Camera

Record only useful observable or strongly inferred features:

- Shot size: ELS / LS / FS / MS / MCU / CU / ECU
- Angle: eye-level / high / low / overhead / worm's-eye / Dutch / POV
- Camera side and relation to subject
- Static vs moving
- Motion type and direction
- Framing behavior
- Focus/depth behavior
- Whether the camera follows, leads, passes, circles, reveals, or holds

Read `camera-motion-and-language.md` before assigning technical motion terms to ambiguous evidence.

### 6. Lighting

Track:

- Primary source: daylight, moonlight, practical, screen, neon, fire, studio source
- Direction: front, side, rim/back, top, under
- Quality: hard, soft, diffused, volumetric
- Contrast ratio impression
- Color temperature
- Motivated practical lights
- Changes during the shot

Do not add cinematic-lighting clichés unless visible.

### 7. Style

Describe the visible image system:

- Photoreal / stylized / animation / anime / 3D / painterly / mixed media
- Production-design language
- Material response
- Palette and saturation
- Contrast
- Texture/grain
- Bloom/halation
- Chromatic aberration
- Lens/image character
- Grading

Avoid relying on artist or director names when direct visual descriptors are sufficient.

### 8. Mood and Rhythm

Mood should be connected to visible design choices.

Track:

- Emotional tone
- Shot duration pattern
- Hold vs rapid change
- Build-up
- Reveal
- Impact beat
- Pause after impact
- Edit acceleration/deceleration

## Cross-Shot Continuity

After per-shot analysis, identify invariants:

- Same character identity
- Same wardrobe and prop state
- Same scene geometry
- Same time of day/weather
- Same palette and lighting motivation
- Same rendering/photographic style

Also track state changes:

- Prop intact → broken
- Character clean → wet/dusty
- Door closed → open
- Light off → on
- Energy core dormant → active

These state transitions should appear explicitly in the generation sequence when they matter.

## Multi-Shot Narrative Logic

For multiple shots, reconstruct why the edit exists.

Common functions:

- Establish → detail → action → reaction
- Wide geography → medium interaction → close-up emphasis
- Anticipation → impact → aftermath
- Reveal → confirmation → response
- Setup → transformation → result
- Procedural montage: repeated action fragments that collectively show a process

Do not flatten these into one continuous camera movement.

## Failure Modes

Reject or revise analysis that:

- Lists objects without temporal relationships.
- Uses generic labels such as "cinematic" instead of visible characteristics.
- Claims exact lens focal lengths without evidence.
- Omits shot boundaries.
- Omits the end state of an action.
- Treats every scale change as a zoom.
- Describes character motion but leaves the camera undefined.
- Describes the camera but leaves subject action vague.
- Repeats unchanged style prose for every shot instead of using a continuity block.
