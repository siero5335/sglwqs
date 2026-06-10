# sglwqs 0.8.13.9001

## Bug fixes

* Bootstrap-only inference summaries now label WQS positive/negative rows as
  loading magnitudes and suppress p-values for these loading rows, avoiding
  confusion with signed downstream refit coefficients.
* Covariate bootstrap summaries and MI bootstrap inference summaries now respect
  the requested confidence level when intervals are displayed.
* Stratified binomial bootstrap resampling now handles singleton strata without
  falling into R's scalar `sample()` behavior.
* MI bootstrap pooling now preserves matrix dimensions when there is only one
  exposure variable.
* `tidy(what = "coefficients", conf.int = TRUE)` now merges bootstrap
  confidence intervals for WQS coefficient rows when intercept or covariate rows
  are present.
* `sglwqs()` and `sglwqs_mice()` now validate that `train_prop` is a single
  finite value strictly between 0 and 1.
* Added `vcov.sglwqs()` for downstream refit and bootstrap-only covariance
  extraction.

# sglwqs 0.8.13

## Improvements

* Bootstrap aggregation now retains covariate coefficients (`cov_coef`) across
  iterations and stores aggregated summaries in `fit$boot_info$mean_cov_coef`,
  `se_cov_coef`, and percentile intervals.
* Bootstrap aggregation now also stores overall and group-level WQS index-sum
  summaries, making bootstrap-only two-stage summaries available through
  `summary_inference()` and `plot_inference_results()`.
* Checkpointed bootstrap runs now persist and restore covariate coefficient
  matrices alongside exposure coefficient matrices.
* MI pooling helpers prefer bootstrap-aggregated covariate coefficients when
  available, while preserving the existing top-level `fit$cov_coef` contract
  for backward compatibility.
* `sglwqs_mice()` now Rubin-pools downstream GLM coefficients from
  `refit = "full"` as well as `validation = TRUE`, exposing pooled WQS-index
  inference via `fit$pooled$inference` and pooled covariate coefficients via
  `fit$pooled$covariates`.
* MI fits with `bootstrap = TRUE` and no downstream GLM now expose pooled
  bootstrap-derived inference via `fit$pooled$bootstrap_inference`.
* Added `compute_diagnostics()` plus unified `summary_inference()` and
  `plot_inference_results()` helpers so validation, refit, and bootstrap-only
  paths can be accessed through the same entry points.
* Diagnostic messages and bootstrap failure warnings now use fact-only wording
  consistent with the diagnostics API.
