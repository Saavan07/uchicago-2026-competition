# UChicago Trading Competition 2026

This repository brings together the trading bot and portfolio research our team worked on for the 2026 UChicago Trading Competition.

My main focus was researching and building the integrated Case 1 trading bot we ran at the competition. That involved bringing our strategies together, working on execution and inventory controls, and debugging and testing with my teammates. I also contributed to our Case 2 portfolio research.

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

## My work and the team

I worked on this project with Ayush Chandra, Caleb Goodman, and Parry Nall. Our shared work comes from [the team repository](https://github.com/ayushchandra8907/uchicago-2026-competition).

My work included the integrated runtime, strategy iterations, risk and execution controls, diagnostic traces, ETF and Market C integration, competition launchers, and settlement and shutdown handling. Some of that involved adapting and integrating my teammates' strategies, with their contributions identified in the code and commit history.

No audited placement, profitability, Sharpe ratio, or live return is claimed here. Any future result claim needs its run configuration, data, evaluation split, and retained evidence.

## Publication and historical artifacts

The original repository is preserved. Public cleanup removes credential values and duplicated email-attachment archives that contained them. Generated logs, caches, and machine metadata are excluded from the current working tree where they are not needed to reproduce the code. Original author records and third-party notices are retained. No new blanket license is assigned to the team's work.

See [publication history and original commit mapping](docs/publication-history.md) for the cleaned-copy provenance.
