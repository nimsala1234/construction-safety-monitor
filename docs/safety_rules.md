# Safety Rules Definition

## Overview
This system monitors construction site images and determines whether workers are compliant with basic PPE requirements. The system enforces safety rules based on visible workers and visible PPE items.

The project focuses on the following PPE items:
- helmet
- high-visibility vest

A pretrained person detector is used to detect workers, and the custom-trained PPE detector identifies helmets and vests.

---

## Rule 1: Every visible worker must wear a helmet
A worker is considered compliant with this rule if a helmet is detected in the upper region of the worker’s body.

### Violation
A violation occurs when:
- a visible worker has no helmet detected
- a helmet is present in the image but is not associated with the worker

### Output label
- `NO_HELMET`

---

## Rule 2: Every visible worker must wear a high-visibility vest
A worker is considered compliant with this rule if a vest is detected in the torso region of the worker’s body.

### Violation
A violation occurs when:
- a visible worker has no vest detected
- a vest is present in the scene but is not associated with the worker

### Output label
- `NO_VEST`

---

## Rule 3: Full PPE compliance requires both helmet and vest
A worker is considered fully compliant only if:
- helmet is detected
- vest is detected

### Possible worker-level outcomes
- `COMPLIANT`
- `NO_HELMET`
- `NO_VEST`
- `NO_HELMET_NO_VEST`

---

## Rule 4: Scene-level safety decision
The scene is considered:

- `SAFE` if all detected workers are compliant
- `UNSAFE` if at least one detected worker violates a PPE rule

---

## Rule 5: Confidence-aware reporting
The system also displays confidence values for:
- person detection
- helmet detection
- vest detection
- scene-level output

This allows the system to provide not only a binary decision but also a basic measure of certainty.

---

## Examples of Violations
Examples of violations include:
- worker detected without a helmet
- worker detected without a vest
- worker detected without both helmet and vest
- multiple workers where at least one worker is non-compliant

---

## Assumptions
This system makes the following assumptions:
1. All detected persons in the construction scene are treated as workers.
2. Helmet and vest are the minimum PPE items required in the monitored environment.
3. PPE is matched to a worker using simple spatial rules:
   - helmet should appear in the upper region of the worker box
   - vest should appear in the torso region of the worker box
4. If any worker is non-compliant, the whole scene is marked unsafe.

---

## Limitations
The current system does not yet enforce:
- zone-specific PPE requirements
- temporal or video-based safety behaviour analysis
- chin strap fastening checks
- vest closure state
- gloves, boots, goggles, or fall-protection harness checks