# PCA on African Energy Systems

Formative 2 (Advanced Linear Algebra) | PCA Pair Team 15, Cohort 2

This is our implementation of Principal Component Analysis (PCA), built from scratch with only numpy for the maths and matplotlib for the plots. We ran it on energy data for 54 African countries to see how far we can shrink 19 features down without losing much of the information.

## The data

We used the [Our World in Data energy dataset](https://github.com/owid/energy-data) (`data/owid-energy-data.csv`, commit `7e387a1`). The file covers the whole world and has 130 columns, so the notebook first keeps the 54 African countries for 2000-2022 (1,230 rows) and the columns we need.

It ticks all the boxes the assignment asked for:

- it's African and about something that matters (how countries produce and use energy)
- we end up with 19 features (15 numeric plus 4 for sub-region), well over the minimum of 7
- it has real missing values: 944 blank cells in the raw file (GDP, oil, gas and coal production)
- it has text columns (`country`, `iso_code`), and we added `sub_region` ourselves
- it isn't a generic dataset like house prices or wine quality

`data/DATA_DICTIONARY.md` explains what each column means and its unit.

## What we did

- **Task 1: PCA from scratch.** Standardization, covariance matrix, eigendecomposition, sorting the eigenvectors by their eigenvalues, and projecting the data. We check each step as we go (for example, the eigenvalues add up to exactly 19 and the eigenvectors are orthonormal).
- **Data handling.** We filled the missing oil, gas and coal values from each country's own years. Four countries have no GDP at all, so we used their sub-region median. We one-hot encoded the sub-region and log-transformed the heavily skewed columns.
- **Task 2: choosing the number of components.** k is picked from a variance threshold, not by hand. We explain the trade-off and what information is lost.
- **Task 3: performance.** We compared loops with vectorized code, float32 with float64, a chunked covariance and SVD, all the way up to 1,000,000 rows.

## What we found

- PC1 explains 34.1% of the variance. It's basically the size of a country's energy system: emissions, energy use, electricity demand and GDP all move together. North African countries score highest on it.
- PC2 explains 18.6%. It separates countries that make their electricity from fossil fuels from those that rely on hydro and other renewables.
- Seven components keep 90.0% of the variance, so we go from 19 features down to 7.
- What we lose is mostly fuel detail. Oil production, gas production and North Africa membership keep the least variance (about 75-76%).

## Running it

1. Open `PCA_African_Energy_Systems.ipynb` in Google Colab: [open in Colab](https://colab.research.google.com/github/nellybutera/pca-african-energy-systems/blob/main/PCA_African_Energy_Systems.ipynb). You can also download it and use **File > Upload notebook**.
2. Click **Runtime > Run all**. Every cell shows its output, including the plots.
3. You don't need to set anything else up. If the data file isn't next to the notebook, it downloads the exact version we used.

The analysis only uses `numpy` and `matplotlib`. We also use `os`, `urllib` and `time` from the standard library, just to download the data and time the benchmarks.

## What's in the repo

| File | What it is |
|---|---|
| `PCA_African_Energy_Systems.ipynb` | The completed notebook, with all outputs saved |
| `data/owid-energy-data.csv` | The raw data, untouched |
| `data/DATA_DICTIONARY.md` | What each column means |
| `figures/` | The plots used in the report |
| `BSE Group Assignments _ Task Sheet_Mathematics_for_Machine_Learning_Formative 2_PCA_Cohort 2_Team15.pdf` | Our task sheet as a PDF |
| `Task_Sheet_PCA_Formative_2_Pair15.xlsx` | Editable copy of the task sheet |

## Team

- **Peer pair:** Team 15, Cohort 2
- **Teta Butera Nelly:** dataset, data handling, the PCA code, plots, benchmarks and the repo setup
- **Mutoni Keira:** the written answers, the Colab check, the README results summary, the data dictionary and the first pull request

Report (Google Doc): https://docs.google.com/document/d/1TvoEBEaP3N5Y8YMTRxT0bt4rbs6NTB0w8B1O_IgAaA4/edit
Task sheet (Google Sheet): https://docs.google.com/spreadsheets/d/1kkgPBFFLvajCwub096beNw43_AatlmdXoaAnaC0QjMc/edit
