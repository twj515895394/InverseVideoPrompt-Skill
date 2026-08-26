# Calibration Examples

These examples teach the skill how to reason about different video structures. They are not rigid templates. Preserve the reasoning pattern and adapt to the evidence.

## Example 1 — Single Continuous Shot

### Evidence

A person stands at the far end of a corridor, begins running toward camera, the camera retreats while preserving a medium framing, then arcs slightly as the person reaches and opens a door. Bright light spills through the doorway.

### Good analysis

- One continuous shot, not three shots.
- Subject motion: person runs forward toward camera.
- Camera motion: backward tracking/dolly while maintaining framing; slight arc near the door.
- Action phases: standing/anticipation → acceleration → approach → door interaction → stop/reveal.
- Lighting continuity: darker corridor, bright source beyond the door.
- Narrative rhythm: acceleration followed by a short reveal hold.

### Good compiled prompt

```text
A continuous cinematic shot in a dim corridor. Start in a medium-long view with the character positioned at the far end. The character suddenly runs straight toward camera; the camera smoothly tracks backward at matching speed, maintaining a stable medium framing while corridor walls create strong forward motion and parallax. As the character reaches the doorway, the camera makes a subtle arc toward screen-right while the character pushes the door open. Bright warm light spills into the darker corridor, briefly blooming around the character. End with the character stopped in the doorway in a medium close framing and hold the reveal for a moment. Preserve the same character, clothing, corridor geometry, lighting logic, and cinematic color treatment throughout.
```

## Example 2 — Multi-Shot Action Sequence

### Evidence

A fighter looks up. Hard cut to a low-angle shot as an opponent leaps from a platform. Hard cut to a side view of both characters colliding. Hard cut to a close-up of dust and feet sliding backward.

### Good analysis

Do not rewrite this as one giant continuous orbiting camera move.

```text
SHOT 01 — reaction/setup
SHOT 02 — leap/attack
SHOT 03 — impact
SHOT 04 — recovery/aftermath
```

Key continuity:

- same two fighters
- same location
- same wardrobe
- spatial left/right relationship remains understandable
- impact direction continues into the final sliding shot

### Good compiled prompt

```text
SHOT 01 — Medium close-up. Fighter A looks sharply upward, shoulders tensing, holding for a brief anticipation beat.

HARD CUT.

SHOT 02 — Low-angle wide shot. Fighter B launches from the elevated platform toward Fighter A, body driving diagonally downward through frame. The camera remains low and slightly tracks the descent to emphasize height and speed.

HARD CUT ON ACTION.

SHOT 03 — Side medium-wide shot. Fighter B collides with Fighter A at the center of frame. Emphasize the exact impact beat with rapid body compression, clothing and dust reaction, then immediate lateral momentum.

HARD CUT.

SHOT 04 — Ground-level close-up. Both fighters' feet skid backward across the dusty floor, kicking up a narrow trail of debris. Hold briefly as the motion settles.

Maintain identical character identities, clothing, environment, direction of force, lighting, and grade across all shots.
```

## Example 3 — Procedural Montage

### Evidence

A rapid montage shows a scientist assembling a machine: components spread on a floor, hands tightening screws, cable insertion, a glowing core being seated, outer casing closing, then indicator lights activating.

### Interpretation

The important structure is not conventional dialogue-driven narrative. It is a **process montage** organized by meaningful state changes.

Suggested decomposition:

```text
state 1: loose components
state 2: mechanical frame assembled
state 3: wiring connected
state 4: core installed
state 5: casing closed
state 6: powered state / activation
```

Sampling should favor each irreversible state change plus important hand-action peaks, not arbitrary equal intervals.

### Prompt logic

