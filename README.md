# A Resilient Mean-Field Game Framework for Autonomous Vehicle Coordination

This repository contains the official Python implementation for the paper: **"A Resilient Mean-Field Game Framework for Distributed Approximate Nash Equilibrium in Multi-Vehicle Systems under Attack."**

Our work introduces the **Resilient Mean-Field Game (R-MFG) framework**, a novel distributed control architecture designed to enable scalable, secure, and real-time coordination for multi-vehicle systems. This framework is robust against False Data Injection (FDI) attacks on V2X communication channels.

[![Paper PDF](https://img.shields.io/badge/Paper-PDF-red)](https://arxiv.org/abs/your_arxiv_id)  

 
_(<-- Optional: You can add a compelling figure from your paper here)_

## Key Features

- **Resilient Control**: Implements an Extended State Observer (ESO) to actively estimate and reject FDI attacks and other disturbances without needing a specific attack model.
- **Scalable by Design**: Leverages Mean-Field Game (MFG) theory to ensure that per-agent computation scales with local traffic density, not the total number of vehicles in the system.
- **Data-Driven Simulation**: Validated in a closed-loop environment using the real-world **nuScenes dataset**, where the agent interacts with actual, unpredictable human driving trajectories.
- **Modular Architecture**: The code is structured into clear, understandable modules:
    1.  **Resilient Mean-Field Perception**
    2.  **Dual-Layer Decision & Optimization** (MPC-based)
    3.  **State Execution**
- **Reproducible Scenarios**: Includes scripts to replicate all key experiments from the paper, including benign performance, resilience under attack, and scalability analysis.

## Getting Started

### Prerequisites

This project is developed in Python. We recommend using a `conda` environment to manage dependencies.

- Python 3.9+
- [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/) (Recommended)

### 1. Setting up the Environment

First, create and activate a new conda environment:

```bash
conda create -n r_mfg_env python=3.10
conda activate r_mfg_env
```

Next, install all the required packages using `pip`:

```bash
pip install numpy scipy matplotlib pyquaternion nuscenes-devkit descartes shapely
```

### 2. Downloading the nuScenes Dataset

Our simulation relies on the nuScenes dataset.

1.  Visit the [nuScenes download page](https://www.nuscenes.org/download).
2.  Download the **`v1.0-mini`** dataset.
3.  Download the **`v1.0 mini-maps`** expansion pack.
4.  Create a directory for your project, and place the unzipped `v1.0-mini` and `maps` folders inside it. Your project directory should look like this:

    ```
    /path/to/your/project/
    |
    ├── main_simulation.ipynb   <-- Your Jupyter Notebook
    ├── maps/
    │   ├── expansion/
    │   └── ...
    └── v1.0-mini/
        ├── samples/
        ├── sweeps/
        └── ...
    ```

### 3. Running the Simulation

1.  Open the `main_simulation.ipynb` (or your Python script) in a code editor or Jupyter Lab.
2.  **No path changes are needed** if your notebook is in the same directory as the `maps` and `v1.0-mini` folders, as the code uses `os.getcwd()` to find the data root automatically.
3.  Execute the cells in the notebook. The simulation will run through three scenarios:
    - **Scenario 1**: Baseline performance in a benign environment.
    - **Scenario 2**: Resilience test under FDI attack (comparing R-MFG vs. a naive baseline).
    - **Scenario 3**: Scalability analysis.

The results, including plots for each scenario, will be saved as PDF files in the project directory (e.g., `nu_scenario_1_baseline.pdf`).

## Code Structure

- **`main_simulation.ipynb`**: The main script that sets up and runs all experiments.
- **Part 1: R-MFG Algorithm Implementation**:
    - `ExtendedStateObserver`: Core class for disturbance estimation.
    - `ResilientPerceptionModule`: Perceives the environment and applies the ESO.
    - `DecisionModule`: Implements the MPC-based trajectory planner.
    - `RMfgAgent`: The main agent class that integrates all modules.
- **Part 2: Simulation Environment and Helper Functions**:
    - Contains functions for interacting with the nuScenes dataset, checking for collisions, and plotting results.
- **Part 3: Main Execution Block**:
    - Defines the experimental scenarios and orchestrates the simulation runs.
