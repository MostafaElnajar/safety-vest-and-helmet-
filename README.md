#Save People from Drowning
This project is a real-time drowning detection system leveraging computer vision, pose estimation, and deep learning techniques to monitor and identify potential drowning incidents in video feeds. The system raises an alert if a person shows distress signs, such as raising hands for help, ensuring timely intervention to save lives.

Objective
To build a robust, automated drowning detection system using video analysis and AI models to enhance water safety and reduce response time during emergencies.

How It Works
Object Detection

The system uses the YOLOv5 pre-trained model to detect and track individuals in the video feed.
Bounding boxes are drawn around detected objects, and only "person" detections with a confidence score > 0.25 are processed further.
Pose Estimation

Mediapipe's Pose module extracts key points (shoulder, elbow, and wrist) from detected persons.
The system calculates angles at the elbows to identify a "raised hand" gesture, which can indicate a distress signal.
Behavior Analysis

Distress behavior is identified if a person's hand remains raised above their shoulder for more than a defined number of frames (7 frames by default).
Alert Mechanism

When a potential drowning incident is detected, an audible alarm is triggered using the miniaudio library to alert nearby rescuers.
Technical Details
Tools and Libraries
YOLOv5: Pre-trained model for object detection, loaded via PyTorch.
Mediapipe: For pose estimation and keypoint extraction.
OpenCV: For video processing and frame manipulation.
miniaudio: For playing alert sound when a distress signal is detected.
NumPy: For mathematical operations like angle calculation.
Mutagen: To get metadata of audio files for precise alert timing.
Workflow
Object Detection:

YOLOv5 detects individuals in each frame of the video feed and filters out non-human objects.
Pose Detection and Angle Calculation:

Mediapipe extracts landmarks (shoulder, elbow, and wrist) for each detected person.
Angles are calculated using the arctangent formula to analyze arm movements.
Drowning Signal Identification:

The system checks if the wrist is above the elbow and shoulder, and if the calculated angle exceeds 150 degrees.
If this posture persists across consecutive frames, it flags the behavior as a distress signal.
Alert Sound:

An MP3 alarm sound is played via miniaudio for a duration equal to the audio file's length to ensure proper alerting.
Key Functions
calc_angle: Calculates the angle between the shoulder, elbow, and wrist to analyze arm posture.
Tracker Class: Tracks multiple individuals across frames to identify consistent distress behaviors
