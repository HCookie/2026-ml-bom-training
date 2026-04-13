# 1-Anemoi: Hands-on Anemoi Training

This section walks through training the AIFS (Artificial Intelligence Forecasting System) using the [Anemoi](https://anemoi.readthedocs.io/projects/training/en/latest/) framework. You will train both a deterministic (AIFS-Single) model and an ensemble (AIFS-ENS) model.

## Notebooks

| Notebook | Description |
|----------|-------------|
| [training_aifs-single.ipynb](training_aifs-single.ipynb) | Train a deterministic AIFS model using weighted MSE loss |
| [training_aifs-ens.ipynb](training_aifs-ens.ipynb) | Train an ensemble AIFS model using CRPS-based loss |

## Contents

```
1-Anemoi/
├── configs/                     # Anemoi training configuration files (YAML)
│   ├── deterministic_minimal.yaml
│   ├── aifs_ens_minimal.yaml
│   └── ...
├── _resources/                  # Images and supplementary assets
├── training_aifs-single.ipynb   # Deterministic training tutorial
├── training_aifs-ens.ipynb      # Ensemble CRPS training tutorial
└── helpers.py                   # Shared utility functions
```

## Running Training

See [configs/README.md](configs/README.md) for full training instructions, including MLflow logging setup.

Quick start:

```bash
export ANEMOI_BASE_SEED=42
export ANEMOI_CONFIG=$PWD/configs
uv run anemoi-training train --config-name=deterministic_minimal.yaml
```

For ensemble training:

```bash
uv run anemoi-training train --config-name=aifs_ens_minimal.yaml
```

## Learning Objectives

By the end of this section you will:

- Understand the key differences between deterministic and ensemble CRPS training
- Learn how to configure the Anemoi training pipeline
- Build a minimal training configuration step-by-step
- Execute a short training run and monitor it with MLflow
