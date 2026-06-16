# Co-Trak: A Physically Constrained Inverse Reinforcement Learning Framework for Sim-to-Real Chassis Control Under Varying Friction

Companion repository for the paper **"Co-Trak: A Physically Constrained Inverse Reinforcement Learning Framework for Sim-to-Real Chassis Control Under Varying Friction"**, submitted to *Engineering Applications of Artificial Intelligence* (EAAI), 2026.

> **Author**: Hongxing Liu
> **Affiliation**: Southwest Jiaotong University (SWJTU)
> **Contact**: lhx@my.swjtu.edu.cn

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)

---

## About this repository

This repository hosts a **partial release** of materials accompanying the paper.
It is **not a full reimplementation**: only selected preprocessing /
postprocessing scripts and a subset of real-vehicle test data are made
publicly available. The core implementation of the Co-Trak framework is
withheld — please see the release policy below.

---

## What's in this repository

### Openly available

- **Preprocessing scripts** (selected) — utilities for preparing input data,
  scenario configuration files, and simulation initialization.
- **Postprocessing scripts** (selected) — evaluation metrics, trajectory
  analysis, and figure generation used in the paper.
- **Real-vehicle test data** (subset) — a portion of the on-road test data
  collected by the author during evaluation.

### Not publicly released

- The **core implementation** of the Co-Trak framework, including the
  inverse reinforcement learning training pipeline, reward network, policy
  network, and the safety-critical controller, is withheld due to ongoing
  follow-up research.
- The **full simulation datasets** and **trained model weights** are not
  released.
- The **remaining real-vehicle data**, part of which was provided by an
  industrial partner under a **non-disclosure agreement (NDA)**, cannot be
  shared publicly.

Access requests for non-commercial academic use can be directed to the
corresponding author and are subject to written approval from the data
owner where applicable.

---

## Repository structure

```
irl-vsc/
├── README.md                  ← this file
├── LICENSE                    ← MIT license for released code
├── DATA_LICENSE               ← terms for released datasets
├── requirements.txt           ← Python dependencies for released scripts
│
├── preprocessing/             ← released preprocessing utilities
│   ├── prepare_inputs.py
│   ├── scenario_config.py
│   └── README.md
│
├── postprocessing/            ← released evaluation & plotting scripts
│   ├── compute_metrics.py
│   ├── plot_trajectories.py
│   └── README.md
│
├── data/
│   ├── real_vehicle_subset/   ← released subset of real-vehicle test data
│   └── README.md              ← data documentation & schema
│
└── docs/                      ← extended documentation, figures
```

> **Note**: directories such as `src/`, `models/`, `scripts/train_*.py`, and
> the full `data/` content referenced in the paper are intentionally absent
> from this repository.

---

## Quick start

### 1. Clone the repository

```bash
git clone https://github.com/yubai-owner/irl-vsc.git
cd irl-vsc
```

### 2. Set up the environment

```bash
pip install -r requirements.txt
```

### 3. Run the released scripts

```bash
# Preprocessing example: prepare a scenario configuration
python preprocessing/scenario_config.py --friction 0.3 --output configs/example.yaml

# Postprocessing example: compute stability metrics on the released data subset
python postprocessing/compute_metrics.py \
       --data data/real_vehicle_subset/ \
       --output results/metrics.csv

# Postprocessing example: regenerate a paper figure
python postprocessing/plot_trajectories.py \
       --data data/real_vehicle_subset/ \
       --output results/figure.pdf
```

These scripts run independently and do **not** require the withheld core
implementation.

---

## License

- **Released code** (preprocessing / postprocessing scripts): [MIT License](LICENSE).
- **Released real-vehicle data subset**: [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). See [`DATA_LICENSE`](DATA_LICENSE) for details.
- **Withheld materials** (core implementation, full datasets, NDA-protected data): not part of this repository and not covered by the licenses above.

---

## Acknowledgements

We thank an industrial partner for providing experimental vehicle data under a
non-disclosure agreement.

---

## Contact

For questions regarding the released scripts or data subset, please open a
[GitHub issue](https://github.com/yubai-owner/irl-vsc/issues).

For collaboration, access requests, or other inquiries, please contact:
**Hongxing Liu** — lhx@my.swjtu.edu.cn
