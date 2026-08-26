# Prompt Compilation

Use this reference after the video has been segmented and analyzed. Its purpose is to convert evidence into instructions a video generator can execute.

## Compilation Principle

A reverse prompt should preserve the reference clip's **temporal grammar**:

- what is stable
- what changes
- when it changes
- what the subject does
- what the camera does
- where cuts occur
- what the shot ends on

Do not flatten a multi-shot clip into one descriptive paragraph.

## Information Priority

Compile in this order unless the target model benefits from another syntax:

1. Subject identity and starting state
2. Subject action and interaction
3. Spatial relationship and environment
4. Camera shot/angle/movement
5. Lighting and atmosphere
6. Visual style and image character
7. Temporal effects, transitions, speed treatment
8. Continuity and negative constraints

## Stable vs Dynamic Information

### Global Continuity

Place repeated stable information here:

- Character appearance
- Wardrobe
- Key props
- Location geometry
- Time/weather
- Art direction
- Color palette
- Lighting logic
- Render/photographic style
- Image texture/grading

### Shot-Local Information

Place changing information here:

- Pose/action
- Position
- Camera angle and shot size
- Camera movement
- Focus target
- Prop state
- Local lighting changes
- Effects
- Cut/transition

This prevents prompt bloat and reduces continuity drift.

## Single Continuous Shot Template

Use temporal connectors rather than comma-stacking unrelated instructions.

```text
[GLOBAL CONTINUITY]

Start: [opening composition and state].
Then: [first action progression] while [camera behavior].
As: [second action/reveal], [environment/effect change].
Peak: [impact/highest-information moment] with [camera/focus/speed behavior].
End: [final composition, subject state, camera state].

Constraints: [only meaningful continuity or failure-prevention constraints].
```

## Multi-Shot Template

```text
[GLOBAL CONTINUITY]

SHOT 01 — [time range / duration]
[shot size + angle]. [subject starting state]. [action progression]. [camera movement]. [lighting/effect]. End on [final state].

CUT / TRANSITION

SHOT 02 — [time range / duration]
...

SHOT 03 — ...

Overall rhythm: [edit pacing / acceleration / holds].
Constraints: [continuity and critical exclusions].
```

Do not write `CUT` when evidence supports a continuous move.

## Shot Prompt Formula

A strong shot instruction normally contains:

`shot setup + subject action + camera behavior + spatial anchors + visible change + end state`

Example:

`Low-angle medium-wide on a runner entering from frame left. He accelerates across the wet street toward camera-right while the camera tracks laterally at matching speed; foreground railings streak past faster than the distant storefronts. Neon reflections ripple underfoot. End as he plants one foot and compresses into a jump preparation.`

The value comes from causal and temporal detail, not adjective count.

## Action Language

Prefer verbs with state change:

- turns
- leans
- plants
- raises
- reaches
- releases
- recoils
- opens
- collapses
- ignites
- expands
- fractures
- settles

Prefer ordered action chains:

`raises the device → thumb presses the switch → core flickers → ring lights sequentially → energy stabilizes`

Avoid vague action language:

- does an action
- moves dynamically
- fights intensely
- performs cinematic movement

## Camera Language

Prefer explicit progression:

`camera begins static in a medium shot, then slowly dollies forward as the subject turns, ending in a close-up`

Avoid:

`cinematic dynamic camera`

When motion is uncertain, describe the visible framing result:

`framing closes from medium-wide to close-up`

rather than fabricating the exact rig motion.

## Rhythm and Timing

Timing can be expressed as:

- Absolute ranges: `0.0–1.8s`
- Relative duration: `for the first two seconds`
- Beat sequence: `brief hold → sudden acceleration → impact → half-second recovery hold`

For reference reconstruction, exact timestamps are useful only when the evidence provides reliable timing.

## Transitions

Use explicit edit language only when visible:

- hard cut
- match cut
- smash cut
- cross dissolve
- fade to black
- flash transition
- wipe
- whip-pan transition

If transition mechanics are uncertain, use `cut to` instead of inventing a special transition.

## Speed Treatment

Describe speed changes at the affected event:

- real-time
- slow motion
- brief speed ramp into impact
- accelerated montage
- freeze/hold

Do not apply `slow motion` to the entire clip when only the impact beat slows down.

## Effects

Describe effect evolution, not only presence.

Weak:

`blue energy effect`

Better:

`a faint blue pulse appears inside the core, brightens in two beats, sends thin arcs around the outer ring, then stabilizes into a continuous glow`

## Negative Constraints

Use negative constraints sparingly. Include only likely failure modes that matter to reconstruction, such as:

- no extra characters
- no wardrobe change
- no camera cut during a continuous take
- keep prop in right hand throughout
- no unexplained scene change
- no text/watermark

Do not append generic long negative-prompt boilerplate unless the target workflow specifically needs it.

## Fidelity Modes

### Faithful

Preserve:

- Subject
- Scene
- Shot design
- Action timing
- Camera grammar
- Lighting
- Style

### Structural

Preserve:

- Shot sequence
- Action architecture
- Camera movement
- Pacing
- Reveal/impact logic

Allow subject, costume, and location replacement.

### Style-Only

Extract:

- Palette
- Lighting
- Image texture
- Rendering style
- Lens/image character
- Typical framing/motion character

Do not copy scene-specific content unless requested.

## Default Reverse-Engineering Output Pattern

When analysis is requested, use:

```text
### Reverse-engineering summary
...

### Shot timeline
| Shot | Time | Composition | Action | Camera | Transition |
|---|---:|---|---|---|---|
| 01 | ... | ... | ... | ... | ... |

### Global continuity
...

### Final reverse prompt
...

### Uncertainty
...
```

Keep uncertainty short and include only items that materially affect reconstruction.

## Final Self-Check

Before returning a compiled prompt, ask:

- Can a generator tell what happens first, next, and last?
- Can it distinguish subject motion from camera motion?
- Are cuts and continuous moves represented correctly?
- Are important state changes explicit?
- Is stable continuity centralized instead of repeated?
- Are unsupported details removed?
- Would removing generic adjectives leave the core choreography intact?

If the last answer is no, the prompt is probably too descriptive and not sufficiently procedural.
