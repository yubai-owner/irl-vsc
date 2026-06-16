# irl-vsc
vehicle sensor data &amp; model

# Co-Trak: A Physically Constrained Inverse Reinforcement Learning Framework for Sim-to-Real Chassis Control Under Varying Friction

Official implementation of the paper **"Co-Trak: A Physically Constrained Inverse Reinforcement Learning Framework for Sim-to-Real Chassis Control Under Varying Friction"**, submitted to *Engineering Applications of Artificial Intelligence* (EAAI), 2026.

> **Author**: Hongxing Liu
> **Affiliation**: Southwest Jiaotong University (SWJTU)
> **Contact**: lhx@my.swjtu.edu.cn

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)

---

## TL;DR

This repository contains the implementation, trained models, and reproduction
scripts for **Co-Trak**, a physically constrained inverse reinforcement learning
(IRL) framework for sim-to-real chassis control of autonomous vehicles operating
under varying road friction conditions.

---

## What's in this repository (tiered availability)

This project follows a **tiered data and code release policy** consistent with
the Data Availability Statement of the published paper.

### Openly available (in this repository)

- **Self-generated simulation datasets** — driving scenarios constructed by
  the author in CarSim / CARLA / MATLAB-Simulink, covering low-friction,
  sharp-curve, and varied-adhesion conditions.
- **Trained models and parameters** — IRL reward networks, policy networks,
  and all hyperparameters reported in the paper.
- **Core implementation** — reward learning module, controller architecture,
  CBF/MPC safety layer, evaluation pipeline, and reproduction scripts.

### Partially released (intentionally withheld)

Some auxiliary modules related to **ongoing follow-up research** are not
included in the public release. The omitted parts are not required to
reproduce any result reported in the paper. If you need access for
non-commercial academic use, please contact the corresponding author.

### Restricted access (NDA-protected)

A subset of the vehicle dynamics data used for evaluation was provided by an
industrial partner under a **non-disclosure agreement (NDA)** and **cannot be
shared publicly**. Access requests can be directed to the corresponding
author and are subject to written approval from the data owner.

---

## Repository structure

```
co-trak/
├── README.md                  ← this file
├── LICENSE                    ← MIT license for code
├── DATA_LICENSE               ← terms for released datasets
├── requirements.txt           ← Python dependencies
├── environment.yml            ← Conda environment (optional)
│
├── src/                       ← core source code
│   ├── irl/                     ← inverse reinforcement learning module
│   ├── controller/              ← safety-critical controller (CBF/MPC layer)
│   ├── vehicle_model/           ← vehicle dynamics & tire model
│   ├── envs/                    ← simulation environments
│   └── utils/                   ← logging, plotting, helpers
│
├── data/
│   ├── simulation/              ← self-generated simulation datasets
│   ├── demonstrations/          ← expert driving demonstrations
│   └── README.md                ← data documentation
│
├── models/                    ← pretrained reward & policy networks
│   ├── reward_net.pt
│   ├── policy_net.pt
│   └── config.yaml
│
├── scripts/
│   ├── train_irl.py             ← train reward model from demonstrations
│   ├── train_policy.py          ← train policy with learned reward
│   ├── evaluate.py              ← run evaluation on test scenarios
│   └── reproduce_paper.sh       ← one-shot reproduction of paper results
│
├── configs/                   ← experiment configuration files
│   ├── low_friction.yaml
│   ├── sharp_curve.yaml
│   └── nominal.yaml
│
├── notebooks/                 ← analysis and visualization notebooks
│
└── docs/                      ← extended documentation, figures, supplementary
```

---

## Quick start

### 1. Clone the repository

```bash
git clone https://github.com/yubai/co-trak.git
cd co-trak
```

### 2. Set up the environment

```bash
# Option A: pip
pip install -r requirements.txt

# Option B: conda
conda env create -f environment.yml
conda activate co-trak
```

### 3. Run a minimal example

```bash
python scripts/evaluate.py --config configs/low_friction.yaml \
                           --model models/policy_net.pt
```

This loads the pretrained policy and evaluates it on a low-friction scenario.
Results (trajectories, control signals, stability metrics) are saved to
`results/`.

---

## Reproducing the experiments in the paper

To reproduce **all** experimental results reported in the paper:

```bash
bash scripts/reproduce_paper.sh
```

This script:
1. Loads the released expert demonstrations from `data/demonstrations/`.
2. Re-trains the IRL reward model (skip with `--use-pretrained`).
3. Trains the policy under three driving conditions.
4. Evaluates on the released test scenarios and produces all paper figures
   in `results/figures/`.

Expected runtime on a single NVIDIA RTX 4090: **~6 hours** for full retraining,
or **~15 minutes** when using the pretrained models.

> **Note**: Results involving the NDA-protected industrial dataset cannot be
> reproduced with this repository alone. The released simulation results
> independently verify all qualitative and quantitative claims.

---

## Pretrained models

| Model | File | Description |
|---|---|---|
| IRL reward network | `models/reward_net.pt` | Learned from expert demonstrations |
| Stability-aware policy | `models/policy_net.pt` | Final policy used in the paper |
| Safety filter parameters | `models/cbf_params.yaml` | CBF / MPC safety layer config |

All models were trained with the configurations under `configs/`.

---

## License

- **Code**: released under the [MIT License](LICENSE).
- **Released datasets and trained models**: released under the
  [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
  license. See [`DATA_LICENSE`](DATA_LICENSE) for details.
- **NDA-protected industrial data**: not part of this repository.

---

## Acknowledgements

We thank an industrial partner for providing experimental vehicle data under a
non-disclosure agreement.

---

## Contact

For questions regarding the code, please open a [GitHub issue](https://github.com/yubai/co-trak/issues).

For collaboration, data access requests, or other inquiries, please contact:
**Hongxing Liu** — lhx@my.swjtu.edu.cn
