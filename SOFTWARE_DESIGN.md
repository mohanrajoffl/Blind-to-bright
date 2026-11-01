# Software Design

- `src/main.py`: command-line entry point and demo
- `src/models.py`: detection and prioritized-event data structures
- `src/priority_engine.py`: configurable ranking heuristic
- `src/alert_manager.py`: concise alert text
- `src/config.py`: loads `config/config.yaml` into the priority engine settings
- `src/perception/`: camera and detector interfaces
- `src/sensors/`: distance and GPS interfaces
- `src/output/`: speech and audio interfaces
- `config/config.yaml`: severity, weights and distance settings (used by the demo)
- `tests/`: unit tests

## Detection contract
Each detection contains a class label, confidence (0..1), optional distance in metres, optional approach score (0..1), path relevance (0..1), and timestamp. Unknown measurements must remain `None`, not fabricated.

## Priority score
`score = severity * (w_proximity * proximity + w_approach * approach + w_path * path_relevance)`

This is a configurable ranking heuristic, not a collision probability. Tune weights only through documented tests.

## Model integration
No model weights are included. Document model name/version, source, license, supported classes, input size, runtime requirements, measured latency, and evaluation results.

## Planned stack (not included yet)
YOLOv8-Nano (detection), MiDaS-Tiny (depth), Tesseract / PaddleOCR (on-demand text), Piper (TTS), Vosk (STT), SQLite (local data). Each must be wrapped behind the interfaces in `src/perception`, `src/sensors` and `src/output` so tests keep running without hardware.
