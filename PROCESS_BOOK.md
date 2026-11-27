# Process Book

Project: How do weather conditions influence tourist arrivals in Singapore?
---

## Entries

### 20 November 2026

**What I've worked on:**
- Set up the GitHub repository with the notebook and the project proposal.
- Used `kagglehub` to load the Kaggle Global Weather Repository (DS1) in the notebook.
- Changed the code so the dataset downloads into the repo's `data/` folder.
- Added a `.gitignore` so Kaggle's leftover download files are not committed.
- Included DS2 (SingStat weather) and DS3 (SingStat tourist arrivals), which includes profiling, structuring, enriching and cleaning.

**What problems I encountered:**
- The notebook crashed with `IndexError: list index out of range` when loading the CSV.
- The cause: the latest Kaggle version downloads as an empty archive, so no CSV was found.
- Fix: pinned the dataset to version 1105.
- DS2 and DS3 are not loaded from SingStat directly. They come from Google Sheets copies, so they will not update by themselves and break if the Sheets are removed.

**What I learned:**
- `kagglehub.dataset_download()` has an `output_dir` option to save files to a chosen folder.
- Pinning a dataset version makes results reproducible, because Kaggle datasets can change daily.
- An empty download does not always raise an error. It is worth checking that files exist after downloading.
- Files on GitHub must be under 100 MB, so our 45 MB CSV can be stored in the repo.
- How to stage, commit and push changes with Git.

**Which resources did I use:**
- kagglehub documentation: https://github.com/Kaggle/kagglehub
- Kaggle Global Weather Repository (DS1): https://www.kaggle.com/datasets/nelgiriyewithana/global-weather-repository
- SingStat Table Builder M890081, weather (DS2): https://tablebuilder.singstat.gov.sg/table/TS/M890081
- SingStat Table Builder M550001, tourist arrivals (DS3): https://tablebuilder.singstat.gov.sg/table/TS/M550001

### 27 November 2026

**What I've worked on:**
- Changed DS2 and DS3 to load straight from the SingStat Table Builder API instead of the Google Sheets copies since it is static data.
- The data now runs to October 2026 for DS2 (622 months) and September 2026 for DS3 (225 months). 
- Added Section 2.4 (merging) and Sections 3.1–3.2 (descriptive and diagnostic analysis):
  - **Merging (2.4):** checks that each month appears only once and that no months are missing. Missing values are now counted from the data instead of typed in.
  - **Pipeline diagram (2.4.1):** the labels are now calculated from the data instead of typed in.
  - **Cross-check (2.4.2):** compares the Kaggle weather (DS1) with the NEA weather (DS2) for the months where both exist.
  - **Descriptive (3.1):** added a seasonal index, and combined the four weather charts into one figure.
  - **Diagnostic (3.2):** tests each weather variable three ways: against raw arrivals, against the seasonal index, and as unusual weather vs unusual arrivals for the same calendar month.
- Wrote the commentary for Sections 2.4, 3.1 and 3.2 based on the results.

**What problems I encountered:**
- The SingStat API returns at most 5,000 data points per request, so the helper fetches the table in pages using `offset`.
- **Raw arrivals misled the correlations:** they doubled from 2008 to 2019, so correlating them with weather mostly measured that growth. Humidity looked linked to arrivals (r = −0.39) only because humidity also fell over the same years. Using the seasonal index removes this.
- **Years that distort the results:** 2020–2021 (COVID), 2022–2023 (recovery) and 2026 (only nine months) are left out of the seasonal and diagnostic analysis.

**What I learned:**
- Many government statistics sites have an API. Loading data from it keeps the analysis up to date and avoids copies that can go missing.
- A correlation between two series that both trend over time can be meaningless. Remove the trend (and the seasonal pattern) before reading anything into it.

**Results so far:**
- Once the growth trend and the holiday calendar are removed, no weather variable is linked to arrivals.
- Arrivals peak in July, August and December (school holidays), not in the months with the best weather.
- February is the sunniest and driest month but one of the quietest.

**Which resources did I use:**
- SingStat Table Builder API: https://tablebuilder.singstat.gov.sg/api/table/tabledata/M890081 and https://tablebuilder.singstat.gov.sg/api/table/tabledata/M550001
- SciPy documentation (Pearson, Spearman, Kruskal–Wallis tests): https://docs.scipy.org/doc/scipy/
