# Safety Vest and Helmet Detection

This project is an AI-based system for detecting workers wearing safety helmets and vests in a video feed. It identifies workers without proper safety gear, labels them appropriately, and saves images of violations for further review. The tool aims to ensure compliance with workplace safety standards in construction, manufacturing, and other industries.

### Objective

To develop a real-time monitoring system that ensures worker safety by detecting safety helmets and vests using computer vision and a custom-trained YOLOv5 model.

### How It Works
1.Object Detection

The system uses a custom YOLOv5 model trained to detect helmets, vests, and workers in video footage.
Bounding boxes are drawn around detected objects, and labels are applied for identification (Helmet, Vest, Worker).

2.Safety Compliance Check

Each worker's bounding box is compared against detected helmets and vests.
If a worker lacks a helmet, a vest, or both, they are flagged as non-compliant.

3.Violation Handling

Images of non-compliant workers are saved with details in the output/ directory for record-keeping.
The type of violation (e.g., "No Helmet," "No Vest," "No Helmet and Vest") is displayed on the video frame.

4.Output Generation

A processed video with all detections, labels, and violations is saved as output.mp4.

### Technical Details
### Workflow
1. Model Loading

The YOLOv5 model (best final.pt) is loaded using PyTorch’s hub functionality.
The custom model is trained specifically to detect three classes: Helmet, Vest, and Worker.

2. Video Processing

Input video frames are resized for consistent processing.
The model outputs predictions for each frame, including bounding boxes, confidence scores, and class IDs.

3. Safety Violation Detection

For each detected worker:
Overlapping checks determine if a helmet or vest is within the worker's bounding box.
If no overlap is detected, the worker is flagged as non-compliant.
Images of non-compliant workers are cropped and saved with descriptive filenames.

4. Output Video and Visualization

Bounding boxes and labels are added to frames for helmets, vests, and workers.
Violations are highlighted in red with appropriate text annotations.
The processed video is saved in MP4 format with all detections and annotations.

### Tools and Technologies
YOLOv5: For custom object detection (trained model).
OpenCV: For video processing, frame handling, and visualization.
PyTorch: For model loading and inference.
NumPy: For numerical operations and bounding box calculations.
Custom Dataset: Trained on images of workers, helmets, and vests.
