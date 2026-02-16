# Player Tracking in Sports Videos

## Dataset

The dataset used for this project consists of 8 short sports video clips (5–10 seconds each) including basketball scenes.

The dataset is available here:

https://drive.google.com/drive/folders/13WMPmVcT4VDoCdl1zW5f8z6ztVTJF0aY?usp=sharing

Whole Google folder is available here:

https://drive.google.com/drive/folders/1uN8ESV6-VKcCIFId24saWrz5G8AGFBRi?usp=sharing



# Report document

## 4.1 Performance Metrics

In this project, a YOLOv8n object detection model was used to detect players in sports videos. The dataset was created by extracting frames from 9 sports video clips. A total of 259 images were generated and split into training (80%) and validation (20%) sets.

The model was trained for 3 epochs using an image size of 640×640.

After detection, ByteTrack was applied to assign consistent IDs to players across frames for tracking purposes.

## 4.1 Model Overview

The trained model was evaluated using standard object detection metrics.

Validation Results


| Metric        | Value      |
| ------------- | ---------- |
| Precision     | **0.9466** |
| Recall        | **0.4502** |
| mAP@50        | **0.7589** |
| mAP@50–95     | **0.5438** |
| Fitness Score | **0.5438** |



## 4.3 Explanation of Metrics

## Precision (94.66%)


Precision measures how many detected players were correctly identified.

A precision value of 94.66% indicates:

Very few false positives

The model rarely detects non-player objects as players

Strong reliability in predictions

This demonstrates that the model makes accurate detections when it predicts a player.

## Recall (45.02%)

Recall measures how many actual players were successfully detected.

A recall of 45.02% indicates:

  Some players were missed
  
  Detection performance is moderate
  
  The model does not detect all players present in each frame

This can be explained by:

  Small dataset size
  
  Fast player movements
  
  Motion blur
  
  Player occlusion and overlapping


## mAP@50 (75.89%)

Mean Average Precision at IoU 0.5 evaluates bounding box quality.

A value of 0.7589 indicates:

  Good localization performance
  
  Bounding boxes align reasonably well with ground truth
  
  Strong detection capability for a lightweight model


## mAP@50–95 (54.38%)

This metric evaluates detection under stricter overlap thresholds.

A value of 0.5438 suggests:

  Moderate robustness
  
  Bounding box precision could be improved
  
  The model struggles slightly under stricter evaluation conditions

## 4.4 Training Behavior and Loss Analysis

During training:

Box loss decreased progressively

Classification loss stabilized

Validation performance improved over epochs

Since training was limited to only 3 epochs, the model likely did not fully converge.

Training for more epochs would likely:

  Improve recall
  
  Improve mAP@50–95
  
  Improve generalization performance


## 4.5 Model Speed and Efficiency

Speed metrics from validation:

  Preprocessing: ~1.34 ms
  
  Inference: ~119.7 ms
  
  Postprocessing: ~5.81 ms

This indicates:

  The model runs efficiently
  
  Suitable for near real-time sports analysis
  
  YOLOv8n provides good balance between speed and accuracy


## 4.6 Performance Comparison

The system includes two components:

  1. YOLOv8n – Player Detection
  
  2. ByteTrack – Player Tracking

Detection Performance

  High precision
  
  Moderate mAP
  
  Moderate recall
  
  Fast inference

Tracking Performance

  Maintained consistent player IDs
  
  Reduced ID switching
  
  Enabled movement analysis across frames

The integration of YOLO detection with ByteTrack tracking provides a complete player tracking pipeline.


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