```text
Rapid procedural montage of a scientist assembling a compact experimental device. Begin with organized components spread across the laboratory floor. Use fast macro and close-up cuts of hands aligning the frame, tightening screws, snapping mechanical joints into place, inserting cables, seating the glowing core, and closing the outer housing. Preserve exact component continuity so each cut shows believable assembly progress rather than random part changes. As the final casing locks, cut to the activation sequence: indicator lights illuminate in order, internal energy begins to glow, and the scientist's hands pull away. Use purposeful match-on-action cuts, tactile mechanical detail, increasing visual energy, and a clear progression from disassembled parts to a completed powered machine.
```

Do not limit this pattern to literal assembly. The same grammar can apply to cooking, repair, crafting, laboratory procedures, transformation processes, preparation rituals, makeup/costume changes, vehicle setup, device operation, or any video whose meaning comes from ordered state transitions.

## Example 4 — Sparse Frames Only

### Evidence

Three screenshots show:

1. person standing beside a car
2. person closer to the driver's door
3. person seated inside

### Weak reconstruction

```text
The person walks exactly three steps, opens the door with the left hand, bends down and enters the car while the camera dollies forward.
```

This invents unsupported details.

### Better reconstruction

```text
The sequence appears to show the person moving from beside the car into the driver's seat. The intermediate walking pattern, hand used to open the door, and exact camera motion are not visible in the supplied frames. Preserve a simple progression: standing beside the vehicle → approaching/opening the driver's door → entering and settling into the seat. Keep the camera behavior conservative unless additional frames show clear movement.
```

## Example 5 — Visual-Only Clip With Sound Inference and Recommendation

### Evidence

A muted five-second clip shows a woman running through a rainy underground parking garage. At about 2.8 seconds she forcefully pushes open a heavy metal fire door. The camera quickly follows behind her and cuts to a close-up just after the door slams shut. No usable source audio is available.

### Bad sound reconstruction

```text
The original video contains loud dramatic orchestral music, thunder, a heartbeat, screaming, heavy breathing, metallic footsteps, a huge bass drop and a cinematic whoosh.
```

This incorrectly presents creative guesses as source facts and overloads the scene.

### Better sound reasoning

```text
Observed:
- No reliable source audio is available.

High-probability inferred sound:
- Repeated wet footsteps synchronized with running.
- Rain/water ambience consistent with the visibly wet garage environment.
- Clothing movement and light breathing may accompany the sprint, but intensity is uncertain.
- A heavy metal push/contact sound at the fire door.
- A distinct metal door slam immediately before/at the close-up cut.
- Short garage reverb tail after the slam.

Recommended sound design:
- Keep a low, diffuse underground garage ambience underneath the whole shot.
- Add restrained low-frequency tension rather than full orchestral music.
- Slightly reduce ambience immediately before the door slam so the impact reads more strongly.
- Add one short low-end accent under the slam; do not add an exaggerated whoosh to every camera movement.
```

### Timeline example

```text
0.0-2.6s — wet running footsteps + garage/rain ambience; subtle clothing movement; optional restrained low tension drone
2.6-2.9s — footsteps accelerate; brief dynamic dip as the hand reaches the door
2.9s — heavy metal door push/contact
3.1s — door slam + short low-frequency accent + garage reverb tail
3.1-5.0s — ambience returns at lower intensity; footsteps stop or move off-screen depending on visible motion
```

### Compiled audiovisual prompt pattern

```text
Follow the woman from behind as she runs rapidly through the wet underground parking garage, keeping the handheld/tracking camera close enough to feel urgent while preserving readable spatial depth. Her footsteps splash lightly on the damp concrete. The garage carries a diffuse rain-and-ventilation ambience with restrained low-frequency tension underneath. As she reaches the heavy metal fire door, briefly thin the ambience, synchronize a solid metal contact sound to the push, then emphasize the door slam with a short dry impact, subtle sub-bass accent, and a compact concrete-garage reverb tail. Cut to the close-up immediately after the slam and let the ambient bed return. Do not add dialogue or exaggerated repeated whooshes.
```

The key lesson is that **sound inference follows visual evidence, while sound recommendation is a separate creative layer**.
