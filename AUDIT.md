# Technical Audit

Rigorous review of the `YoloCellViabilityDetection` repository, focused on bugs, reproducibility, maintainability and low-risk contribution opportunities.

## Summary

The project is a strong academic YOLOv8 notebook for detecting and classifying cell viability in brightfield microscopy images. The core scientific workflow is documented in the notebook and README, but the repository still benefits from small structural corrections that improve execution clarity without changing the research logic.

## Changes Applied

- Renamed the notebook from `tcc_yolo_cell_detection.ipynb.ipynb` to `tcc_yolo_cell_detection.ipynb`.
- Updated `torchvision` minimum version to `0.21.0`, which aligns better with `torch>=2.6.0`.
- Added Git ignore rules for generated YOLO/Kaggle artifacts, model weights and inference reports.
- Expanded README reproducibility notes and documented Kaggle-specific assumptions.

## High-Priority Findings

### 1. Notebook filename mismatch

**Status:** Fixed.

The README instructed users to execute `tcc_yolo_cell_detection.ipynb`, but the repository stored `tcc_yolo_cell_detection.ipynb.ipynb`. This creates immediate friction for users and external references.

### 2. Kaggle-specific hardcoded paths

**Status:** Documented, not changed in code.

The notebook relies heavily on paths such as `/kaggle/input/...` and `/kaggle/working/...`. This is valid for the original environment, but it limits local execution.

Recommended next step:

```python
DATA_ROOT = Path(os.getenv("YOLO_CELL_DATA_ROOT", "/kaggle/input/dataset2-tcc/DatasetV2"))
WORK_ROOT = Path(os.getenv("YOLO_CELL_WORK_ROOT", "/kaggle/working"))
```

This would keep Kaggle compatibility while allowing local overrides.

### 3. Generated artifacts were not ignored

**Status:** Fixed.

Training runs, converted datasets and model weights can be large and should not enter Git accidentally. The `.gitignore` now covers typical YOLO/Kaggle outputs.

## Medium-Priority Findings

### 1. Notebook contains production-style logic

The final universal analysis block is useful enough to become a standalone Python module. Keeping it only inside the notebook makes reuse and testing harder.

Recommended extraction:

- `src/cell_viability/inference.py`
- `src/cell_viability/metrics.py`
- `src/cell_viability/dataset.py`

### 2. Dataset conversion lacks automated tests

The COCO-to-YOLO conversion is central to the project and should have a small smoke test with synthetic annotations. This would catch coordinate conversion regressions without requiring the full dataset.

### 3. Runtime dependency installation inside notebook

The notebook installs dependencies through `subprocess` in the first cell. This is convenient in Kaggle, but less predictable in controlled environments.

Recommended approach:

- Keep `requirements.txt` as the primary dependency source.
- In the notebook, install only missing packages when running on Kaggle.
- Avoid silently changing package versions in a previously configured environment.

## Low-Risk Future Contributions

- Add `notebooks/` and move the notebook there when repository structure grows.
- Add a `src/` package for reusable inference and metric functions.
- Add a small CLI for batch inference:

```bash
python -m cell_viability.infer --weights best.pt --input images/ --conf 0.55
```

- Add a lightweight `tests/` suite for:
  - YOLO annotation conversion.
  - IoU calculation.
  - threshold metric calculation.
  - single-image inference path validation.

## Risk Notes

No scientific thresholds, model metrics, training parameters or notebook experiment logic were changed in this contribution. The applied changes are structural/documentation improvements intended to reduce user friction and accidental repository pollution.
