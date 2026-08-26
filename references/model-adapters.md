# Model Adapters

Use this reference only when the user names a target video generator or asks for multiple model-specific versions.

## Adapter Principle

The reverse-engineering analysis is model-independent. Do not change the inferred shot/action structure merely to fit a generator.

Adapt only the **packaging**:

- Prompt density
- Chronological phrasing
- Shot labels
- Camera vocabulary
- Negative constraints
- Platform-native fields
- Reference-image/video instructions

Model interfaces change frequently. Do not invent current parameter names, limits, or capabilities. If the exact version matters and current documentation is available, consult it before using platform-specific syntax.

## Model-Neutral Default

Use this when the target is unspecified.

Prioritize:

1. Global continuity
2. Chronological shot/action sequence
3. Explicit camera behavior
4. Visible state changes
5. Lighting/style
6. Minimal constraints

This should be portable enough to adapt later.

## Seedance Family

Prefer a clear temporal description with strong action and camera sequencing.

Recommended packaging:

```text
Global continuity: ...

0.0–2.0s: ...
2.0–4.5s: ...
4.5–6.0s: ...

Camera: ...
Visual style: ...
Continuity constraints: ...
```

For a multi-shot reference, preserve explicit edit boundaries instead of describing all shots as a single uninterrupted move.

If the current Seedance interface provides native reference or shot controls, put information into those controls rather than redundantly forcing everything into prose.

## MiniMax / Hailuo Family

Favor concise chronological motion instructions.

Recommended emphasis:

- Subject start state
- Clear action verbs
- Direction and interaction
- Camera relation and movement
- Peak event
- End state

Avoid burying motion under long style prose.

When the exact MiniMax model/version has dedicated camera, reference, or duration controls, map the reverse-engineered fields to those controls when possible.

## Kling Family

Keep action choreography and camera movement explicit and physically coherent.

Useful packaging:

```text
Scene and subject continuity: ...
Action sequence: ...
Camera sequence: ...
Lighting/style: ...
End frame/state: ...
```

For image-to-video workflows, avoid re-describing stable visual identity that is already fully supplied by the reference image unless the detail is needed to prevent drift.

## Veo Family

Use clear cinematography language and temporal progression.

Separate when useful:

- Scene/subject
- Action
- Camera
- Lighting/style
- Audio/dialogue only if the user wants audio reconstruction and the interface supports it

Do not invent audio merely because the source video contains visual action.

## Wan Family

Use a direct generation prompt with an optional compact negative-constraint block when the workflow exposes one.

Prioritize:

- Subject and action
- Camera
- Environment
- Lighting/style
- Temporal sequence

Do not copy a long analytical report into the generation field.

## Image-to-Video Adaptation

When the user will provide a start/reference image:

Move stable visual information out of the prompt when the image already establishes it reliably.

Prompt mainly:

- Motion
- Camera
- Interaction
- Environment changes
- Effects
- End state

Still state continuity constraints that are likely to drift, such as keeping the same outfit, prop, or number of characters.

## Start/End-Frame Workflows

When both start and end frames are provided:

Do not waste the prompt describing the two images in detail. Reconstruct the **transition path**:

- What initiates movement
- Intermediate action phases
- Camera path
- Object/character interaction
- Timing and easing impression
- Effects evolution
- How the final frame is reached

If the reference video uses cuts between the start and end states, do not falsely describe a continuous physical transition unless the user's target workflow requires one.

## Multi-Model Output

When asked for several target models:

1. Perform reverse engineering once.
2. Keep one shared shot timeline and continuity specification.
3. Compile separate model adapters from the same evidence.
4. Do not independently reinterpret the source for each model unless necessary.

This prevents model-specific versions from drifting away from the reference.
