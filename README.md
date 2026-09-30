# PCA on African energy systems (Formative 2, PCA Pair Team 15)

Group: Teta Butera Nelly, Mutoni Keira

## Submission documents
- **Report (Google Doc):** https://docs.google.com/document/d/1vekiISmocnkwVbJh9MmUXKHiB82lJhQ3brzOcpq6Hxo/edit
- **Task sheet (Google Sheet):** https://docs.google.com/spreadsheets/d/1kkgPBFFLvajCwub096beNw43_AatlmdXoaAnaC0QjMc/edit

## Files in this repo
| File | What it is |
|---|---|
| `PCA_African_Energy_Systems.ipynb` | The notebook (all outputs saved; open in Google Colab) |
| `BSE Group Assignments _ Task Sheet_Mathematics_for_Machine_Learning_Formative 2_PCA_Cohort 2_Team15.pdf` | Contribution sheet (PDF copy of the Google Sheet) |
| `Task_Sheet_PCA_Formative_2_Pair15.xlsx` | Editable copy of the contribution sheet |
| `data/owid-energy-data.csv` | Raw data, unmodified, from the [Our World in Data energy dataset](https://github.com/owid/energy-data) (commit `7e387a1`). The notebook filters it to the 54 African countries, 2000-2022. |
| `figures/` | Figures used in the report |

The analysis uses only `numpy` and `matplotlib`. The standard-library modules `os`, `urllib` and `time` are used only to download the data and time the benchmarks.

[Open the notebook in Google Colab](https://colab.research.google.com/github/nellybutera/pca-african-energy-systems/blob/main/PCA_African_Energy_Systems.ipynb)

## How to run in Google Colab

1. Download `PCA_African_Energy_Systems.ipynb` from this repository.
2. In Colab, choose **File > Upload notebook** and select the downloaded notebook.
3. Choose **Runtime > Run all** and confirm each cell completes with its output.
4. The notebook downloads the pinned OWID data file when it is not available locally. The analysis uses `numpy` and `matplotlib`.

## Results summary

The analysis covers 1,230 country-years from 54 African countries (2000-2022). It imputes missing values, one-hot encodes sub-regions, log-transforms selected skewed measures, and standardizes 19 features before PCA. PC1 explains 34.1% of the variance; seven components retain 90.0%, reducing the feature space from 19 dimensions to 7.
