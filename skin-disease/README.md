# Skin Image Classification: Accuracy, Uncertainty, and Human Review

A student portfolio project that audits a small image dataset before comparing image-classification models and evaluating a confidence-based human-review policy.

Open `Skin_Image_Classification_Human_Review.ipynb` for the full executed analysis, charts, and conclusions.

## Main findings from the recorded run

- Kaggle version 1 contains 1,429 combined-folder images. The documented class distribution is inconsistent with the files.
- A conservative perceptual/pixel-hash audit found 749 image groups, including one conflicting-label group. Excluding its four images and retaining one representative per remaining group left 748 observations.
- Frozen MobileNetV3-Small embeddings plus logistic regression achieved 86.7% accuracy and 0.817 macro-F1 on 150 held-out images. The RGB-histogram baseline achieved 0.463 macro-F1.
- A policy selected before test evaluation accepted 134 images and deferred 16. Accepted-only accuracy was 90.3%, but 13 incorrect model labels remained accepted. Deferral routed only seven of 20 model errors to review. Actual reviewer performance was not measured.
- The data include source signatures, possible stock-style controls, unknown patient identities, and unverified labels. This is a benchmark of agreement with supplied labels, not a clinical diagnostic system.

## Run

The recorded environment used Python 3.14.4 on macOS with CPU inference. Exact package versions are in `requirements.txt` and `artifacts/environment.json`; package availability may differ on other platforms.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Open the notebook in Jupyter, VS Code, or another notebook client using that environment. Run cells in order. With no `SKIN_DATA_ROOT`, KaggleHub downloads `gupiii/infectious-skin-disease-dataset/versions/1`. The first run also downloads ImageNet-pretrained MobileNetV3-Small weights. Network access is needed for those downloads, and Kaggle may request authentication.

For an existing extraction, set this variable before starting the notebook kernel:

```bash
export SKIN_DATA_ROOT=/path/to/extracted-dataset
```

Point it to the directory containing `Dataset_1`, `Dataset_2`, and `Dataset_Gabungan`. Run from this project directory so generated files are written under `artifacts/`.

The notebook caches frozen embeddings using an input-content and model-version key. Raw dataset images and pretrained weights are not bundled in the project archive.

## Included evidence

- `artifacts/dataset_provenance.json`: data-card snapshot, version, archive checksum, and attribution.
- `artifacts/image_manifest.csv`: file integrity, hashes, dimensions, and image-property audit.
- `artifacts/near_duplicate_candidates.csv`: candidate duplicate links, not verified patient matches.
- `artifacts/excluded_label_conflicts.csv`: quarantined conflicting-label images.
- `artifacts/split_manifest.csv`: reproducible, mutually exclusive partition assignments.
- `artifacts/policy_validation_curve.csv`: validation-only threshold selection evidence.
- `artifacts/test_predictions.csv`: final benchmark predictions and routing outcomes.
- `artifacts/human_review_queue.csv`: deferred cases with blank reviewer fields. No reviewer results are invented.
- `artifacts/metrics.json` and `artifacts/summary.txt`: computed results.

## Attribution

Lutfi Farhan Prayoga (2026), *Infectious Skin Disease Dataset & Classification using Hybrid MobileNetV2-Xception with CLAHE Image Enhancement*, Universitas Airlangga.

- Dataset: https://www.kaggle.com/datasets/gupiii/infectious-skin-disease-dataset
- Curator repository: https://github.com/lutfi015/skin-disease

The Kaggle card lists CC BY 4.0 and names the University of Jammu Monkeypox Images Dataset and MSID as upstream sources. Original image permissions, consent, clinical verification, and demographic representativeness have not been independently established. Raw photos are not redistributed here.
