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

## Annotation Format
Object detection bounding boxes in YOLO format.

## Class Labels
0 person
1 helmet
2 vest

## Planned Data Split
- Train: 70%
- Validation: 20%
- Test: 10%

## Notes
Custom images will be added intentionally to improve variation in safety violations, worker distance, occlusion, and lighting conditions.