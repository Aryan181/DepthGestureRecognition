# Capturing Depth, Detecting Hand Gestures using LiDAR Camera

Access the LiDAR camera on supporting devices to capture precise depth data and detect hand gestures.

## Example demonstration 

https://github.com/user-attachments/assets/282f34d1-40bd-407f-adfb-8e3b8da77985

## Overview


<img width="631" alt="image" src="https://github.com/user-attachments/assets/3267489c-79ea-4b93-8d46-eacab252c1be">


This sample code project demonstrates how to capture and render depth data from the LiDAR camera, as well as detect hand gestures using Vision framework. The app operates in two modes:

1. Streaming mode: Captures synchronized video and depth data.
2. Photo mode: Captures photos with depth data.

In both modes, the app provides Metal-based visualizations of the depth and image data. Additionally, it now includes hand gesture recognition capabilities.


<img width="631" alt="image" src="https://github.com/user-attachments/assets/a2e26099-7dc9-45ee-9c11-b5214bf6ab40">

<img width="858" alt="image" src="https://github.com/user-attachments/assets/ef02c205-e4e9-4be2-abc2-c222f7537356">

<img width="617" alt="image" src="https://github.com/user-attachments/assets/4b84a379-f47d-4a6f-ad64-2d265b553528">


## New Features

- Hand pose detection using Vision framework
- Gesture recognition based on finger positions

## Configure the sample code project

Run this sample code on a device that provides a LiDAR camera, such as:
- iPhone 12 Pro or later
- iPad Pro 11-inch (3rd generation) or later
- iPad Pro 12.9-inch (5th generation) or later

## Key Components

### LiDAR Camera Configuration

The `CameraController` class configures and manages the capture session. It retrieves the LiDAR camera and sets up the appropriate video and depth formats.

### Hand Pose Detection Setup

The `CameraController` now includes methods to set up and process hand pose detection:

```swift
private func setupHandPoseDetection() {
    handPoseRequest = VNDetectHumanHandPoseRequest()
    handPoseRequest?.maximumHandCount = 1
}
```

### Gesture Recognition

The app processes detected hand poses to recognize gestures:

```swift
private func recognizeGesture(observation: VNHumanHandPoseObservation) {
    guard let thumbTip = try? observation.recognizedPoint(.thumbTip),
          let indexTip = try? observation.recognizedPoint(.indexTip),
          let middleTip = try? observation.recognizedPoint(.middleTip),
          let ringTip = try? observation.recognizedPoint(.ringTip),
          let littleTip = try? observation.recognizedPoint(.littleTip),
          let wrist = try? observation.recognizedPoint(.wrist) else {
        return
    }
    // Gesture recognition logic here
}
```

## Capture Synchronized Video and Depth

The app uses `AVCaptureDataOutputSynchronizer` to synchronize the delivery of video and depth data. The `dataOutputSynchronizer(_:didOutput:)` method handles this synchronized data.

## Capture Photos and Depth

When the user taps the Camera button, the app switches to photo mode and captures a photo with depth data using `AVCapturePhotoOutput`.

## Hand Gesture Detection

The app now processes each frame to detect hand poses and recognize gestures. This adds an interactive element to the depth capture functionality.

## Usage

1. Run the app on a supported device.
2. The app starts in streaming mode, showing real-time depth data.
3. Perform hand gestures in front of the camera to test the gesture recognition feature.
4. Tap the Camera button to switch to photo mode and capture depth photos.

## Implementation Details

### Capturing Depth Data

The app captures depth data using the LiDAR camera's depth data output. It configures the `AVCaptureDepthDataOutput` to deliver depth data in the appropriate format.

### Visualizing Depth Data

The app uses Metal to efficiently render the depth data. It creates a color representation of the depth values, allowing users to visually understand the depth information.

### Synchronizing Video and Depth

To ensure accurate alignment between the color image and depth data, the app uses `AVCaptureDataOutputSynchronizer`. This synchronizer delivers color and depth data as a matching pair.

### Processing Hand Gestures

The app uses the Vision framework to detect hand poses in each frame. It then analyzes the positions of key points (like fingertips and wrist) to recognize specific gestures.

## Requirements

- Xcode 12.0 or later
- iOS 14.0 or later
- A device with LiDAR camera (iPhone 12 Pro or later, or compatible iPad Pro models)

