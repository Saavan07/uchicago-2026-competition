# Curated Market C Logs

These historical standalone Market C runs are retained as examples for debugging
and integration. They document individual development runs rather than results
for the final integrated competition bot.

- `c_only_run_20260410_112113.csv`: Early poor run where C ignored important CPI
  and C earnings events.
- `c_only_run_20260410_113917.csv`: Follow-up poor run used to identify missing
  CPI/C earnings handling and repeated blocked entries.
- `c_only_run_20260410_122214.csv`: A run used as a comparison baseline
  during standalone development.
- `c_only_run_20260410_125247.csv`: Weaker follow-up run used to compare against
  that baseline and identify regressions.
- `c_only_run_20260410_140905.csv`: A run used for
  studying position-hold timing and short-side behavior.
- `c_only_run_20260410_183404.csv`: Later live run showing earnings-shock
  shorting behavior, profit taking, max-hold exits, and remaining hold-time
  concerns.
- `c_only_run_20260410_200812.csv`: A later C-only diagnostic log from the
  standalone development workspace.
