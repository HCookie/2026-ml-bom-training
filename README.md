# ECMWF - BOM Anemoi Training

This repo contains code examples and resources for use in the Anemoi training tutorial being run with the Australian Bureau of Meteorology.

## Repository Structure

```
2026-ml-bom-training/
├── 1-Anemoi/                        # Hands-on Anemoi training exercises
│   ├── configs/                     # Training configuration files (YAML)
│   ├── training_aifs-single.ipynb   # Train a deterministic AIFS model
│   ├── training_aifs-ens.ipynb      # Train an ensemble AIFS model
│   ├── inference_your_ckpt_o48.ipynb # Run inference on your own checkpoint
│   └── helpers.py
├── 2-run-AIFS/                      # Run pre-trained AIFS inference
│   ├── inference_aifs-ens.ipynb     # Ensemble inference notebook
│   └── helpers.py
├── Extra/                           # Optional supplementary exercises
│   ├── 1-ml-basics/                 # ML fundamentals with surface observations
│   ├── 2-model-debugging/           # Debugging CNNs with PyTorch
│   └── 3-graph-neural-networks/     # Graph neural network introduction
├── pyproject.toml                   # Project dependencies (managed by uv)
└── uv.lock                          # Locked dependency versions
```

## Setup

Dependencies are managed with [uv](https://docs.astral.sh/uv/).

### 1. Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Clone the repository

```bash
git clone <repo-url>
cd 2026-ml-bom-training
```

### 3. Create the virtual environment and install dependencies

```bash
uv sync
```

This will create a `.venv` directory and install all packages pinned in `uv.lock`, including PyTorch and the full Anemoi stack.

### 4. Activate the environment

```bash
source .venv/bin/activate
```

Or run commands directly without activating:

```bash
uv run jupyter notebook
ANEMOI_CONFIG=$PWD/configs uv run anemoi-training train --config-name=deterministic_minimal.yaml
```

### 5. Register the kernel with Jupyter

```bash
uv run python -m ipykernel install --user --name=bom-training --display-name "BOM Training"
```

Then select the **BOM Training** kernel when opening notebooks.

## Running the Notebooks

Launch JupyterLab from the repo root:

```bash
uv run jupyter lab
```

Navigate to the relevant section (`1-Anemoi/`, `2-run-AIFS/`, or `Extra/`) and open the notebook for your exercise.

## Training (1-Anemoi)

See [1-Anemoi/configs/README.md](1-Anemoi/configs/README.md) for full training instructions, including how to launch MLflow logging.

Quick start:

```bash
export ANEMOI_BASE_SEED=42
export ANEMOI_CONFIG=$PWD/configs
uv run anemoi-training train --config-name=deterministic_minimal.yaml
```
