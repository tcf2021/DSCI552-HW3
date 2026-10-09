# DSCI 552 - Homework 3

**Name:** Chengfeng Tang  
**GitHub username:** tcf2021  
**USC ID:** 5488902262

This repository contains my solutions to the AReM feature extraction problem and ISLR Exercise 3.7.4. The notebook includes my answers, code, and executed outputs.

## Files

- `notebook/Tang_Chengfeng_HW3.ipynb`: complete assignment.
- `data/AReM/`: the 88 original CSV recordings in seven activity folders.
- `data/processed/instance_manifest.csv`: instance IDs, filenames, train/test assignments, and cleaning counts.
- `data/processed/features_all.csv`: all 42 features for all 88 instances, with identifying metadata.
- `data/processed/features_train.csv` and `features_test.csv`: the prescribed training and test subsets.
- `data/processed/feature_sd_bootstrap_90.csv`: feature standard deviations and 90% bootstrap confidence intervals.
- `data/processed/features_selected.csv`: mean, standard deviation, and maximum for each channel.
- `requirements.txt`: Python dependencies.

## Running the notebook

I ran all code cells sequentially using Python 3.12. From the repository root:

```bash
python -m pip install -r requirements.txt
cd notebook
jupyter notebook Tang_Chengfeng_HW3.ipynb
```

The notebook uses relative paths and can run from a fresh kernel. Running all cells regenerates the processed CSV files from the original recordings.

## Methods

I used the specified split of 69 training and 19 test instances. I retained the original measurement scales, used sample standard deviations (`ddof=1`), and calculated quartiles using linear interpolation.

The loader handles whitespace delimiters and trailing commas. One missing time point at 13,500 ms in `sitting/dataset8.csv` is interpolated from its immediate neighbors within that recording. The original CSV files are unchanged.

For each feature, I estimated its standard deviation across all 88 instances and computed a percentile bootstrap interval using 20,000 resamples of entire instance rows, with seed 42. This treats recordings as independent sampling units. The intervals are individual 90% intervals for the pooled activity mixture.

## Data source

Palumbo, F., Gallicchio, C., Pucci, R., and Micheli, A. (2016). *Activity Recognition system based on Multisensor data fusion (AReM).* UCI Machine Learning Repository. https://doi.org/10.24432/C5SS33. License: CC BY 4.0. Additional references are listed in the notebook.
