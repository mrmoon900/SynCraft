# SynCraft

[![Status](https://img.shields.io/badge/status-alpha-yellow.svg)](https://github.com/Q-Aljanabi/SynCraft)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Web Server](https://img.shields.io/badge/web--server-live-brightgreen.svg)](https://syncraft.denglab.org)
[![Repo](https://img.shields.io/badge/repo-Q--Aljanabi%2FSynCraft-lightgrey.svg)](https://github.com/Q-Aljanabi/SynCraft)

**An integrated web server for retrosynthetic planning with real-time ADMET evaluation.**

---

## Table of Contents

- [About](#about)
- [Key Results](#key-results)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Data Availability](#data-availability)
- [Package Structure](#package-structure)
- [Related Tools & Implementations](#related-tools--implementations)
- [Development](#development)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

---

## About

Drug candidate attrition due to poor pharmacokinetics and genotoxic synthetic intermediates remains a critical bottleneck in pharmaceutical R&D. Current computational tools treat retrosynthetic planning and ADMET prediction as decoupled, sequential tasks, forcing medicinal chemists into time-consuming manual iteration cycles.

**SynCraft** is an integrated, registration-free web server that unifies template-based retrosynthesis with real-time, 3D-aware ADMET evaluation in a single platform. It leverages:

1. A library of **384,512 USPTO-derived reaction templates** searched via a breadth-first algorithm with real-time ADMET pruning.
2. The **MolMVC multi-view contrastive learning framework**, achieving 98.4% ROC-AUC on the ClinTox benchmark and outperforming established baselines across six MoleculeNet datasets.
3. A **unified workflow interface** that eliminates the manual file-export and tool-switching overhead of sequential pipelines.

SynCraft is free and open to all users with no login required: **[https://syncraft.denglab.org](https://syncraft.denglab.org)**

> **Source code & full package:** Available for download at [Google Drive (SynCraft-7.0.0.rar)](https://drive.google.com/file/d/1WMW3ZnYv1jqVREd10l6nnwF2cDo10EBv/view)

---

## Key Results

| Benchmark | Result |
|---|---|
| ClinTox ROC-AUC (MolMVC) | **98.4%** |
| Drug-like ChEMBL molecules solved (≤6 steps) | **71%** |
| Commercial building blocks linked | **22.4 million** |
| End-to-end analysis time (1,000-molecule benchmark) | **~42 s** (vs. ~161 s for sequential pipelines) |
| Reaction templates | **384,512** USPTO-derived |

Applied to **imatinib synthesis**, SynCraft automatically identifies and avoids ICH M7 Class 2 genotoxic intermediates that all five AiZynthFinder-generated routes converge upon.

---

## Features

- **Integrated retrosynthesis + ADMET** — template-based retrosynthetic planning with real-time ADMET pruning in a single workflow; no file export or tool switching required
- **MolMVC ADMET prediction** — multi-view contrastive learning achieving state-of-the-art performance across six MoleculeNet benchmarks
- **Genotoxicity-aware routing** — automatically detects and avoids ICH M7 genotoxic intermediates during route generation
- **Synthesis accessibility scoring** — SA score and SCScore to assess ease of synthesis
- **Drug-likeness evaluation** — Lipinski, QED, and related filters applied throughout the search
- **Molecular descriptors** — comprehensive physicochemical property calculation
- **3D-aware ADMET evaluation** — 3D molecular features integrated into property predictions
- **Interactive visualizations** — structure rendering, route trees, and property dashboards
- **Commercial building block linking** — routes linked to 22.4 million purchasable compounds from ZINC15, Enamine REAL, and eMolecules
- **No registration required** — fully open access at [syncraft.denglab.org](https://syncraft.denglab.org)

---

## Tech Stack

- **Language:** Python ≥ 3.8
- **Cheminformatics:** RDKit
- **Deep Learning:** PyTorch (MolMVC multi-view contrastive learning)
- **Search:** Breadth-first search with MCTS (Monte Carlo Tree Search)
- **Web Server:** Flask / Django (see `engines/`)
- **Data:** USPTO-MIT reaction templates, MoleculeNet benchmarks, ZINC15, Enamine REAL

---

## Requirements

- Python ≥ 3.8
- NVIDIA GPU with ≥ 16 GB VRAM (required for ADMET prediction)
- 32 GB RAM (required for retrosynthesis template search)
- Git
- Conda (recommended for environment management)

---

## Installation

### 1. Download the package

Clone the repository or download the full package from Google Drive:

Download the full package from Google Drive:

```bash
# Download from Google Drive
# https://drive.google.com/file/d/1WMW3ZnYv1jqVREd10l6nnwF2cDo10EBv/view
# Extract SynCraft-7.0.0.rar and enter the directory
cd SynCraft
```

### 2. Create and activate a conda environment

```bash
conda create -n syncraft python=3.8
conda activate syncraft
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Install RDKit

```bash
conda install -c conda-forge rdkit
```

---

## Usage

### Web Server

SynCraft is freely accessible online without registration:

**[https://syncraft.denglab.org](https://syncraft.denglab.org)**

Interactive tutorials with worked examples (aspirin, caffeine, ibuprofen) are available at [https://syncraft.denglab.org/tutorials](https://syncraft.denglab.org/tutorials).

### Command-line

```bash
# Run retrosynthesis on a target molecule (SMILES input)
python -m retrosynthesis.main --smiles "CC1=CC=C(C=C1)NC2=NC=CC(=N2)NC3=CC=CC(=C3)S(=O)(=O)N" --output results/

# Run with ADMET pruning enabled
python -m retrosynthesis.main --smiles "YOUR_SMILES" --admet --output results/
```

### Python API

```python
from retrosynthesis import Synthesizer

s = Synthesizer(config="config/settings.py")

# Run retrosynthesis with real-time ADMET evaluation
result = s.run(
    smiles="CC1=CC=C(C=C1)NC2=NC=CC(=N2)NC3=CC=CC(=C3)S(=O)(=O)N",  # Imatinib
    max_steps=6,
    admet_pruning=True
)

print(result.routes)         # Retrosynthetic routes
print(result.admet_scores)   # ADMET predictions per intermediate
print(result.sa_scores)      # Synthesis accessibility scores
print(result.sc_scores)      # SCScores
```

---

## Data Availability

The SynCraft web server is freely accessible at [https://syncraft.denglab.org](https://syncraft.denglab.org) without registration. Complete source code, trained models, and documentation are available at [https://github.com/denglab/syncraft](https://github.com/denglab/syncraft) under the MIT License.

**Datasets:**

| Dataset | Description | Source |
|---|---|---|
| USPTO-MIT | 479,035 reactions → 384,512 templates | [wengong-jin/nips17-rexgen](https://github.com/wengong-jin/nips17-rexgen) |
| MoleculeNet | ADMET training benchmarks (6 datasets) | [moleculenet.ai](http://moleculenet.ai/) |
| ZINC15 / Enamine REAL / eMolecules | 22.4M commercial building blocks | Various |
| ChEMBL validation set | 1,000 drug-like molecules (MW 200–500) | Supplementary Data S1 |

**Reproducibility:** All experiments are reproducible using the provided scripts and conda environments.
- ADMET models require: NVIDIA GPU with ≥ 16 GB VRAM
- Retrosynthesis templates require: 32 GB RAM

---

## Package Structure

```
retrosynthesis/
├── __init__.py
├── __main__.py                  # CLI entry point
├── setup.py                     # Package setup
├── README.md
├── requirements.txt
├── config/
│   ├── __init__.py
│   └── settings.py              # Merged configuration
├── core/
│   ├── __init__.py
│   ├── molecules.py             # Chemical, Reaction classes
│   ├── templates.py             # Template handling
│   └── databases.py             # Commercial availability
├── search/
│   ├── __init__.py
│   ├── mcts.py                  # Monte Carlo Tree Search
│   ├── tree_builder.py          # Tree building logic
│   └── orchestrator.py          # Main search orchestration
├── transformers/
│   ├── __init__.py
│   ├── template_transformer.py  # Template-based transformations
│   ├── retro_transformer.py     # Neural retrosynthesis
│   └── template_extractor.py   # Template extraction
├── evaluation/
│   ├── __init__.py
│   ├── sa_predictor.py          # Synthesis accessibility (SA score)
│   ├── route_evaluator.py       # Route quality evaluation
│   └── sc_scorer.py             # SCScore implementation
├── utils/
│   ├── __init__.py
│   ├── rdkit_utils.py           # RDKit utilities
│   ├── data_processing.py       # Data preprocessing
│   ├── validation.py            # Input validation
│   └── helpers.py               # Common utilities
├── engines/
│   ├── __init__.py
│   ├── base_engine.py           # Abstract base class
│   ├── retrosynthesis_engine.py # Main engine
│   └── dlab_syn_engine.py       # DengLab synthesis engine
├── data/
│   ├── models/
│   │   ├── best_model.pth
│   │   └── model.ckpt-10654.as_numpy.json.gz
│   ├── templates/
│   │   ├── retro_templates.json.gz
│   │   └── forward.templates.json.gz
│   ├── scores/
│   │   ├── BRScores_*.pkl.gz
│   │   └── BScores_*.pkl.gz
│   └── reactions/
│       └── combined_reactions120k.pkl.gz
└── tests/
    ├── __init__.py
    ├── test_basic.py            # Basic functionality tests
    ├── test_mcts.py             # MCTS algorithm tests
    └── test_evaluation.py       # Evaluation module tests
```

---

## Related Tools & Implementations

The following tools and implementations are used or referenced within SynCraft. Please cite them appropriately in publications and respect their licenses.

- **MolMVC** — Multi-view contrastive learning for molecular property prediction: [Hhhzj-7/MolMVC](https://github.com/Hhhzj-7/MolMVC)
- **Retro\*** — Retrosynthetic planning with neural-guided A\* search: [binghong-ml/retro_star](https://github.com/binghong-ml/retro_star)
- **SCScore** (Coley et al., 2018) — Synthetic complexity score: [connorcoley/scscore](https://github.com/connorcoley/scscore)
- **SA Score** (Ertl & Schuffenhauer, 2009) — Synthesis accessibility score: [rdkit/Contrib/SA_Score/sascorer.py](https://github.com/rdkit/rdkit/blob/master/Contrib/SA_Score/sascorer.py)
- **AiZynthFinder** — Computer-assisted retrosynthesis tool for benchmarking comparison
- **USPTO-MIT dataset** — Reaction template source: [wengong-jin/nips17-rexgen](https://github.com/wengong-jin/nips17-rexgen)
- **MoleculeNet** — ADMET benchmark datasets: [moleculenet.ai](http://moleculenet.ai/)

---

## Development

```bash
# Create a feature branch
git checkout -b feat/your-feature

# Format code
black .

# Lint
flake8 retrosynthesis/

# Run locally
python -m retrosynthesis.main --smiles "CCO" --output out/
```

---

## Testing

```bash
# Run all tests
pytest tests/

# Run specific module tests
pytest tests/test_mcts.py
pytest tests/test_evaluation.py
```

---

## Contributing

- Fork the repository
- Create a new branch for your change (`git checkout -b feat/your-feature`)
- Make small, focused commits with clear messages
- Open a pull request against `main`
- Ensure all tests pass and update documentation as needed

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## Contact

**Maintainer:** Q-Aljanabi
**Repository:** [https://github.com/Q-Aljanabi/SynCraft](https://github.com/Q-Aljanabi/SynCraft)
**Web Server:** [https://syncraft.denglab.org](https://syncraft.denglab.org)

For feature requests or bug reports, please [open an issue](https://github.com/Q-Aljanabi/SynCraft/issues).

---

## Acknowledgements

- [MolMVC](https://github.com/Hhhzj-7/MolMVC) — multi-view contrastive learning framework
- [RDKit](https://www.rdkit.org/) — cheminformatics toolkit
- [MoleculeNet](http://moleculenet.ai/) — benchmark datasets
- [USPTO-MIT](https://github.com/wengong-jin/nips17-rexgen) — reaction template dataset
- [SCScore](https://github.com/connorcoley/scscore) and [SA Score](https://github.com/rdkit/rdkit/blob/master/Contrib/SA_Score/sascorer.py) — synthesis scoring tools
- DengLab for hosting the web server
