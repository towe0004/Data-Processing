# Process Book

Project: How do weather conditions influence tourist arrivals in Singapore?

## Template

**Date of entry:**
**What I've worked on:**
**What problems I encountered:**
**What I learned:**
**Which resources did I use:**

---

## Entries

### 20 November 2026

**What I've worked on:**
- Set up the GitHub repository with the notebook (`DP.ipynb`) and the project proposal.
- Used `kagglehub` to load the Kaggle Global Weather Repository (DS1) in the notebook.
- Changed the code so the dataset downloads into the repo's `data/` folder instead of a hidden cache folder. Teammates who clone the repo now get the same file.
- Added a `.gitignore` so Kaggle's leftover download files are not committed.
- Included the DS2 (SingStat weather) and DS3 (SingStat tourist arrivals), performed profiling, structuring, enriching and cleaning.

**What problems I encountered:**
- The notebook crashed with `IndexError: list index out of range` when loading the CSV.
- The cause: the latest Kaggle version (1106) downloads as an empty archive, so no CSV was found.
- Fix: pinned the dataset to version 1105, which works
- The old code saved data relative to wherever Jupyter was started. I changed it to find the repo folder automatically.
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
- GitHub file size limits: https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github
