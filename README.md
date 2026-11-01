# Blind to Bright
## Offline, Danger-First AI Smart Glasses for Safer Outdoor Mobility

Blind to Bright is a proposed assistive smart-glasses platform intended to help visually impaired people understand nearby outdoor hazards and receive concise, prioritized audio guidance.

**Important status note:** This repository is a development scaffold. It includes a working priority-engine example, simulation, tests, and project documentation. Real camera integration, trained AI model weights, sensor calibration, GPS, OCR, TTS hardware, and user validation are not yet implemented here. Do not describe this repository as a complete or safety-certified mobility aid.

## Problem
Outdoor navigation can be challenging because of potholes, open drains, uneven footpaths, stairs, parked vehicles, two-wheelers, autos, stray animals, and crowded pedestrian areas. Blind to Bright is designed as a supplement to a white cane or other established mobility aids, not a replacement.

## Proposed solution
RGB and NoIR cameras capture the environment. Edge AI identifies candidate objects and hazards. Optional distance sensing and tracking add context. The Danger-First Decision and Priority Engine ranks events by severity, proximity, approach trend, and relevance to the walking path. The system selects the most important alert first instead of announcing every object. OCR is intended for on-demand sign reading. Core inference and speech are designed for local operation; SOS transmission requires a communication connection.

## Workflow
```text
RGB / NoIR Cameras
        -> Frame Processing
        -> AI Object / Hazard Detection ---- OCR (on demand)
        -> Distance / GPS Context
        -> Sensor and Context Fusion
        -> Danger-First Priority Engine
        -> Alert Selection
        -> Offline TTS / Urgent Beep
        -> Open-ear / Bone-conduction Audio
```

## Repository status
| Component | Status |
|---|---|
| Priority scoring and ranking | Starter implementation |
| Alert message generation | Starter implementation |
| Simulation demo | Included |
| Config loading (`config/config.yaml`) | Included |
| Unit tests + GitHub Actions CI | Included |
| Camera capture | Placeholder interface |
| YOLO / hazard model | Not included; integration required |
| Distance sensor / GPS | Placeholder interfaces |
| OCR / TTS | Integration required |
| Hardware validation | Not completed |

## Hardware direction (proposed, not yet validated)
- Raspberry Pi 5 (main edge computer)
- Pi NoIR camera with IR LEDs (low light) and a wide-angle RGB camera option
- HC-SR04 ultrasonic distance sensor (must be calibrated; ToF is an alternative)
- NEO-6M GPS module, MPU-6050 motion sensor, USB microphone, push button
- Bone-conduction / open-ear speaker
- 10,000 mAh power bank with regulated supply
- 3D-printed lightweight frame; consider placing compute and battery in a waist/neck enclosure
- Optional AI accelerator (for example Raspberry Pi AI HAT+ / Hailo)

Confirm connector compatibility, power budget, heat, mounting, and software support before purchasing parts.

## Software direction
Python 3.10+, OpenCV, a lightweight detector (planned: YOLOv8-Nano via TFLite/accelerator runtime), depth estimation (planned: MiDaS-Tiny), OCR (Tesseract / PaddleOCR), offline TTS (Piper) and speech input (Vosk), SQLite, optional GPS/SOS via Firebase. **None of these models or services are included yet**; no model weights are shipped. Check model and dataset licenses before use.

## Quick start
Requires Python 3.10+.

**Windows (PowerShell)**
```powershell
git clone https://github.com/YOUR_USERNAME/Blind_to_Bright_GitHub.git
cd Blind_to_Bright_GitHub
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python -m src.main --demo
pytest
```
**Linux / macOS / Raspberry Pi**
```bash
git clone https://github.com/YOUR_USERNAME/Blind_to_Bright_GitHub.git
cd Blind_to_Bright_GitHub
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m src.main --demo
pytest
```
On the Raspberry Pi also run `pip install -r requirements-pi.txt` (OpenCV, serial GPS).
Run the demo as `python -m src.main` (not `python src/main.py`). Severity values and weights are read from `config/config.yaml`.

The demo uses illustrative sample detections only. It does not access a camera or detect real hazards.

## Safety and responsible use
- Experimental project; not a certified medical or mobility device.
- Must not replace a white cane, guide dog, orientation-and-mobility training, or other established assistance.
- Never test by deliberately exposing anyone to traffic, stairs, drains, or other hazards.
- Start in controlled environments with a sighted safety assistant.
- False positives and missed detections are possible. No alert does not mean the path is clear.
- GPS location alone does not send an SOS; a communication channel is required.
- Obtain consent before recording or sharing images. Prefer local processing.

## Validation plan
Measure per-class precision/recall/mAP, false alerts, missed hazards in a controlled protocol, end-to-end latency, distance error, battery runtime, audio intelligibility, comfort, and usability. Label all numerical performance goals as targets until measured.

## Roadmap
1. Validate Raspberry Pi, one camera, and power.
2. Integrate a detector and measure latency.
3. Select and calibrate the distance sensor.
4. Add tracking and approach estimation.
5. Tune priority and alert suppression in controlled tests.
6. Integrate offline TTS and on-demand OCR.
7. Add GPS/SOS after choosing a communication method.
8. Conduct supervised evaluation and iterate.

## Team
Team: HackMinds | Project: Blind to Bright | Smart India Hackathon 2026

## License
Original project code and documentation are released under the MIT License. Third-party models, datasets, libraries, and hardware designs may have separate licenses.
