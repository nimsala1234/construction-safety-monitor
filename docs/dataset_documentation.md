# Dataset Documentation

## Data Collection
This project focuses on construction safety monitoring through PPE detection. The dataset used for this work was created by extending an existing public PPE dataset and organizing it for custom training.

The starting dataset was a public Kaggle dataset containing annotated construction PPE images. The original dataset included labels for:
- Safety Helmet
- Reflective Jacket

These labels were mapped into the project’s final PPE classes:
- helmet
- vest

The dataset was imported into Roboflow, cleaned, and exported for training in Google Colab. The project primarily trained a custom detector for helmet and vest detection. Worker/person detection was handled separately at inference time using a pretrained YOLO person detector.

## Dataset Source
Base dataset source:
- Kaggle PPE dataset containing Safety Helmet and Reflective Jacket annotations

## Custom Additions / Changes
The original dataset labels were adapted to match the project class names:
- Safety-Helmet → helmet
- Reflective-Jacket → vest

The dataset was then restructured into train, validation, and test splits for training in Colab.

## Dataset Size
The final dataset contained:

- Train images: Images = 694
                Labels = 694
- Validation images: Images = 195
                     Labels = 195
- Test images: Images = 100
               Labels = 100
- Total images: Images = 989
                Labels = 989
## Class Distribution
The project used 2 PPE classes:

- helmet
- vest

Validation class distribution:
- Helmet instances: 373
- Vest instances: 317

If you want, you can also add the train/test class counts if available.

## Annotation Approach
The dataset uses object detection bounding box annotations in YOLO format.

Annotation approach:
- Each visible helmet was annotated with a bounding box and labelled as `helmet`
- Each visible safety vest was annotated with a bounding box and labelled as `vest`
- Bounding boxes were kept tight around the visible PPE item
- Only visible objects were labelled; hidden or unclear objects were not guessed

The project did not rely on custom person annotations for training. Instead, worker detection was performed using a pretrained person detector during inference, while the custom-trained model focused on PPE detection.

## Why This Dataset Strategy Was Chosen
This dataset strategy was chosen to make the project feasible within the available time while still supporting the core task:
- PPE detection using a custom-trained model
- worker detection using a pretrained detector
- rule-based compliance checking
- safe/unsafe scene classification

## Limitations of the Dataset
Some limitations of the dataset include:
- no custom person class training in the final detector
- variation in lighting and object size across images
- some difficult cases such as occlusion and small distant workers
- limited ability to capture all real-world construction scenarios