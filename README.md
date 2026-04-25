# YOLOv8 Cell Viability Detection

![Python](https://img.shields.io/badge/python-v3.11+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-v2.6+-red.svg)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-green.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

Automated detection and classification of *Saccharomyces cerevisiae* cells with/without methylene blue staining using YOLOv8 deep learning.

## Key Results

- **Performance**: 94.4% mAP@0.5 (validation), 88.7% F1-Score (test)
- **Methodology**: Systematic framework with 5 optimization strategies
- **Key Finding**: Minimal augmentation proved more effective for microscopy
- **Reproducibility**: Complete code with deterministic controls

## About This Project

**Bachelor's Thesis (TCC)** - Electronic Engineering, UFSC 2025

**Objective**: Automate cell viability analysis traditionally performed manually, reducing subjectivity and increasing throughput.

**Context**: Specific application for *S. cerevisiae* + methylene blue in brightfield microscopy.

## Technologies

- **Deep Learning**: YOLOv8 (Ultralytics)
- **Framework**: PyTorch, Python 3.11
- **Environment**: Kaggle (Tesla P100)
- **Dataset**: 329 images, 4,930 cellular annotations

## Dataset Overview

- **Total**: 329 microscopic images (640×640px)
- **Classes**: COM_corante (dead cells) vs SEM_corante (viable cells)
- **Splits**: Train (233), Validation (64), Test (32)
- **Format**: COCO → YOLO conversion
- **Balance**: 46.2% vs 53.8% (adequate)

## Quick Start

### Prerequisites
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### Complete Implementation Structure
Execute `tcc_yolo_cell_detection.ipynb` sequentially - **11 comprehensive blocks:**

**Setup & Foundation:**
- **Setup**: Environment configuration and library imports
- **Block 1**: COCO dataset loading and exploratory analysis  
- **Block 2**: Data preparation (COCO→YOLO conversion + quality filters)

**Core Training & Evaluation:**
- **Block 3**: YOLOv8 baseline training and validation
- **Block 4**: YOLO detection visualization and analysis

**Advanced Optimization:**
- **Block 5**: Systematic optimization (5 strategies: baseline, fine-tuning, class weight, regularization, minimal augmentation)
- **Block 6**: Individual threshold optimization for all 5 trained models
- **Block 7**: Final results consolidation and tabular analysis

**Comprehensive Testing:**
- **Block 8**: Microscopic cell detection metrics analysis  
- **Block 9**: Robustness testing - Inference validation
- **Block 10**: Robustness testing - Multi-seed training validation

**Production System:**
- **Block 11**: Unified analysis system (automatic single image or batch processing)

### Key Features
- **Automated path detection** - Works with Kaggle or custom environments
- **Anti-leakage protocol** - Rigorous data splitting methodology  
- **Universal inference** - Single function handles images or folders
- **Deterministic training** - Reproducible results with seed control
- **Scientific metrics** - IoU, mAP@0.5, precision, recall, F1-Score

## Optimization Strategies Tested

The notebook implements 5 systematic optimization strategies:

| Strategy | Description | Key Features |
|----------|-------------|--------------|
| **Baseline** | Standard YOLOv8s | Reference model (90.8% mAP@0.5) |
| **Advanced Fine-tuning** | Reduced LR + regularization | Learning rate optimization |
| **High Class Weight** | Balanced class weighting | Focus on minority class |
| **High Regularization** | Dropout + weight decay | Overfitting prevention |
| **Minimal Augmentation** | Reduced transformations | **94.4% mAP@0.5** |

## Notebook Architecture

### Block-by-Block Structure
```
Setup Block: Environment + Dependencies    → Complete setup and imports
Block 1: Dataset Analysis                  → COCO loading + statistics  
Block 2: Data Preparation                  → COCO→YOLO + quality filters
Block 3: Baseline Training                 → YOLOv8s standard training
Block 4: Visualization                     → Results analysis + plots  
Block 5: Optimization                      → 5 systematic strategies
Block 6: Threshold Tuning                  → Individual model optimization
Block 7: Results Consolidation             → Final tabular analysis
Block 8: Metrics Analysis                  → Microscopy-specific metrics
Block 9: Inference Testing                 → Robustness validation
Block 10: Multi-seed Testing               → Training stability analysis
Block 11: Production System                → Universal inference API
```

## Reproducibility Notes

- The notebook metadata targets Python 3.11 and a Kaggle GPU runtime.
- The implementation uses fixed seeds for Python, NumPy and PyTorch.
- Dataset paths are optimized for Kaggle (`/kaggle/input/...` and `/kaggle/working/...`).
- Generated datasets, training runs and model weights are intentionally ignored by Git.
- The canonical notebook file is `tcc_yolo_cell_detection.ipynb`.

### Universal Inference System
```python
# Single image analysis
results = universal_analysis('path/to/image.jpg')

# Batch processing  
results = universal_analysis('path/to/folder/', conf_threshold=0.55)

# Custom parameters
results = universal_analysis('path/', conf_threshold=0.6, max_visualize=10)
```

## Key Discoveries

### Minimal Augmentation Insight
Reduced data augmentation outperformed conventional extensive transformations for microscopy, possibly due to preservation of specific morphological characteristics.

### Anti-Leakage Methodology
Rigorous data leakage prevention protocol:
- Chronological splits respected
- Test set isolated during development
- Deterministic seeds controlled

### Threshold Optimization
F1-Score based methodology (threshold=0.55) outperformed arbitrary values.

## Limitations

- **Specific scope**: Only *S. cerevisiae* + methylene blue
- **Small dataset**: 32-image test set (high variance)
- **Single modality**: Brightfield microscopy only
- **Academic context**: Limited undergraduate resources
- **Environment coupling**: Several notebook paths are currently Kaggle-specific

## Future Work

- Validation on larger datasets (>1000 images)
- Extension to other cell species
- Different staining techniques
- Laboratory GUI interface
- Comparison with other architectures
- Parameterize dataset/model paths for local execution outside Kaggle
- Export the production inference block to a standalone Python module
- Add smoke tests for dataset conversion and inference utilities

## Technical Audit

A detailed technical audit is available in [`AUDIT.md`](AUDIT.md), with prioritized bugs, maintainability improvements and low-risk contribution opportunities.

## Citation

```bibtex
@misc{tcc2025celldetection,
  title={Sistema Automatizado para Detecção e Classificação de Viabilidade Celular em Saccharomyces cerevisiae Utilizando YOLOv8},
  author={[João Henrique Anizelli Godoi]},
  year={2025},
  school={Universidade Federal de Santa Catarina},
  type={Trabalho de Conclusão de Curso},
  url={https://github.com/joaohanizelli/yolo-cell-viability-detection}
}
```

## Complete Documentation

Full thesis (Portuguese): https://repositorio.ufsc.br/handle/123456789/266740

## Contributing

This is an academic project, but suggestions and extensions are welcome!

## License

MIT License - Feel free to use for academic research.

---

**Developed as Bachelor's Thesis - Electronic Engineering, UFSC 2025**
