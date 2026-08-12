# Data Folder Guide

## /final — the 4 files that feed the actual reported model
- `monthly_training_dataset_FINAL.csv` — the merged, model-ready table (96 core rows, 
  7 features, target = Flood_Label_HighPlusProxy). **This is the file your notebook loads.**
- `infrastructure_financial.csv` — R&M expenditure, NRW%, water losses, effluent/water 
  quality compliance, by city and financial year (2016/17–2024/25).
- `flood_events_emdat.csv` — 22 EM-DAT flood records (8 High-confidence, 14 Proxy-confidence).
- `rainfall_monthly.csv` — ASSA/AgERA5 monthly extreme precipitation index, both cities.

## /exploratory — tested, verified, but not in the final model
Kept for the methodology/sensitivity-analysis chapter of your report — every file here 
represents a real, documented step in the project, not a discarded mistake.

- `flood_events_floodlist_local.csv` — 20 independently verified local flood events 
  (FloodList/peer-reviewed), used in the sensitivity analysis (all-evidence, 
  confirmed-only tests).
- `drop_scores_original.csv`, `drop_scores_corrected_v2.csv`, `drop_scores_blended.csv` — 
  Green Drop/Blue Drop/No Drop data across three iterations; too sparse for the core 
  7-feature model, used only as secondary/enrichment features.
- `infrastructure_treasury_v2.csv`, `infrastructure_blended.csv` — National Treasury 
  mSCOA R&M data and the blended (Treasury + legacy) version; underperformed the 
  original scraped R&M in cross-validation.
- `treasury_rm_water_raw.csv`, `treasury_rm_stormwater_raw.csv`, 
  `treasury_capital_summary.csv` — raw National Treasury extracts behind the above.
- `monthly_training_dataset_all_evidence.csv`, `monthly_training_dataset_v2_blended.csv`, 
  `monthly_training_dataset_full_rebuild.csv` — the three alternative merged datasets 
  used in the 4-way sensitivity analysis (all scored worse than the final model).
- `fy_coverage_matrix.csv` — financial-year coverage check across all sources, used 
  during data cleaning to decide the final study window.
