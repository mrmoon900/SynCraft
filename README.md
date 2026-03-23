# SynCraft

[![Status](https://img.shields.io/badge/status-alpha-yellow.svg)](https://github.com/Q-Aljanabi/SynCraft)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Repo](https://img.shields.io/badge/repo-Q--Aljanabi%2FSynCraft-lightgrey.svg)](https://github.com/Q-Aljanabi/SynCraft)

A short tagline describing what SynCraft does (replace this with a one-line description).

## Table of Contents

- [About](#about)
-- [Data Availability](#data-availability)
- [Tech Stack](#tech-stack)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Related tools & implementations](#related-tools--implementations)
- [Development](#development)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## About

SynCraft is a concise description of the project — what problem it solves, who it's for, and a short summary of how it works. Replace this paragraph with a short overview and goals for the repository.

## Data Availability

The SynCraft web server is freely accessible at https://syncraft.denglab.org without registration. Complete source code, trained models, and documentation are available at https://drive.google.com/file/d/1WMW3ZnYv1jqVREd10l6nnwF2cDo10EBv/view?usp=sharing under the MIT License (public upon publication).

- Planned: additional features you intend to implement

## Tech Stack

List the primary languages, frameworks, and libraries used. Example placeholders:

- Language: JavaScript / Python / Rust / Go / TypeScript
- Framework: Node.js / Deno / Django / Flask / Actix / Rocket
- Build: npm, yarn, cargo, pip, mvn
- Other: Docker, GitHub Actions, etc.

(Replace with the actual stack used by SynCraft.)

## Requirements

Specify OS, runtime versions, and tools required. Example:

- Node.js >= 16 (if applicable)
- Python >= 3.10 (if applicable)
- Rust toolchain (if applicable)
- Docker (optional)
- Git

## Installation

Clone the repo and follow installation steps. Replace the commands below with ones appropriate for your project.

1. Clone the repository
```bash
git clone https://github.com/Q-Aljanabi/SynCraft.git
cd SynCraft
```

2. Install dependencies (example: Node.js)
```bash
# npm
npm install

# or yarn
yarn install
```

Example for Python projects:
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Example for Rust:
```bash
cargo build --release
```

## Usage

Give examples of how to run and use SynCraft. Include code snippets and expected outputs.

Command-line example:
```bash
# Run the main app (replace with real command)
npm start

# or
python -m src.main --input examples/input.json --output out/
```

Library / API example:
```python
from syncraft import Synthesizer

s = Synthesizer(config="configs/default.yaml")
result = s.run("input")
print(result)
```


**Datasets:**

- Retrosynthesis templates: USPTO-MIT dataset (479,035 reactions), https://github.com/wengong-jin/nips17-rexgen  
- ADMET training: MoleculeNet benchmarks, http://moleculenet.ai/  
- Building blocks: ZINC15, Enamine REAL, eMolecules  
- Validation: 1,000 ChEMBL drug-like molecules (MW 200–500) in Supplementary Data S1

**Reproducibility:** All experiments are reproducible using the provided scripts and conda environments. Requirements: NVIDIA GPU with ≥16GB VRAM for ADMET, 32GB RAM for retrosynthesis.

**Tutorials:** Interactive tutorials with examples (aspirin, caffeine, ibuprofen) are available at https://syncraft.denglab.org/tutorials.

## Related tools & implementations

- MolMVC — related repository: [Hhhzj-7/MolMVC](https://github.com/Hhhzj-7/MolMVC)  
- Retro* (Retro Star) — implementation of Retro*: Learning Retrosynthetic Planning with Neural Guided A* Search: [binghong-ml/retro_star](https://github.com/binghong-ml/retro_star)  
- SCScore (Coley et al., 2018) — Synthetic Complexity Score implementation and models: [connorcoley/scscore](https://github.com/connorcoley/scscore)  
- SA score (Ertl & Schuffenhauer, 2009) — common implementation available in RDKit: [rdkit/Contrib/SA_Score/sascorer.py](https://github.com/rdkit/rdkit/blob/master/Contrib/SA_Score/sascorer.py)

Include or reference these resources when you reuse scores, models, or code; respect their licenses and citations in publications.

## Development

Guidance for contributors to set up a development environment and the typical workflow.

- Create a feature branch: `git checkout -b feat/awesome`
- Run linters and formatters: e.g. `npm run lint` / `black .`
- Run the app locally and iterate

Suggested scripts (add to package.json or Makefile):
```json
{
  "scripts": {
    "start": "node ./src/index.js",
    "build": "tsc",
    "test": "jest",
    "lint": "eslint ."
  }
}
```

## Testing

Describe how to run tests and add new tests.

```bash
# Example: JavaScript
npm test

# Example: Python (pytest)
pytest tests/
```

## Contributing

Guidelines for contributing, code style, and PR process.

- Fork the repository
- Create a new branch for your change
- Make small, focused commits with clear messages
- Open a pull request against `main`
- Ensure tests pass and include/update documentation

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details. Replace with the correct license if different.

## Contact

Maintainer: Q-Aljanabi  
Repository: https://github.com/Q-Aljanabi/SynCraft

For feature requests or bug reports, please open an issue.

## Acknowledgements

- List libraries, tutorials, or people to thank
- Any third-party assets (icons, images) and their licenses
"""
Final Package Structure:

retrosynthesis/
├── **init**.py
├── **main**.py                  # CLI entry point
├── setup.py                     # Package setup
├── README.md
├── requirements.txt
├── config/
│   ├── **init**.py
│   └── settings.py              # Merged configuration
├── core/
│   ├── **init**.py
│   ├── molecules.py             # Chemical, Reaction classes
│   ├── templates.py             # Template handling
│   └── databases.py             # Commercial availability
├── search/
│   ├── **init**.py
│   ├── mcts.py                  # Monte Carlo Tree Search
│   ├── tree\_builder.py          # Tree building logic
│   └── orchestrator.py          # Main search orchestration
├── transformers/
│   ├── **init**.py
│   ├── template\_transformer.py  # Template-based transformations
│   ├── retro\_transformer.py     # Neural retrosynthesis
│   └── template\_extractor.py    # Template extraction
├── evaluation/
│   ├── **init**.py
│   ├── sa\_predictor.py          # Synthesis accessibility
│   ├── route\_evaluator.py       # Route quality evaluation
│   └── sc\_scorer.py             # SCScore implementation
├── utils/
│   ├── **init**.py
│   ├── rdkit\_utils.py           # RDKit utilities
│   ├── data\_processing.py       # Data preprocessing
│   ├── validation.py            # Input validation
│   └── helpers.py               # Common utilities
├── engines/
│   ├── **init**.py
│   ├── base\_engine.py           # Abstract base class
│   ├── retrosynthesis\_engine.py # Main engine
│   └── dlab\_syn\_engine.py  
├── data/
│   ├── models/
│   │   ├── best\_model.pth
│   │   └── model.ckpt-10654.as\_numpy.json.gz
│   ├── templates/
│   │   ├── retro\_templates.json.gz
│   │   └── forward.templates.json.gz
│   ├── scores/
│   │   ├── BRScores\_*.pkl.gz
│   │   └── BScores\_*.pkl.gz
│   └── reactions/
│       └── combined\_reactions120k.pkl.gz
└── tests/
├── **init**.py
├── test\_basic.py            # Basic functionality tests
├── test\_mcts.py             # MCTS algorithm tests
└── test\_evaluation.py       # Evaluation module tests
"""


