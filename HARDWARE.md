# Hardware Plan

Planning list only; verify exact models and compatibility before purchase.

| Subsystem | Proposed component | Purpose | Status |
|---|---|---|---|
| Compute | Raspberry Pi 5 | Main edge computer | Proposed |
| AI acceleration | Optional AI HAT+ / Hailo | Faster inference if needed | Validate model/runtime |
| Low-light camera | Pi NoIR camera + IR LEDs | Low-light capture | Proposed |
| Day camera | RGB wide-angle camera | Daytime capture | Proposed |
| Proximity | HC-SR04 ultrasonic (ToF alternative) | Distance measurement | Calibrate before use |
| Location | NEO-6M GPS | Location context | Optional |
| Motion | MPU-6050 | Head motion / orientation | Proposed |
| Voice input | USB microphone | Voice commands (Vosk) | Proposed |
| User input | Push button | OCR request / SOS | Proposed |
| Audio | Bone-conduction speaker | Voice alerts | Proposed |
| Power | 10,000 mAh power bank + regulation | Portable power | Calculate load / runtime |
| Frame | 3D-printed glasses frame | Mounting | Design and test comfort |

## Engineering checks
- Raspberry Pi and accelerator power/thermal budget
- Camera connector and cable compatibility
- IR illuminator safety, current draw, and heat
- Sensor range, field of view, and calibration
- Audio audibility without masking ambient sound
- Battery capacity, regulator efficiency, and runtime
- Frame comfort, stability, and cable strain relief

Keep the glasses frame light. Consider placing compute and battery in a waist/neck enclosure.
