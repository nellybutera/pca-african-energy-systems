# PCA on African Energy Systems

Formative 2 (Advanced Linear Algebra) | PCA Pair Team 15, Cohort 2

This is our PCA project. We wrote PCA from scratch (numpy for the maths, matplotlib for the plots) and ran it on energy data for 54 African countries, to see how far we could shrink 19 features without losing much information.

## The data

We used the [Our World in Data energy dataset](https://github.com/owid/energy-data) (`data/owid-energy-data.csv`, commit `7e387a1`). It covers the whole world with 130 columns, so the notebook starts by keeping only the 54 African countries for 2000-2022 (1,230 rows) and the columns we need.

It ticks everything the assignment asked for:

- it's African, and about something that matters (how countries make and use energy)
- we end up with 19 features (15 numeric plus 4 for sub-region), well above the minimum of 7
- it has real missing values: 944 blank cells in the raw file (GDP, oil, gas and coal production)
- it has text columns (`country`, `iso_code`), plus a `sub_region` column we added
- it's not a generic dataset like house prices or wine quality

`data/DATA_DICTIONARY.md` explains what each column is and its unit.

## What we did

- **Task 1, PCA from scratch.** Standardization, covariance matrix, eigendecomposition, sorting the eigenvectors and projecting the data. We check each step as we go, for example the eigenvalues add up to exactly 19 and the eigenvectors are orthonormal.
- **Data handling.** We filled the missing oil, gas and coal values from each country's own years. Four countries have no GDP at all, so they got their sub-region median. Sub-region is one-hot encoded, and the very skewed columns are log-transformed.
- **Task 2, number of components.** We pick k from a variance threshold instead of by hand, and explain the trade-off and what gets lost.
- **Task 3, performance.** We compared loops with vectorized code, float32 with float64, a chunked covariance and SVD, all the way up to 1,000,000 rows.

## What we found

- PC1 explains 34.1% of the variance. It's mostly the size of a country's energy system: emissions, energy use, electricity demand and GDP all move together, and North African countries score highest.
- PC2 explains 18.6%. It splits countries that make electricity from fossil fuels from the ones that rely on hydro and other renewables.
- Seven components keep 90.0% of the variance, so 19 features become 7.
- What we lose is mostly fuel detail. Oil production, gas production and being in North Africa keep the least variance (around 75-76%).

## Libraries used

- NumPy (computation)
- Matplotlib (plots)
- `os`, `urllib` and `time` from the standard library, only to download the data and time the benchmarks

## Running it

1. Open the notebook in Colab: [open in Colab](https://colab.research.google.com/github/nellybutera/pca-african-energy-systems/blob/main/PCA_African_Energy_Systems.ipynb). You can also download `PCA_African_Energy_Systems.ipynb` and use **File > Upload notebook**.
2. Click **Runtime > Run all**. Every cell shows its output, plots included.
3. Nothing else to set up. If the data file isn't next to the notebook, it downloads the exact version we used.

## What's in the repo

| File | What it is |
|---|---|
| `PCA_African_Energy_Systems.ipynb` | The notebook, with all outputs saved |
| `data/owid-energy-data.csv` | The raw data, untouched |
| `data/DATA_DICTIONARY.md` | What each column means |
| `BSE Group Assignments _ Task Sheet_Mathematics_for_Machine_Learning_Formative 2_PCA_Cohort 2_Team15.pdf` | Our task sheet as a PDF |

## Team

- Peer Pair Number: `15` (Cohort 2)
- Teta Butera Nelly
- Mutoni Keira

Task sheet (Google Sheet): https://docs.google.com/spreadsheets/d/1rfQdATzpVLD14FrYAnIOOqQ-1z50cfM5duubmhoiAAM/edit
