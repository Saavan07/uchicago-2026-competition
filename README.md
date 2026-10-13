# UChicago Trading Competition 2026

A collaborative competition repository containing the team's Case 1 trading bot and Case 2 portfolio-strategy research. This project is separate from the SIG Predictions Cup.

Saavan Kiran led development and research for the integrated Case 1 bot used by the team at the competition. The bot incorporates teammate components and joint debugging and experimentation. Saavan also contributed to Case 2; that case is shared work and is not presented as his sole implementation.

## Start here

| Area | Where to look | Scope |
| --- | --- | --- |
| Case 1 integrated bot | `case1/Case 1 Saavan/` | Event-driven trading runtime, strategy configuration, order management, and diagnostics |
| Competition entry points | `run_competition.py`, `run_competition_upgraded.py` within that directory | Integrated bot and optional prediction-market companion |
| Market A logic | `a_bot_strategy.py`, `ayush_a_port.py`, `a_news_tracker.py` | Valuation, news response, inventory and order decisions; preserves Ayush's strategy lineage |
| Additional strategy work | ETF, Market B, and Market C modules in the same directory | Cross-market integration and experiments, with configuration-dependent activation |
| Team components | `case1/ayush_work/`, `case1/caleb_work/`, `case1/Parry/` | Original teammate implementations and experiments |
| Case 2 | `case2/` | Portfolio submissions, notebooks, validation, diagnostics, and model-search experiments |
| Exchange client | `utc_exchange_codebase/utcxchangelib-main/` | Vendored competition client, with its own license |

## Case 1 architecture

```text
Exchange events -> async client/runtime -> pricing and strategy state
  -> inventory/risk checks -> order management -> exchange orders
  -> structured trace/journal -> offline diagnostic summaries
```

The repository includes earnings/news handling, passive-order guards, ETF and cross-market strategy components, shutdown and settlement handling, and diagnostic tests. Experimental branches are retained for comparison. A module's presence does not mean it was enabled in the final competition configuration.

## Offline verification

Python 3.13 was used for the October 2026 verification. Create an isolated environment from the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m unittest discover -s 'case1/Case 1 Saavan/tests'
```

The tests exercise strategy and runtime behavior with fake exchange objects and fixtures. They do not connect to a live competition exchange. See `docs/verification.md` for exact results and limits.

To connect to an exchange, you must supply your own authorized `UTC_HOST`, `UTC_USERNAME`, and `UTC_PASSWORD` environment variables. The cleaned entry points require explicit credentials. The historic competition server is not part of the offline reproduction path.

## Case 2

The directory contains `submission.py`, `submission_converted.py`, research/backtesting helpers, diagnostics, and notebooks. `validate.py` implements local historical validation with transaction and borrowing costs and time-series splits. The default single split imports `submission_converted.py`, while `--cv` currently imports `submission.py` inside each fold. These are distinct variants, so their printed results are not a like-for-like comparison.

From `case2/`, run `python validate.py --help` to inspect the evaluator. The repository includes `prices.csv` and `meta.csv` for local validation. `whole_dataset_model_search.py` still has a teammate-specific absolute path and should be adapted before use. Notebook outputs and tuning runs are not claims of out-of-sample competition performance.

## Team and contribution record

The source repository is [ayushchandra8907/uchicago-2026-competition](https://github.com/ayushchandra8907/uchicago-2026-competition), with work by Saavan Kiran, Ayush Chandra, Caleb Goodman, and Parry Nall.

Saavan's recorded history covers the integrated runtime, strategy iterations, risk and execution controls, traces, ETF and Market C integration, competition launchers, and settlement/shutdown behavior. Some changes explicitly port or integrate teammate strategies; those origins remain identified in code and history. Commit counts are not used to assign exclusive ownership.

No audited placement, profitability, Sharpe ratio, or live return is claimed here. Any future result claim needs its run configuration, data, evaluation split, and retained evidence.

## Publication and historical artifacts

The original repository is preserved. Public cleanup removes credential values and duplicated email-attachment archives that contained them. Generated logs, caches, and machine metadata are excluded from the current working tree where they are not needed to reproduce the code. Original author records and third-party notices are retained. No new blanket license is assigned to the team's work.
