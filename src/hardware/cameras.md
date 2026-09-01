# Native Cameras

## Why cameras need their own subsystem

Vision algorithms need a stream of images, not a generic “camera object.” SW9S's native camera layer turns Linux video devices into OpenCV images that missions can inspect.

## SW9S implementation

`src/video_source/appsink.rs` builds a GStreamer pipeline around V4L2 JPEG input. It decodes frames, tees them toward an OpenCV appsink and a recording branch, and can push a stream to a local RTSP endpoint. `Camera::jetson_new` fixes the native path to 640×480 at 30 FPS.

A detached OS thread repeatedly captures the newest frame into a shared `Option<Mat>`. `get_mat()` takes the latest frame. This is a latest-value cache rather than a queue: it favors current visual information over preserving every frame.

## Inputs → outputs

```text
/dev/videoN → GStreamer pipeline → newest OpenCV Mat → FrontCamIO/BottomCamIO → vision action
```

## Operational dependencies

The source assumes V4L2 devices, GStreamer plugins/codecs, writable `/tmp`, and—in the RTSP path—a server at `127.0.0.1:8554`. Jetson and non-Jetson encoding paths differ. These are runtime dependencies, not guarantees established by Cargo alone.

## Debugging

Check the configured device path, capture pipeline string, generated recordings, and detector input dimensions. A missing frame may cause polling rather than a clean error, so validate camera availability before debugging a detector.

## Last verified against SW9S

Source-derived from `fc780a1`; deployed devices and media services need team confirmation.
