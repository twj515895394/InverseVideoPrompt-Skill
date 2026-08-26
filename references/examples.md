# Reverse-Engineering Examples

Use these examples to calibrate the difference between ordinary description and generation-oriented reverse engineering.

## Example 1: Single Continuous Shot

### Evidence

A six-second clip shows one person walking toward camera through a narrow rainy alley. The person stays near center frame. Store signs and walls expand outward with increasing foreground parallax. Near the end, the person stops and looks upward while the camera continues slightly closer.

### Weak Description

`A cinematic person walks through a rainy neon alley at night with dramatic lighting.`

This captures appearance but loses the temporal and camera behavior.

### Better Reverse Analysis

- One continuous shot; no visible cut.
- Subject advances toward camera at steady walking speed.
- Camera retreats ahead of subject, maintaining roughly medium framing.
- Background parallax and widening perspective support physical camera translation rather than a simple zoom.
- Rain and wet neon reflections remain continuous.
- Final beat: subject stops, tilts head upward; camera continues a short closing move into a tighter frame.

### Compiled Prompt

`Nighttime narrow urban alley in steady rain, wet pavement reflecting cyan and warm shop lights. One adult in a dark coat walks directly toward the camera. Start in a medium-wide frontal view; the camera retreats smoothly ahead of the subject at matching speed, keeping the body centered while alley walls and foreground signs show natural parallax. Rain streaks remain visible against the backlights. During the final second the subject stops, raises the chin and looks upward; the camera continues a subtle push closer, ending in a medium close-up. Keep the same alley geometry, wardrobe, lighting direction, rain intensity, and color palette throughout. No cuts.`

## Example 2: Multi-Shot Action Sequence

### Evidence

A short clip contains four edits:

1. Wide side view of a runner approaching an obstacle.
2. Close-up of one foot planting on the ground.
3. Low-angle shot of the runner jumping over the obstacle.
4. Front three-quarter medium shot of the landing with a small handheld impact shake.

### Weak Reconstruction

`A runner approaches an obstacle, jumps over it and lands while the camera follows dynamically.`

This erases the edit grammar.

### Better Reverse Structure

```text
SHOT 01 — wide side tracking setup
runner accelerates toward obstacle
hard cut
SHOT 02 — foot close-up
plant/compression beat
hard cut
SHOT 03 — low-angle jump
launch → airborne peak → clears obstacle
hard cut
SHOT 04 — landing
impact → camera micro-shake → recovery
```

### Compiled Prompt

`Global continuity: same athletic runner, same dark training outfit, same concrete outdoor course, overcast daylight, cool low-saturation grade.

SHOT 01 — Wide side view. The runner accelerates from frame left toward a waist-high obstacle while the camera tracks laterally at matching speed. End just before takeoff.

HARD CUT.

SHOT 02 — Tight close-up on the lead foot. The shoe strikes the ground, compresses for an instant, and pushes off sharply. Very brief shot.

HARD CUT.

SHOT 03 — Low-angle medium-wide near the obstacle. The runner launches upward and forward, knees folding as the body passes above the obstacle; camera tilts slightly upward to follow the airborne arc. End at the clearing peak.

HARD CUT.

SHOT 04 — Front three-quarter medium shot. The runner lands heavily, body absorbing the impact; add a short natural handheld impact shake, then stabilize as the runner regains balance. Hold briefly on the recovered stance.`

## Example 3: Procedural Montage

### Evidence

A 12-second clip rapidly shows a technician assembling a sci-fi device through many close shots: parts laid out, screws tightened, cables connected, core inserted, casing closed, power switch pressed, light sequence activates.

### Important Insight

The useful reverse-engineering target is not merely `technician builds a device`.

The generative structure is a **procedural montage**:

- repeated hand-detail shots
- state progression of the device
- short edit durations
- continuity of workspace and components
- escalating visual feedback toward activation

### Compiled Prompt Pattern

`Global continuity: same technician hands, same workbench, same partially assembled circular device, cream-and-red retro-science-fiction industrial design, cyan energy core, consistent overhead workshop lighting.

Rapid procedural montage, each shot about 0.4–0.9 seconds:
1. Overhead insert: components arranged in a semicircle around the empty chassis.
2. Macro close-up: two metal brackets slide into matching slots.
3. Tight hand shot: screwdriver turns three fast rotations, screw head seats flush.
4. Side close-up: braided cable clicks into a recessed connector.
5. Macro insert: cyan core module lowers into the center housing and locks with a quarter turn.
6. Close-up: outer casing halves close around the core.
7. Finger presses the recessed power switch.
8. Extreme close-up: one indicator lights, then a second and third in sequence.
9. Medium reveal: the completed device emits a stable cyan glow while the technician's hands pull away.

Keep component geometry and assembly state causally consistent between cuts. Fast precise editing, clean mechanical hand actions, no unexplained part changes.`

## Example 4: Sparse Frames with Uncertainty

### Evidence

Only three screenshots are available:

- Frame A: subject appears full-body at the far end of a corridor.
- Frame B: subject appears larger at mid-corridor.
- Frame C: close-up of the face.

There are no timestamps and no intermediate frames.

### Incorrect Overclaim

`The camera performs a 5-second 35 mm dolly-in at constant speed.`

### Better Handling

Observed:

- Framing progresses from full-body to close-up.
- Subject/camera distance decreases substantially.

Unknown:

- Whether the subject walks toward camera.
- Whether the camera moves toward subject.
- Whether there is an edit between frames.
- Exact duration and lens behavior.

Generation-oriented approximation:

`Begin with a full-body view at the far end of the corridor and progressively close to a face close-up. If a continuous reconstruction is desired, have the subject walk toward camera while the camera performs a restrained forward closing move; preserve corridor alignment and identity throughout. If fidelity to the original edit is more important, additional temporal evidence is required to determine whether cuts occurred.`

## Calibration Rule

A good reverse prompt should answer all of these when the evidence permits:

- What is stable?
- What changes first?
- What changes next?
- What is the subject doing?
- What is the camera doing?
- Where does the edit happen?
- What is the peak/reveal/impact?
- What state does the shot end on?

If the answer only describes a still image, the reverse engineering is incomplete.
