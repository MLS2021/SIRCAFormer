# Evaluation notes

## Method identifiers and model selection

`B1` = Direct SAR Fusion; `C3` = SIRCAFormer. The other identifiers are AnytimeFormer, DSen2-CR, EDM-CR, and RESTORE-DiT.

The four external models were evaluated using their final (`last`) checkpoints. B1 and C3 used checkpoints selected by validation reflectance MAE (`best`). These are different checkpoint-selection rules; the comparisons describe these evaluated models and do not establish superiority over validation-selected external checkpoints.

## Tables

`grouped_metrics.csv` and `grouped_band_metrics.csv` include overall, AOI, landscape, and change-stratified aggregates. Use `group_type == "overall"` and `group == "all"` for pooled overall results. Full numeric precision is retained from the archived analysis.

Pooled MAE and RMSE aggregate error accumulators over image elements. PSNR uses a reflectance range of one. SSIM and SAM are averaged from patch statistics; SAM is in degrees. AOI-macro effects weight AOIs equally. The `estimand` column distinguishes summaries in the reflectance paired-statistics file. Negative candidate-minus-baseline MAE/RMSE/SAM effects favour the candidate, while positive PSNR/SSIM effects favour it.

NDVI uses (B8 - B4) / (B8 + B4 + 1e-6). Its common reference-defined mask requires reference B8 + B4 > 1e-4. Signed bias is prediction minus reference. A bias difference alone has no universal favourable direction. NDVI paired intervals are descriptive, pointwise intervals; the same is true of the reported individual reflectance intervals rather than a simultaneous guarantee across comparisons. AOI bootstrap intervals describe sampling variability across the evaluated areas, not repeated training-seed variability.

## Reconstruction examples

Twelve examples are provided, two per landscape category. Selection was restricted to the 18 locally archived candidate patches. Within each category, the two patches with the largest positive relative reflectance-MAE reduction versus Direct SAR Fusion were selected. This is a favourable, performance-based selection, not a random or representative sample of the full test set. See `data/examples_index.csv` for errors and selection details. Favourable mountain patches coexist with the slight pooled mountain-category deterioration in the manuscript.

Each NPZ contains `s2_before`, `s2_target`, `s2_after`, `prediction`, and `baseline_prediction` (float32, 4 x 128 x 128, B2/B3/B4/B8 order); `s1_before`, `s1_target`, and `s1_after` (float32, 2 x 128 x 128, VV/VH order); and `ndvi_prediction`, `ndvi_reference`, `ndvi_valid` (128 x 128).

Optical arrays are physical reflectance. SAR arrays are the dataset values obtained by clipping backscatter to [-30, 5] dB and mapping linearly to [0, 1], before channel standardization. `s2_target` is the held-out reference, not an available input: model evaluation must hide the entire target optical frame. No model implementation or weights are included in this initial package.

Prediction and baseline arrays were checked against the archived C3 and B1 per-patch MAE accumulators (absolute tolerance 1e-7), and each example has lower C3 MAE than B1. The chosen set is for illustrating successful reconstructions and cannot estimate the frequency of improvement.
