# Vision Pipeline

## Why vision needs a pipeline

An image does not tell a robot what to do until it is converted into a measurement that a mission can use. SW9S's native vision pipeline moves from pixels to detections to normalized geometric values, then into motion actions.

## Beginner mental model

A **bounding box** is a rectangle around a detected object. An **offset** says where the object lies relative to image center. Normalizing an offset converts pixel-specific values into a reusable range, often near -1 to 1. An **angle** may describe a path or pole orientation in the image.

## SW9S implementation

`src/vision/mod.rs` defines `VisualDetector`, `VisualDetection`, `RelPos`, `RelPosAngle`, `Offset2D`, `Angle2D`, and drawing helpers. `src/missions/vision.rs` obtains frames through `FrontCamIO`/`BottomCamIO`, invokes detectors, can write annotated images, and transforms results for movement code.

```mermaid
flowchart LR
    A[OpenCV Mat] --> B[VisualDetector]
    B --> C[VisualDetection]
    C --> D[Offset / angle / class]
    D --> E[Mission transform]
    E --> F[Movement action]
```

## Classical detectors

`gate_cv.rs`, `path_cv.rs`, `slalom.rs`, and `octagon.rs` use image resizing, color-space thresholds, contours, and minimum-area rectangles. A contour is a connected boundary in an image; thresholding turns a color rule into a mask that makes those shapes easier to find.

Color ranges come from `ColorProfile` configuration. This makes calibration important: a threshold that works in one lighting condition may fail in another.

## Debugging

Start at the frame: verify camera source, resolution, color format, and saved annotated output before changing detection logic. Then inspect threshold/mask/contour choices and only then tune movement response. A detection bug and a control bug can look identical from the vehicle's motion alone.

## Last verified against SW9S

Source-derived from `fc780a1`.
