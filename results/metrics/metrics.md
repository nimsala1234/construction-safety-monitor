# Evaluation Metrics
## Validation Setup

The PPE detector was evaluated on the validation split of the custom dataset. The validation set contained 195 images and 690 total labeled PPE instances, consisting of 373 helmet instances and 317 vest instances.

---

## Overall Detection Results

The trained YOLO PPE detector achieved the following validation results:

Precision: 0.8385
Recall: 0.7414
mAP@50: 0.8358
mAP@50-95: 0.5283

These values show that the model performs well at detecting PPE items, especially at IoU 0.50, while performance decreases under stricter localization thresholds.

---

## Per-Class Results

Per-class mAP@50-95 values were:

Helmet: 0.5606
Vest: 0.4961

Class-wise precision and recall were:

Helmet: Precision 0.921, Recall 0.723
Vest: Precision 0.756, Recall 0.760

---

## Interpretation

The model shows strong precision, meaning many predicted detections are correct, but recall is lower, which means some PPE instances are still missed. Helmet detection performed slightly better than vest detection overall. This may be due to clearer helmet shapes and more visually consistent appearance compared to vests, which can vary more with pose, lighting, and partial occlusion.

---

## Inference Speed

Validation speed per image was approximately:

Preprocess: 1.6 ms
Inference: 178.6 ms
Postprocess: 12.0 ms

---

## Failure Cases and Limitations

The model may still struggle in these cases:

small or distant workers
partially occluded helmets or vests
cluttered backgrounds
difficult lighting conditions
incorrect PPE-to-worker matching in crowded scenes

These limitations are consistent with the assignment’s expectation to report where the model performs well and where it struggles.

---
 
## Final System Note

In the final system, helmet and vest detection are handled by the custom-trained YOLO PPE detector, while worker detection is handled by a pretrained person detector. A rule-based compliance module then combines both outputs to classify workers and scenes as SAFE or UNSAFE, matching the core task requirements of worker detection, PPE recognition, compliance checking, and violation flagging along with confidence.