# Changelog

## 0.1.1
### Fixed
- `requirements.txt` / `requirements-pi.txt` contained literal `\n` characters: pytest was never installed and the Pi file installed nothing.
- Plain `pytest` failed with `ModuleNotFoundError: No module named 'src'` (added `pytest.ini`).
- `LICENSE` text was cut off after "WITHOUT WARRANTY OF ANY KIND." (full MIT text restored).
- `Detection.timestamp` defaulted to year 0001; now defaults to the current UTC time.
- `config/config.yaml` was never read; severities were hard-coded (and `animal` was missing from the demo).
- README Windows activation command had doubled backslashes.
- Demo banner used a non-ASCII dash that can break some Windows consoles.
### Added
- `src/config.py`, more unit tests (models, alerts, config, demo), GitHub Actions CI, `models/README.md`, CHANGELOG.
- HARDWARE.md and README now list the specific proposed components.
