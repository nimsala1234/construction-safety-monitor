# Construction Safety Monitor

## Project Overview
This project builds a construction safety monitoring system using computer vision. The system detects workers, identifies personal protective equipment (PPE), and determines whether a scene is safe or unsafe.

The final system combines:
- a pretrained person detector for worker detection
- a custom-trained YOLO PPE detector for helmet and vest detection
- a rule-based compliance module for safety decision making

---

## Features
- Worker detection
- Helmet detection
- Safety vest detection
- Worker-level compliance checking
- Scene-level SAFE / UNSAFE classification
- Confidence-aware output
- Human-readable violation labels

---

## Classes
Custom-trained PPE model classes:
- helmet
- vest

Worker detection:
- person (detected using pretrained YOLO model)

---

## Model and Architecture Choice
YOLO object detection was chosen because the task requires locating PPE items with bounding boxes rather than only classifying the whole image.

A lightweight pretrained YOLO model was used as the PPE detector because:
- it supports transfer learning
- it trains efficiently in Google Colab
- it provides a good balance between speed and performance

The final system uses:
1. Pretrained YOLO model for person detection
2. Custom-trained YOLO model for helmet and vest detection
3. Rule-based matching logic to determine compliance

---

## Training Setup
The PPE detector was trained in Google Colab using transfer learning from pretrained YOLO weights.

Training setup:
- Framework: Ultralytics YOLO
- Task: Object detection
- Classes: helmet, vest
- Base weights: YOLOv8 pretrained weights
- Image size: 640
- Epochs: 30
- Batch size: 16
- Environment: Google Colab

---

## Validation Results
Validation results for the PPE detector:

- Precision: 0.8385
- Recall: 0.7414
- mAP@50: 0.8358
- mAP@50-95: 0.5283

Per-class mAP@50-95:
- Helmet: 0.5606
- Vest: 0.4961

These results show that the model performs reasonably well at detecting PPE, with stronger precision than recall.

---

## How the Final System Works
1. Detect persons using a pretrained YOLO model
2. Detect helmets and vests using the custom-trained PPE detector
3. Match PPE detections to each detected worker using spatial rules
4. Classify each worker as:
   - COMPLIANT
   - NO_HELMET
   - NO_VEST
   - NO_HELMET_NO_VEST
5. Classify the full scene as:
   - SAFE
   - UNSAFE

---

## Prerequisites
To run the project in Colab or locally, install:

```bash
pip install ultralytics opencv-python

```

## Key Design Decisions

Important design choices made in this project:

object detection was used instead of image classification
PPE detection was custom-trained on the dataset
person detection was handled using a pretrained detector to avoid heavy manual annotation
rule-based logic was used for compliance checking
confidence scoring was added to improve interpretability

---

## Honest Evaluation

## Where the model performs well

- clear construction scenes with visible helmets and vests
- medium-distance workers with low occlusion
- scenes where PPE is visually distinct from the background

## Where the model struggles
- small or distant workers
- partial occlusion
- difficult lighting
- crowded scenes
- imperfect PPE-to-worker matching when workers overlap

---

## Known Limitations

- person detection is not custom-trained in the final version
- no temporal/video-based analysis
- no zone-based PPE rules
- no additional PPE classes such as gloves, boots, goggles, or harness
- matching logic is simple and may fail in complex scenes

--- 

## Future Improvements

Possible future improvements include:

- training a full custom person + PPE detector
- zone-based safety rules
- temporal video analysis
- automatic violation report generation
- more PPE categories and richer safety logic