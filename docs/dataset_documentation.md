# Dataset Strategy

## Objective
Build a custom dataset for construction safety monitoring focused on worker detection and PPE compliance.

## Classes
- person
- helmet
- vest

## Data Collection Approach
This dataset will be created by combining:
1. Publicly available PPE/construction safety datasets
2. Custom-added images and video frames collected and annotated by the project author

## Why this approach was chosen
This approach satisfies the assignment requirement for a custom dataset while allowing a manageable project scope and sufficient data diversity.

## Target Dataset Size
- Public base: 700 images
- Custom additions: 300 images
- Final total: 1000 images

## Required Diversity
The dataset will include:
- indoor and outdoor construction settings
- daylight, shadow, overcast, and artificial lighting
- safe and unsafe scenes
- single-worker and multi-worker scenes
- close, medium, and far worker visibility

## Annotation Approach

### Annotation Tool
The dataset is annotated using Roboflow Annotate with bounding boxes and exported in YOLO format.

### Object Classes
- person
- helmet
- vest

### Labelling Policy
- `person`: every clearly visible worker/person in the construction scene
- `helmet`: every clearly visible construction helmet
- `vest`: every clearly visible high-visibility safety vest

### Annotation Rules
- Only visible objects are annotated; hidden or assumed objects are not labelled.
- Bounding boxes are drawn tightly around each object.
- Cropped or partially visible objects are labelled only for the visible portion.
- Very small, highly blurred, or highly uncertain objects are skipped to preserve annotation quality.
- In crowded scenes, each visible worker and PPE item is labelled separately.

### Edge Cases
- Occluded workers are labelled only if enough of the body is visible.
- PPE is labelled only when clearly visible.
- Far-away workers may be labelled as `person` without PPE labels if PPE cannot be reliably identified.

## Planned Data Split
- Train: 70%
- Validation: 20%
- Test: 10%

## Notes
Custom images will be added intentionally to improve variation in safety violations, worker distance, occlusion, and lighting conditions.