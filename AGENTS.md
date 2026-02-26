# AGENTS.md

## Cursor Cloud specific instructions

### Project overview

**astro_bark** is a Python-based scheduled push-notification bot using the [Bark](https://github.com/Finb/Bark) iOS notification service. The main entry point is `main.py`, which runs an infinite scheduler loop sending reminders on Tuesdays and Thursdays via the Bark API.

Additional standalone scripts (`ai_gemini.py`, `ai_zhipu.py`, `demo.py`) are experimental/demo and not part of the core product.

### Dependencies

- Install with `pip install -r requirements.txt` from the repo root.
- The `zhipuai` package has an unlisted transitive dependency on `sniffio`; pip may not install it automatically. If you see `ModuleNotFoundError: No module named 'sniffio'`, run `pip install sniffio`.

### Running the application

- `main.py` requires the `bark_token` environment variable: `bark_token=<token> python3 main.py`
- `demo.py` requires `lingjie_bark_token` (and optionally `jacob_bark_token`).
- The app runs an infinite `while True` loop with `schedule.run_pending()` — it will not exit on its own.

### Known issues

- `main.py` uses time format `"1:30"` in `schedule.every().tuesday.at("1:30")`, but all recent versions of the `schedule` library require zero-padded `HH:MM` format (e.g., `"01:30"`). This causes a `ScheduleValueError` at startup.

### No linter / tests / build

This project has no configured linter, test suite, or build system. Verification is limited to checking that all imports succeed and the scheduler + HTTP request logic functions correctly.
