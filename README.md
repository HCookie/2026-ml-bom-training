# ECMWF - BOM Anemoi Training

This repo contains code examples and resources for use in the Anemoi training tutorial being run with the Australian Bureau of Meteorology.

## Repository Structure

```
2026-ml-bom-training/
├── 1-Anemoi/                        # Hands-on Anemoi training exercises
│   ├── configs/                     # Training configuration files (YAML)
│   ├── training_aifs-single.ipynb   # Train a deterministic AIFS model
│   ├── training_aifs-ens.ipynb      # Train an ensemble AIFS model
│   └── helpers.py
├── 2-run-AIFS/                      # Run pre-trained AIFS inference
│   ├── inference_aifs-ens.ipynb     # Ensemble inference notebook
│   ├── inference_aifs-single.ipynb  # Single inference notebook
│   └── helpers.py
├── Extra/                           # Optional supplementary exercises
│   ├── 1-ml-basics/                 # ML fundamentals with surface observations
│   ├── 2-model-debugging/           # Debugging CNNs with PyTorch
│   └── 3-graph-neural-networks/     # Graph neural network introduction
├── pyproject.toml                   # Project dependencies (managed by uv)
└── uv.lock                          # Locked dependency versions
```

## Clone the repository

```bash
git clone <repo-url>
cd 2026-ml-bom-training
```

## Setup with ARE

Log into [ARE](https://are.nci.org.au/)

### 1. Create a jupyterlab session

Create a jupyterlab session with the following compute setup

- Queue: gpuvolta
- Compute Size: 1gpu
- Project: Use your own
- Storage: gdata/ma14+scratch/ma14+gdata/dk92+scratch/dk92+scratch/YOUR_OWN+gdata/YOUR_OWN

### 2. Configure module

Use the dk92 module

- Module directories: /g/data/dk92/apps/Modules/modulefiles
- Modules: anemoi/26.04

### 3. Launch the job

Launch the session, and wait for the allocation


### Running the Notebooks

Navigate to the location you cloned the repo within the ARE session and navigate to the relevant section (`1-Anemoi/`, `2-run-AIFS/`, or `Extra/`) and open the notebook for your exercise.

## Setup with uv

Dependencies are managed with [uv](https://docs.astral.sh/uv/).

### 1. Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Create the virtual environment and install dependencies

```bash
uv sync
```

This will create a `.venv` directory and install all packages pinned in `uv.lock`, including PyTorch and the full Anemoi stack.

### 3. Activate the environment

```bash
source .venv/bin/activate
```

Or run commands directly without activating:

```bash
uv run jupyter notebook
ANEMOI_CONFIG=$PWD/configs uv run anemoi-training train --config-name=deterministic_minimal.yaml
```

### 4. Register the kernel with Jupyter

```bash
uv run python -m ipykernel install --user --name=bom-training --display-name "BOM Training"
```

Then select the **BOM Training** kernel when opening notebooks.

### Running the Notebooks

Launch JupyterLab from the repo root:

```bash
uv run jupyter lab
```

Navigate to the relevant section (`1-Anemoi/`, `2-run-AIFS/`, or `Extra/`) and open the notebook for your exercise.
