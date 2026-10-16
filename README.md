# SIRCAFormer: Target-centred SAR change-guided reconstruction of Sentinel-2 reflectance across heterogeneous landscapes

**Authors:** Zheng Luo<sup>1</sup>, Zhenfeng Shao<sup>1*</sup>, Hong Shu<sup>1</sup>, Bingwei Hui<sup>2</sup>, Bo Liu<sup>1</sup>, Yige Liang<sup>1</sup>, Yi Bao<sup>3,1</sup>

<sup>1</sup> State Key Laboratory of Information Engineering in Surveying, Mapping and Remote Sensing (LIESMARS), Wuhan University, Wuhan 430072, China  
<sup>2</sup> Key Laboratory of Automatic Target Recognition, School of Electronic Science, National University of Defense Technology, 410073, China  
<sup>3</sup> Institute of Space Earth Science, Nanjing University, Suzhou, China  

**Corresponding author:** Zhenfeng Shao ([shaozhenfeng@whu.edu.cn](mailto:shaozhenfeng@whu.edu.cn)).

## Abstract

Optical acquisition gaps leave target-date surface reflectance unobserved, while SAR changes provide complementary information whose optical interpretation varies across landscapes. We propose SIRCAFormer to reconstruct missing Sentinel-2 reflectance from bracketing optical images and three-phase SAR observations. A temporal CNN–Transformer backbone produces a base estimate, and a separate correction branch combines signed SAR changes on both sides of the target date with observed optical evolution. Local cross-attention associates these changes with reconstruction features, and bounded band-specific residuals refine the frozen backbone prediction. On an AOI-disjoint test set spanning six landscape categories, SIRCAFormer achieved the lowest pooled MAE and RMSE and the highest PSNR and SSIM among four representative comparison methods. Relative to Direct SAR Fusion using the same input observations, MAE and spectral angle decreased by 2.33% and 2.96%, respectively, with lower MAE in 13 of 17 test AOIs. Gains varied across landscapes and diminished under larger before–after optical changes. These results demonstrate that explicit target-centred SAR changes, interpreted with optical temporal context, can improve missing-date reflectance reconstruction beyond their use in the temporal backbone.

## Scope of this initial package

This package contains selected evaluation tables, three result figures, and twelve selected reconstruction examples. It is a partial research-output release. It does not contain the model implementation, training code, pretrained weights, full dataset, complete train/validation/test split manifests, or a complete test-set input archive. The twelve examples include input observations and reference data, but the package does not yet support end-to-end training or inference reproduction because model implementation and weights are not included.

- `results/`: archived evaluation summaries for the six methods.
- `figures/`: landscape/change, correction-response, and NDVI figures.
- `data/examples/`: two favourable examples per category across Agricultural Zone, Forest, Grassland, Mountain, Peri-Urban Mixed, and Wetland; each includes optical/SAR observations, reference, SIRCAFormer and Direct SAR Fusion predictions, and NDVI arrays.
- `data/examples_index.csv`: case-level errors, relative gains, paths, and selection criteria.
- `docs/evaluation_notes.md`: method identifiers, evaluation conventions, and example selection.

Results use B2, B3, B4, B8 in that order. Reflectance metrics cover 11,780 patches from 17 test AOIs. `B1` denotes Direct SAR Fusion and `C3` denotes SIRCAFormer.

See the evaluation notes for model-selection conditions and the distinction between pooled and AOI-macro summaries. These examples were intentionally selected for positive MAE improvement relative to Direct SAR Fusion. They are not a random sample of test performance. Mountain examples do not negate the small pooled mountain-category deterioration reported in the manuscript.
