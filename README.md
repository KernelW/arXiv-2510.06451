# arXiv-2510.06451

## System requirements
This project uses **Python 3** and has been tested on **Apple Silicon (M2) with 16 GB memory**.

Typical runtimes:
- **Installation time (pip):** ~ **2–6 minutes** (network dependent).
- **Notebook runtime:** each Jupyter notebook completes in **≤ 10 minutes** on an **M2 (16 GB RAM)**.

## Installation (pip)
Create and activate a Python environment (recommended), then install dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install numpy scipy matplotlib jupyter
```
## How to run
Open a notebook and click **Kernel → Restart & Run All**.

## Outputs
Generated data and figures are saved in the output directories specified inside each notebook.

## Data Generation
The datasets for this project are generated using the Jupyter notebooks located in the `/Data_Generation` directory.

### 1. Form Factor Generation
* **`Lambda_Matrix_Generate.ipynb`** Running this notebook generates the Lambda-matrix (form factors) used in the paper. It performs two primary functions:
    * **BM Model Definition:** Implements the Bistritzer-MacDonald (BM) model for Twisted Bilayer Graphene (TBG) with tunable parameters ($w_0, w_1$, and twist angle). These are located in the first block; search for `TBG_Parameter` to adjust them.
    * **Pair Momentum Calculation:** Defines and stores the particle-particle form factors at a specific pair momentum (e.g., the M-point). This is located in the second block; search for `Loc: COM_Tune` to modify the pairing momentum.

### 2. Symmetry Channel Construction
* **`read_Lambda_Construct_triplet.ipynb`** Constructs the Lambda-matrix for the triplet channel. By default, it processes the $A$-symmetry channel (`sym=0`). To generate the $E_1$ and $E_2$ channels, search for `loc_sym` and update the symmetry indices (e.g., `syms=(0,1,2)`).
* **`read_Lambda_Construct_singlet.ipynb`** Constructs the Lambda-matrix for the singlet channel ($A$-symmetry, `sym=0`). Similarly, search for `loc_sym` to include other symmetry channels.

---

## Solving Gap Equations
Once the singlet and triplet form factors are stored, use the following notebooks to solve the gap equations:

* **`Solvegrand_singlet.ipynb`** Solves the gap equation within the **grand-canonical ensemble**.
    * **Configuration:** Switch between singlet and triplet solutions by changing `flat_dir` (e.g., from `"lambda_singlet"` to `"lambda_triplet"`).
    * **Parameters:** Tunable variables include the symmetry channel, temperature ($T$), subspace dimension, and interaction strength.
* **`Solve_singlet.ipynb`** Solves the gap equation within the **canonical ensemble**.

---

## Figure Reproduction
Notebooks for reproducing the main-text figures (Figs. 2–6) are located in the `/figures` directory. Ensure the data generation steps above are completed before running these.

* **Fig. 2 (`fig2.ipynb`):** Plots the BM band dispersion and form factors. Requires data from `Lambda_Matrix_Generate.ipynb` and `read_Lambda_Construct_triplet.ipynb`.
* **Fig. 3 (`fig3.ipynb`):** Compares singlet and triplet solutions. While baseline data is included, you can use the `Solvegrand` notebooks to generate custom datasets.
* **Fig. 4 (`fig4.ipynb`):** Displays results for the gap equation solved in the canonical ensemble.
* **Fig. 5 (`fig5.ipynb`):** Generates Density of States (DOS) plots and two Bogoliubov-de Gennes (BdG) dispersions.
* **Fig. 6 (`preparation_fig6.ipynb` & `fig6.ipynb`):** Calculates and plots zero-bias conductance. **Note:** Run `preparation_fig6.ipynb` first to process the data before executing `fig6.ipynb`.
