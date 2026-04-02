# Safety Rules Definition

## Project Scope
This project monitors construction site images and determines whether a scene is safe or unsafe based on visible worker compliance with personal protective equipment (PPE) rules.

The system focuses on three main visual elements:
- Person / worker detection
- Helmet detection
- High-visibility vest detection

The final goal is to determine:
- whether each detected worker is compliant or non-compliant
- whether the overall scene is safe or unsafe

---

## Rule 1: Helmet Required
Every visible worker in the monitored construction zone must wear a safety helmet.

### Counts as compliant
- A worker is visible and a helmet is clearly detected on the head region.

### Counts as a violation
- A visible worker has no helmet detected.
- A helmet is present in the scene but not being worn by the worker.
- The helmet is carried in hand or placed nearby instead of worn.

### System decision
- If a worker is detected without a helmet, flag: `NO_HELMET`

---

## Rule 2: High-Visibility Vest Required
Every visible worker in the monitored construction zone must wear a high-visibility safety vest.

### Counts as compliant
- A worker is visible and a safety vest is clearly detected on the torso region.

### Counts as a violation
- A visible worker has no vest detected.
- A vest is nearby but not being worn.
- Clothing that is not a proper high-visibility vest does not count as compliant.

### System decision
- If a worker is detected without a vest, flag: `NO_VEST`

---

## Rule 3: Full PPE Compliance Required
A worker is considered compliant only if both required PPE items are present:
- helmet
- high-visibility vest

### Counts as compliant
- Helmet detected on head region
- Vest detected on torso region

### Counts as a violation
- Missing helmet only
- Missing vest only
- Missing both helmet and vest

### System decision
Possible worker-level outputs:
- `COMPLIANT`
- `NO_HELMET`
- `NO_VEST`
- `NO_HELMET_NO_VEST`

---

## Rule 4: Scene Safety Decision
The entire scene is considered safe only if all clearly visible workers are compliant.

### Safe scene
- All detected workers wear both helmet and vest.

### Unsafe scene
- At least one detected worker violates any PPE rule.

### System decision
- `SAFE` if all workers are compliant
- `UNSAFE` if one or more violations are detected

---

## Rule 5: Visibility Condition
Rules are enforced only for workers who are sufficiently visible in the frame.

### Enforced when
- Most of the worker’s body is visible
- Head and torso regions are visible enough for PPE checking

### Not enforced strictly when
- Worker is heavily occluded
- Worker is too far away for reliable PPE detection
- Image quality is too poor to make a confident judgment

### System handling
- Such cases may be marked as uncertain rather than immediately treated as violations.

---

## Rule 6: PPE Must Be Worn Correctly
Safety equipment must be worn in the expected body region.

### Counts as compliant
- Helmet appears on the head region
- Vest appears on the upper body / torso region

### Counts as a violation
- Helmet detected away from head
- Vest detected away from torso
- PPE object visible but not associated with a worker

### Reason
This avoids false compliance when PPE is present in the image but not actually worn.

---

## Worker-Level Violation Categories
The system will use these worker-level categories:
- `COMPLIANT`
- `NO_HELMET`
- `NO_VEST`
- `NO_HELMET_NO_VEST`
- `UNCERTAIN` (optional, for low-visibility or low-confidence cases)

---

## Scene-Level Categories
The system will use these scene-level labels:
- `SAFE`
- `UNSAFE`
- `UNCERTAIN` (optional, if image quality is too poor)

---

## Assumptions
This project makes the following assumptions:
1. All detected persons in the monitored construction area are treated as workers.
2. Helmet and vest are the minimum required PPE for the current project scope.
3. Compliance is judged from a single image or frame.
4. If a worker is visible but required PPE is missing, the worker is considered non-compliant.
5. If PPE is present in the image but not worn correctly, it does not count.

---

## Limitations
These rules are intentionally limited to visual checks that can be reliably implemented in a first-version computer vision system.

The current system does not fully enforce:
- chin strap fastening
- open vs closed vest state
- gloves
- boots
- goggles
- fall protection harness
- zone-specific PPE requirements

These may be added in future versions.

---

## Why These Rules Were Chosen
These rules were selected because:
- they match the core assignment requirements
- they are visually detectable using object detection
- they allow clear worker-level and scene-level safety decisions
- they are realistic for a first implementation using a custom dataset

---

## Example Decision Logic
- Worker detected + helmet yes + vest yes = `COMPLIANT`
- Worker detected + helmet no + vest yes = `NO_HELMET`
- Worker detected + helmet yes + vest no = `NO_VEST`
- Worker detected + helmet no + vest no = `NO_HELMET_NO_VEST`

Scene decision:
- all workers compliant = `SAFE`
- any worker non-compliant = `UNSAFE`