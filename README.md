# Player Tracking in Sports Videos

## Dataset

The dataset used for this project consists of 8 short sports video clips (5–10 seconds each) including basketball scenes.

The dataset is available here:

https://drive.google.com/drive/folders/13WMPmVcT4VDoCdl1zW5f8z6ztVTJF0aY?usp=sharing

Whole Google folder is available here:

https://drive.google.com/drive/folders/1uN8ESV6-VKcCIFId24saWrz5G8AGFBRi?usp=sharing



# Report document

## 4.1 Performance Metrics

In this project, a YOLOv8n object detection model was used to detect players in sports videos. The model was fine-tuned using a custom dataset created by extracting frames from 9 sports video clips. A total of 259 images were generated and split into training (80%) and validation (20%) sets.

The model was trained for 3 epochs using an image size of 640×640.

After detection, ByteTrack was used to assign consistent IDs to detected players for tracking across frames.

## 4.1 Model Overview

The trained model was evaluated using standard object detection metrics.

Validation Results


| Metric        | Value      |
| ------------- | ---------- |
| Precision     | **0.9626** |
| Recall        | **0.3919** |
| mAP@50        | **0.7474** |
| mAP@50–95     | **0.5582** |
| Fitness Score | **0.5582** |


## 4.3 Explanation of Metrics

## Precision (96.26%)

Precision measures how many detected players were actually correct.

A high precision value indicates:

Very few false positives

The model rarely detects non-player objects as players

Strong classification reliability

This is a strong result and shows the model is confident in its predictions.

## Recall (39.19%)

Recall measures how many actual players were detected by the model.

The recall value is relatively low, which indicates:

Some players were missed

The model does not detect all players present in frames

This is expected because:

The dataset is small

Sports scenes include motion blur and occlusion

Players often overlap or move fast


## mAP@50 (74.74%)

Mean Average Precision at IoU 0.5 shows overall detection performance.

A value of 0.74 indicates:

Good localization performance

Bounding boxes are reasonably accurate


## mAP@50–95 (55.82%)

This metric evaluates detection performance at stricter IoU thresholds.

Since this is above 0.55, it indicates:

Acceptable performance for a lightweight model

Bounding box alignment could still be improved

## 4.4 Training Behavior and Loss Analysis

During training:

Box loss decreased gradually

Classification loss stabilized

Validation performance improved over epochs

Since training was limited to only 3 epochs, the model likely did not fully converge. Increasing epochs may further improve recall and mAP scores.


## 4.5 Model Speed and Efficiency

The model speed measurements were:

Preprocessing: ~1.36 ms

Inference: ~118.7 ms

Postprocessing: ~5.49 ms

This indicates:

The model can process frames relatively fast

It is suitable for near real-time sports analysis

Lightweight YOLOv8n is efficient for practical deployment


## 4.6 Performance Comparison

The system consists of two main components:

YOLOv8n – Player Detection

ByteTrack – Player Tracking

Detection Performance

High precision

Moderate mAP

Low recall

Tracking Performance

Maintained consistent player IDs across frames

Reduced ID switching using ByteTrack

Improved player movement analysis capability

The combination of YOLO detection and ByteTrack tracking provides a complete player tracking pipeline.


## 4.7 Discussion on Model Performance

The model performed well in terms of precision but struggled with recall.

Strengths

High precision (very accurate detections)

Good bounding box localization

Fast inference speed

Effective ID tracking with ByteTrack

Suitable for sports analytics tasks

Weaknesses

Low recall (missed players)

Small dataset size (259 images only)

Limited training epochs (03)

Only one class (person)

Complex sports scenes affect detection

## 4.8 Limitations

Several limitations were observed:

Small Dataset
The dataset size is insufficient for robust generalization.

Limited Training Duration
03 epochs may not be enough for optimal performance.

Occlusion and Overlapping Players
Players frequently overlap, causing missed detections.

Motion Blur
Fast movement in sports videos reduces detection clarity.

Single-Class Detection
The model detects only "person" and does not distinguish teams

## 4.9 Possible Improvements

To improve system performance, the following enhancements are recommended:

Increase Dataset Size
Collect and annotate at least 1000+ images.

Increase Training Epochs
Train for 50–100 epochs for better convergence.

Use a Larger Model
YOLOv8m or YOLOv8l may improve recall.

Advanced Data Augmentation
Include motion blur simulation and brightness variation.

Hyperparameter Tuning
Adjust confidence and IoU thresholds.

Multi-Class Detection
Separate players by team jersey color.

Use Pose Estimation
Integrate OpenPose-style keypoint detection for richer analysis.


## 4.10 Conclusion of Performance Evaluation

The proposed player tracking system successfully detects and tracks players in sports videos using YOLOv8n and ByteTrack.

The model achieved:

High precision (96%)

Moderate localization accuracy (mAP 74%)

Fast inference suitable for near real-time applications

However, recall remains low due to dataset limitations and complex sports environments.

With additional training data and longer training duration, the system performance can be significantly improved.
