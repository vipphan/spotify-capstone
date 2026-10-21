## Notebook

(https://github.com/vipphan/spotify-capstone/blob/main/spotify_capstone.ipynb)
## Tools & Libraries used
• Python 

• Pandas 

• NumPy

• Matplotlib

• Seaborn 

• Scikit-learn

## Overview
A capstone project examining which audio characteristics, danceability, 
energy, tempo, valence, loudness, and acousticness, are most predictive 
of a song's popularity, and whether these relationships have shifted 
between older and more recently released songs. The analysis uses the 
30,000 Spotify Songs dataset from Kaggle, which includes audio features, 
release dates, popularity scores, and genre. Three regression methods, 
LASSO, decision tree, and kernel regression, are each fit on the full 
dataset to identify which features matter most overall, then fit 
separately on older and more recent tracks to test whether those 
relationships change over time. Sequential feature selection is used 
alongside these models as an independent check on feature importance.

## Approach
**Data Cleaning:**
Missing metadata rows, a track with an invalid tempo of 0, and duration 
outliers are removed. Release dates are reduced to release year, which 
is used to split tracks into an older group and a recent group at a 
2015 cutoff, with 2020 excluded due to incomplete coverage.

**EDA:**
Covers general dataset trends, including the most popular tracks, 
artists, and genres, followed by the distribution of each audio feature, 
a correlation heatmap, and a comparison of feature correlations with 
popularity across the older and recent groups.

**Modeling:**
LASSO, decision tree, and kernel regression are each fit on the full 
dataset to identify which features are most predictive of popularity 
overall, then fit separately on the older and recent groups to test 
whether those relationships shift over time. Sequential feature 
selection is used alongside these models as an independent check on 
feature importance. Each model is tuned using grid search.

**Evaluation:**
Model performance is measured using RMSE and R-squared. Results are 
compared across models and across eras to determine which features are 
most predictive overall and whether their predictive strength has 
changed between older and more recent tracks.

## Key Findings

* Across all three models, predictive performance from audio features 
  alone is modest, with R-squared values generally below 0.1.
* Energy and loudness are the most consistently influential features 
  across methods and eras.
* Tempo shows a stronger relationship with popularity in the decision 
  tree model for older tracks specifically, a pattern not captured by 
  the linear-based methods.
* Feature relationships with popularity differ somewhat between older 
  and more recent tracks, both in which features contribute and in 
  overall model performance.

## Next Steps

* Finalize full-dataset versions of each model to directly answer which 
  features matter most overall, separate from the era comparison.
* Complete grid search tuning for the remaining models.
* Write up the final discussion, limitations, and conclusion sections 
  of the report.
