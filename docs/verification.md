# Verification on October 13, 2026

## Environment and installation

Python 3.13 in an isolated environment. The root requirements now install the vendored exchange client rather than fetching an unpinned remote repository. The client's `pyproject.toml` previously required protobuf 5.29.0 and grpcio 1.71.0 even though the checked-in generated bindings require protobuf 6.31.1 and grpcio 1.78.0. Its package version and minimum Python version also disagreed with `setup.py`. Those metadata fields now agree with the existing setup and generated code.

`python -m pip install -r requirements.txt` completed successfully, and `python -m pip check` reported no broken requirements. Scientific packages are not locked to a complete frozen environment.

## Case 1

`python -m unittest discover -s 'case1/Case 1 Saavan/tests'` passed all 211 tests after the publication changes. This includes a new check that the integrated launcher rejects missing explicit credentials. The previous 210 tests passed before that change.

These are offline tests using fixtures and fake exchange objects. No live server connection, trade, competition replay, or profitability benchmark was run in this verification. The count is not a claim that every experimental teammate module is tested.

## Case 2

Both submission variants, notebooks, research tools, `prices.csv`, and `meta.csv` are included. The local evaluator's single-split path selects `submission_converted.py`, while its cross-validation loop selects `submission.py`. That inconsistency is preserved and called out rather than presenting their outputs as directly comparable.

`python validate.py --help` passed. Loading the supplied data and constructing `MyStrategy` also passed: 37,800 price rows for 25 assets and 25 metadata entries. This verifies imports and data loading, not the strategy's predictive quality.

No model tuning, full backtest, performance benchmark, or official competition scoring was rerun. A teammate-specific absolute path remains in `whole_dataset_model_search.py`.

## History and attribution

Saavan confirmed that he led the Case 1 integrated bot and contributed to Case 2. Teammate strategy lineages remain identified. October publication maintenance is distinct from the competition implementation.

The prepared working tree replaces the known competition password and removes its default from the integrated launch path. The duplicate email-attachment ZIP, Python caches, package-install metadata, and Finder files are excluded from the current tree. The public copy removes those values throughout the copied history; deleting a current-file value alone would not have been sufficient. See publication-history.md for the scope and commit map. Credential owners should invalidate any exposed credentials that remain usable.
