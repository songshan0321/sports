<div align="center">

  <h1>Football Analytics</h1>

</div>

This repository is a computer vision project for football analytics, designed to provide detailed insights into the game through advanced video analysis. It is a fork of [roboflow/sports](https://github.com/roboflow/sports), which offers foundational functionality and examples for training models.

**Declaration**: All models in this repository have been retrained to achieve improved accuracy compared to the original repository.

---

## Features and Workflow

This project follows a step-by-step implementation based on the tutorial: [Football Analytics with YOLOv8 and ByteTrack](https://youtu.be/aBVGKoNZQUw?si=M7-6FJU2p5CUAJn_). Below is an overview of the workflow and features:

1. **Object Detection**:
   - **YOLOv8** is used to detect four classes: `player`, `goalkeeper`, `referee`, and `football`.

2. **Player and Object Tracking**:
   - **ByteTrack** tracks `players`, `goalkeepers`, and `referees`.

3. **Field Keypoint Detection**:
   - **YOLOv8-pose** detects the keypoints of the football field.

4. **Team Classification**:
   - Uses **K-means clustering** with SigLip output as the feature for classifying players into teams based on their jersey colors.

5. **Bird-Eye View (BEV) Transformation**:
   - Perspective projection transforms camera frames into a top-down BEV for better spatial analysis.

---

## Challenges and Improvements

### 1. Unstable Keypoint Detection
- **Issue**: The original training parameters for keypoint detection produced inconsistent results.
- **Solution**: Enhanced data augmentation techniques, such as:
  - Random perspective transformations.
  - Random rotations.
  - Increased random cropping.
  - Additional training epochs.
- **Result**: Improved model stability, which is critical for accurate perspective transformation to BEV.

### 2. Occlusion in Player Tracking
- **Issue**: ByteTrack often struggled with occlusions, causing ID switches.
- **Solution**: Replaced ByteTrack with **DeepSORT** and used SigLip as the feature extractor.
- **Result**: The feature-based tracker performed significantly better during player occlusions, as players from different teams usually have distinct jersey colors.

### 3. Improving Feature Extraction
- **Issue**: Initially, the feature extractor cropped the entire bounding box (bbox) around a player, leading to noisy background information.
- **Solution**: Shrinking the bbox during cropping reduced background noise.
- **Result**: Improved team classification and better tracking performance.

### 4. Ball Trajectory in BEV
- **Issue**: Using the ball's current position in the camera frame for perspective transformation often caused inaccuracies, especially when the ball was in the air.
- **Solution**: Refined the ball trajectory using cues from changes in direction and velocity.
- **Result**: Accurate BEV projection, even when the ball was airborne, as demonstrated in the video.

---

## Acknowledgments

This project is built on the foundational work of the roboflow/sports repository and leverages the techniques explained in the [YouTube tutorial](https://youtu.be/aBVGKoNZQUw?si=M7-6FJU2p5CUAJn_). Special thanks to the creators for their contributions to sports analytics.

Feel free to explore, contribute, or use this project to enhance football analytics workflows!

## 💻 install

We don't have a Python package yet. Install from source in a
[**Python>=3.8**](https://www.python.org/) environment.

```bash
pip install git+https://github.com/roboflow/sports.git
```

## ⚽ datasets

| use case                        | dataset                                                                                                                                                          |
|:--------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| soccer player detection         | [![Download Dataset](https://app.roboflow.com/images/download-dataset-badge.svg)](https://universe.roboflow.com/roboflow-jvuqo/football-players-detection-3zvbc) |
| soccer ball detection           | [![Download Dataset](https://app.roboflow.com/images/download-dataset-badge.svg)](https://universe.roboflow.com/roboflow-jvuqo/football-ball-detection-rejhg)    |
| soccer pitch keypoint detection | [![Download Dataset](https://app.roboflow.com/images/download-dataset-badge.svg)](https://universe.roboflow.com/roboflow-jvuqo/football-field-detection-f07vi)   |

Visit [Roboflow Universe](https://universe.roboflow.com/) and explore other sport-related datasets.

## 🔥 demos

https://github.com/roboflow/sports/assets/26109316/7ad414dd-cc4e-476d-9af3-02dfdf029205

## 🏆 contribution

We love your input! [Let us know](https://github.com/roboflow/sports/issues) what else we should build!
