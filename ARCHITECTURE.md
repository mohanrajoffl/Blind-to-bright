# System Architecture

## Layers
**Input:** RGB camera, NoIR camera + IR illumination, optional distance sensor, GPS, user button.

**Perception:** frame capture, pre-processing, object/hazard detection, optional OCR, object tracking.

**Context and fusion:** associate detections with distance only when calibrated; estimate approach only from timestamped tracking; estimate path relevance; preserve uncertainty.

**Decision:** assign severity, rank by proximity/approach/path relevance, suppress repeated static alerts, allow urgent events to supersede lower-priority messages.

**Output:** short voice alert, offline TTS, optional urgent beep, open-ear/bone-conduction audio.

```text
Camera(s) -> Frame Processor -> Detector ----+
                                              |
Distance Sensor -----------------------------+-> Context/Fusion
                                              |        |
GPS (optional) -------------------------------+        v
                                                Priority Engine
                                                       |
                                                Alert Selector
                                                       |
                                                  TTS / Beep
                                                       |
                                                      User
```

## Safety boundaries
- A bounding box is not a verified obstacle distance.
- A class label does not prove a path is blocked.
- Camera field of view does not guarantee full environmental coverage.
- Sensor-camera association must be calibrated.
- No alert must not be interpreted as proof that the path is clear.
