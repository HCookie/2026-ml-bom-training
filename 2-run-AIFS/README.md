# 2-run-AIFS: Running Pre-trained AIFS Inference

This section covers running inference with an existing AIFS checkpoint using the [anemoi-inference](https://anemoi-inference.readthedocs.io/en/latest/) package.

## Notebooks

| Notebook | Description |
|----------|-------------|
| [inference_aifs-ens.ipynb](inference_aifs-ens.ipynb) | Run ensemble inference from a pre-trained ENS checkpoint |
| [inference_aifs-single.ipynb](inference_aifs-ens.ipynb) | Run ensemble inference from a pre-trained Single checkpoint |

## Contents

```
2-run-AIFS/
├── inference_aifs-ens.ipynb     # Ensemble inference tutorial
├── inference_aifs-single.ipynb  # Single inference tutorial
├── command_line.md              # Command line documentation
└── helpers.py                   # Shared utility functions
```

## Running Inference

Open the notebook and follow the steps to:

1. Locate an ENS / SINGLE checkpoint
2. Inspect the checkpoint contents
3. Run ensemble inference with `anemoi-inference`
4. Visualise the forecast output

## Learning Objectives

By the end of this section you will:

- Know how to load and inspect a pre-trained ENS / SINGLE checkpoint
- Understand how to configure and run `anemoi-inference`
- Be able to generate and visualise ensemble forecasts

