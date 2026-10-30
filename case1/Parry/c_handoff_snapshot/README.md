# Market C Handoff Snapshot

This folder preserves selected Market C development files from Parry's standalone
workspace for reference alongside the team's integrated bot.

## Files

- `C.py`: Current standalone C-only bot architecture used as the base for the
  repo version in `case1/Parry/prediction_C.py`. It includes the newer C fair
  model, CPI/macro handling, CSV diagnostics, and earnings-shock lifecycle work.
- `prediction.py`: Older standalone C-only implementation. Treat this as
  historical context only; it is useful for understanding the earlier fair/rate
  model and simpler execution loop, but it is not the current source of truth.
- `logs/`: Curated run logs from the private workspace. These were selected
  to illustrate different strategy behaviors during Market C development.

## Important Notes

- The current repo bot remains `case1/Parry/prediction_C.py`.
- These source snapshots have been sanitized to use `UCHICAGO_USERNAME` and
  `UCHICAGO_PASSWORD` environment variables instead of hardcoded credentials.
- This is intentionally not a full folder dump: `.venv`, `__pycache__`, generated
  files, and most logs are excluded.
