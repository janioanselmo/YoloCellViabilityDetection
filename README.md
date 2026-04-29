# YOLOv8 Cell Viability Detection

![Python](https://img.shields.io/badge/python-v3.11+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-v2.6+-red.svg)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-green.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 🇧🇷 PT-BR

Detecção e classificação automatizada de células de *Saccharomyces cerevisiae* com e sem coloração por azul de metileno usando deep learning com YOLOv8.

### Visão Geral

Este projeto foi desenvolvido como Trabalho de Conclusão de Curso em Engenharia Eletrônica na UFSC em 2025. O objetivo é automatizar a análise de viabilidade celular tradicionalmente feita de forma manual, reduzindo subjetividade e aumentando produtividade.

### Resultados Principais

- **Desempenho:** 94,4% mAP@0.5 em validação e 88,7% F1-Score em teste.
- **Metodologia:** estrutura sistemática com 5 estratégias de otimização.
- **Achado principal:** augmentação mínima foi mais efetiva para microscopia.
- **Reprodutibilidade:** notebook completo com controles determinísticos.

### Tecnologias

- YOLOv8 / Ultralytics.
- PyTorch.
- Python 3.11.
- Ambiente Kaggle com GPU Tesla P100.
- Dataset com 329 imagens e 4.930 anotações celulares.

### Estrutura

| Arquivo | Descrição |
| --- | --- |
| `tcc_yolo_cell_detection.ipynb` | Notebook principal com preparação, treinamento, avaliação e inferência |
| `requirements.txt` | Dependências Python |
| `AUDIT.md` | Auditoria técnica com riscos e melhorias |
| `LICENSE` | Licença MIT |

### Como Executar

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

No Windows:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Execute o notebook `tcc_yolo_cell_detection.ipynb` sequencialmente.

### Arquitetura do Notebook

- Setup: ambiente, dependências e imports.
- Bloco 1: análise exploratória do dataset COCO.
- Bloco 2: preparação de dados e conversão COCO para YOLO.
- Bloco 3: treinamento baseline YOLOv8.
- Bloco 4: visualização e análise de detecções.
- Bloco 5: otimização sistemática com 5 estratégias.
- Bloco 6: ajuste de thresholds por modelo.
- Bloco 7: consolidação de resultados.
- Bloco 8: métricas específicas de microscopia.
- Bloco 9: testes de inferência.
- Bloco 10: validação multi-seed.
- Bloco 11: sistema de análise unificado.

### Sistema de Inferência

```python
results = universal_analysis("path/to/image.jpg")
results = universal_analysis("path/to/folder/", conf_threshold=0.55)
results = universal_analysis("path/", conf_threshold=0.6, max_visualize=10)
```

### Limitações

- Escopo específico para *S. cerevisiae* com azul de metileno.
- Dataset pequeno no conjunto de teste.
- Modalidade única: microscopia brightfield.
- Alguns caminhos do notebook são específicos do Kaggle.

### Trabalhos Futuros

- Validar com datasets maiores.
- Estender para outras espécies celulares.
- Testar diferentes técnicas de coloração.
- Criar interface laboratorial.
- Comparar com outras arquiteturas.
- Exportar o bloco de inferência para módulo Python independente.

### Auditoria Técnica

Consulte [`AUDIT.md`](AUDIT.md) para bugs priorizados, melhorias de manutenção e oportunidades de contribuição.

### Citação

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

### Licença

MIT License. Consulte `LICENSE`.

---

## 🇺🇸 English

Automated detection and classification of *Saccharomyces cerevisiae* cells with and without methylene blue staining using YOLOv8 deep learning.

### Overview

This project was developed as a Bachelor's Thesis in Electronic Engineering at UFSC in 2025. The goal is to automate cell viability analysis traditionally performed manually, reducing subjectivity and increasing throughput.

### Key Results

- **Performance:** 94.4% mAP@0.5 on validation and 88.7% F1-Score on test.
- **Methodology:** systematic framework with 5 optimization strategies.
- **Key finding:** minimal augmentation was more effective for microscopy.
- **Reproducibility:** complete notebook with deterministic controls.

### Technologies

- YOLOv8 / Ultralytics.
- PyTorch.
- Python 3.11.
- Kaggle environment with Tesla P100 GPU.
- Dataset with 329 images and 4,930 cellular annotations.

### Structure

| File | Description |
| --- | --- |
| `tcc_yolo_cell_detection.ipynb` | Main notebook with preparation, training, evaluation and inference |
| `requirements.txt` | Python dependencies |
| `AUDIT.md` | Technical audit with risks and improvements |
| `LICENSE` | MIT license |

### How to Run

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

On Windows:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Run `tcc_yolo_cell_detection.ipynb` sequentially.

### Notebook Architecture

- Setup: environment, dependencies and imports.
- Block 1: COCO dataset exploratory analysis.
- Block 2: data preparation and COCO to YOLO conversion.
- Block 3: YOLOv8 baseline training.
- Block 4: detection visualization and analysis.
- Block 5: systematic optimization with 5 strategies.
- Block 6: per-model threshold tuning.
- Block 7: final results consolidation.
- Block 8: microscopy-specific metrics.
- Block 9: inference testing.
- Block 10: multi-seed validation.
- Block 11: unified analysis system.

### Inference System

```python
results = universal_analysis("path/to/image.jpg")
results = universal_analysis("path/to/folder/", conf_threshold=0.55)
results = universal_analysis("path/", conf_threshold=0.6, max_visualize=10)
```

### Limitations

- Specific scope for *S. cerevisiae* with methylene blue.
- Small test dataset.
- Single modality: brightfield microscopy.
- Some notebook paths are Kaggle-specific.

### Future Work

- Validate on larger datasets.
- Extend to other cell species.
- Test different staining techniques.
- Create a laboratory GUI.
- Compare with other architectures.
- Export inference block to a standalone Python module.

### Technical Audit

See [`AUDIT.md`](AUDIT.md) for prioritized bugs, maintainability improvements and contribution opportunities.

### Citation

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

### License

MIT License. See `LICENSE`.
