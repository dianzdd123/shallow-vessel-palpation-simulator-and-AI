# Reuse guide — shallow-vessel-palpation-simulator-and-AI

[README](../README.md) · [Dandan Zhang’s fork](https://github.com/dianzdd123/shallow-vessel-palpation-simulator-and-AI) · [MSEI Lab](https://zhangrobotics.com/msei_website/)

## Get this copy

```bash
git clone https://github.com/dianzdd123/shallow-vessel-palpation-simulator-and-AI.git
cd shallow-vessel-palpation-simulator-and-AI
```

## Choose the right entry point

This is the simulation, dataset and learning side of the shallow-vessel palpation project. Use it to work with the released data and reproduce analyses without a robot. The [robot-control companion](https://github.com/dianzdd123/shallow-vessel-palpation-robot-control) is for new physical data collection.

| Area | Purpose |
|---|---|
| `docker/` | Supported runtime and user-facing launch scripts |
| `difftactile/scripts/` | Thin Python wrappers for pipeline stages |
| `difftactile/main/` | Taichi FEM simulation and domain adaptation |
| `difftactile/cnn/` | GNN datasets, training, evaluation and prediction inspection |
| `difftactile/data_analysis/` | Real marker tracking, calibration and analysis |
| `difftactile/system_params/` | Experiment configuration |
| `data/MANIFEST.md` | External bundle contents and restoration information |
| `analysis/` | Poster analyses, figures and reports |

## Environment and data

**Docker is the supported execution route.** Follow the complete Docker quickstart in the [README](../README.md). It specifies a Linux NVIDIA host, Docker, NVIDIA Container Toolkit and the pinned CUDA/Taichi/Torch/PyG stack. Display forwarding is needed for interactive viewers. Bare-metal installation is not validated by this maintenance pass.

The dataset, checkpoints and result assets are provided separately through the Zenodo bundle linked in the README and [data manifest](../data/MANIFEST.md). Download and restore that bundle before the pipeline's data check. The DOI identifies the upstream archived release; it does not identify later commits in this fork.

## Working sequence

1. Clone this fork, fetch the data bundle and build/start the Docker environment using the README commands.
2. Run the provided GPU/dependency/data validation inside the container.
3. Begin with the existing evaluation workflow and released checkpoints. Use the README's script-to-figure/table mapping to choose the desired result.
4. Run training, domain adaptation or data generation only after inspecting the relevant JSON configuration and output location.
5. For new simulated data, preserve the marker ordering and the documented Hungarian-reordering stage before GNN consumption.

Use the entrypoint wrappers rather than importing large simulation modules into ad hoc scripts. GUI imports are deliberately delayed in some modules; preserve that behaviour when modifying headless code.

## Reproducibility and outputs

Keep the commit SHA, container image/build details, bundle DOI/version, configuration JSON, random seeds and output tables together. Configuration determines where generated data and results are written. Preserve the released results when generating new runs. The README documents modelling assumptions, calibration/domain-randomisation distinctions and known limitations; those qualify comparisons to the manuscript.

## Validation scope

The added CI job checks source and documentation structure without starting Docker, Taichi, Qt, GPU training or simulator execution. The upstream numerical and experimental claims were not remeasured in this pass. Existing engineering notes and all simulation/control algorithms are retained.

## Local quality checks

Run `python scripts/check_repository.py` from a Git checkout with Python 3.10+ and Git installed. It parses Python, JSON/notebook containers and links in the navigation documents without importing research modules. Notebook cells and remote links are not executed or tested.

## Attribution and reuse terms

This is a fork of [piotr-blaszyk/shallow-vessel-palpation-simulator-and-AI](https://github.com/piotr-blaszyk/shallow-vessel-palpation-simulator-and-AI). Original paper authorship, upstream citations and notices remain authoritative. Cite the associated work and identify this fork’s commit when reporting modifications.

The root [LICENSE](../LICENSE) contains MIT terms. Preserve its notices and inspect separately supplied data, models and third-party components for their own terms.
