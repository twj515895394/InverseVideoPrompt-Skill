# Video Analysis Framework

Use this reference for detailed reverse-engineering of a reference video. The goal is to reconstruct the generative logic of the clip rather than produce a generic visual description.

## Analysis Hierarchy

Analyze from large structure to small detail:

1. Clip-level intent and rhythm
2. Shot / visual-event segmentation
3. Shot-level subject, action, environment, camera, lighting, style
4. Cross-shot temporal continuity
5. Audio evidence, sound inference, and audiovisual rhythm
6. Global continuity
7. Final generation-oriented prompt compilation

## 1. Subject

Record only identity-relevant or generation-relevant attributes:

- person / creature / object type
- visible age range or design category when useful
- hair, silhouette, proportions
- wardrobe and accessories
- important props
- body orientation
- position in frame
- relationship to other subjects

Do not over-describe minor details that do not affect reconstruction.

## 2. Action

Treat actions as temporal processes, not static labels.

Useful fields:

- opening pose/state
- anticipation
- initiation
- execution
- peak/impact
- follow-through
- recovery/end state
- screen direction
- acceleration/deceleration
- interaction target
- cause-and-effect relationship

For simple actions, use only the phases that are actually visible.

## 3. Environment

Describe spatially meaningful scene information:

- location type
- foreground / midground / background layers
- entrances/exits
- recurring anchors
- surfaces and materials
- weather and atmosphere
- time of day
- crowd/traffic/background activity
- depth and scale

Prioritize details that help preserve camera geography and continuity.

## 4. Camera

Analyze:

- shot size
- angle
- camera height
- subject-camera distance
- camera movement
- framing behavior
- focus/depth cues
- stabilization character
- foreground parallax
- perspective change

Separate camera motion from subject motion. Read `camera-motion-and-language.md` when the distinction is uncertain.

## 5. Lighting

Identify visible lighting logic:

- primary source
- source direction
- hard / soft
- contrast
- key-to-fill relationship
- color temperature
- practical sources
- rim/back light
- volumetric effects
- exposure behavior
- highlight bloom or clipping

Do not invent exact fixture types when only light behavior is visible.

## 6. Style

Translate vague style into visible properties:

- photorealistic / stylized / animation / illustrative
- color palette
- saturation and contrast
- materials and texture
- skin rendering
- grain / noise
- bloom / diffusion
- sharpness
- lens/image character
- grading
- motion rendering character

Avoid generic adjectives without visible evidence.

## 7. Temporal Continuity

For each shot or event, ask:

### What stays stable?

- identity
- clothing
- object design
- scene geometry
- lighting logic
- color palette
- visual style

### What changes?

- subject pose/action
- object state
- camera position
- framing
- focus
- environment state
- light intensity
- particles/effects

The final prompt should preserve the stable set and explicitly sequence the changing set.

## 8. Narrative Rhythm

Record the temporal function of each beat:

- setup
- hold
- anticipation
- acceleration
- reveal
- impact
- pause
- recovery
- transition
- climax

For montage, identify whether edits are driven by:

- process state changes
- rhythmic matching
- action matching
- spatial progression
- escalation
- contrast

Rhythm should be encoded in the final prompt when it affects generation.

## 9. Sound and Audiovisual Rhythm

Treat sound as a temporal layer aligned to the same shot and action timeline.

First determine evidence quality:

- usable original audio exists
- partial/noisy audio exists
- video is muted
- only visual frames are available

Then separate:

- **Observed** — directly audible
- **Inferred** — strongly implied by visible events/materials/environment
- **Recommended** — creative enhancement for generation or post-production

Check six sound layers:

1. dialogue/vocal
2. Foley/action SFX
3. environmental ambience
4. cinematic/designed SFX
5. music
6. silence/dynamic contrast

Ask how sound relates to visible rhythm:

- Does an impact coincide with an action peak?
- Does ambience establish the location?
- Does music accelerate with the cut rate?
- Is there a deliberate silence before a reveal or impact?
- Does a transition sound bridge two edits?
- Are footsteps, mechanical clicks, doors, splashes, or collisions synchronized to visible contact?

Do not infer exact dialogue from visible mouth movement. Do not treat generic cinematic sound effects as evidence of the original soundtrack.

For detailed rules, read `audio-inference-and-design.md`.

## Shot Record Template

A detailed shot record can use:

```text
SHOT ID:
TIME RANGE:
FUNCTION:

SUBJECT:
ACTION:
ENVIRONMENT:
CAMERA:
LIGHTING:
STYLE:
AUDIO OBSERVED/INFERRED:
AUDIO RECOMMENDED:

OPENING STATE:
PEAK EVENT:
ENDING STATE:
TRANSITION OUT:
CONTINUITY NOTES:
UNCERTAINTY:
```

Use only fields that help the actual task.

## Cross-Shot Analysis

After individual shots, compare them for:

- left/right screen direction
- subject identity
- prop state
- location geometry
- lighting continuity
- action causality
- edit motivation
- rhythm escalation
- repeated framing patterns
- recurring ambience
- sound bridges / audio cuts

This step prevents locally correct shot descriptions from becoming globally incoherent.

## Confidence Discipline

Prefer evidence-backed phrasing.

High confidence:

```text
The subject crosses from screen-left to screen-right.
The metal door visibly slams shut.
```

Moderate confidence:

```text
The framing change is consistent with a forward camera move.
A synchronized metal impact is highly likely from the visible door contact.
```

Low confidence:

```text
The sparse frames do not establish whether the scale change comes from a zoom or physical camera movement.
The visuals suggest tense sound design, but the original music or effects cannot be confirmed.
```

Never convert low-confidence interpretation into fake exact technical parameters or fake audio facts.
