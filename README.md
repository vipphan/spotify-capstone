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
A capstone project examining which audio characteristics, danceability, energy, tempo, valence, loudness, and acousticness, are most predictive of a song's popularity, and whether these relationships have shifted between older and more recently released songs. The analysis uses the 30,000 Spotify Songs dataset from Kaggle, which includes audio features, release dates, popularity scores, and genre. Duplicate playlist entries for the same track are removed before analysis, since the raw dataset repeats a track once for every playlist it appears in. Sequential feature selection runs first to narrow down which features a linear model finds most useful, followed by LASSO, decision tree, and kernel regression, each fit on the full dataset to identify which features matter most overall and fit separately on older and more recent tracks to test whether those relationships change over time. A random forest is added as an ensemble method, fit with the original features and again with a set of engineered features. Because regression performance is modest, popularity is also reframed as a three-tier classification problem to test whether audio features predict general performance tier more reliably than the exact score.

## Approach
**Data Cleaning:**
Missing metadata rows, a track with an invalid tempo of 0, and duration outliers are removed. Duplicate rows for the same track, which differ only in playlist metadata, are reduced to one row per track. Release dates are reduced to release year, which is used to split tracks into an older group and a recent group at a 2015 cutoff, with 2020 excluded due to incomplete coverage.

**EDA:**
Covers general dataset trends, including the most popular tracks, artists, and genres, followed by the distribution of each audio feature, a correlation heatmap, and a comparison of feature correlations with popularity across the older and recent groups. A Yeo-Johnson power transformation is applied to the audio features to sharpen the pairplot pattern. This transformation is used for visualization only and is not carried into modeling.

**Feature Engineering:**
 Five features are built from audio feature combinations that showed a notable relationship with popularity or with each other during EDA, including energy and loudness together, danceability and valence together, the gap between energy and acousticness, loudness relative to energy, and distance from a tempo of 125. These are added to the older, recent, and whole-dataset splits before modeling.

**Modeling:**
Sequential feature selection runs first, on the older group, recent group, and whole dataset, to identify which three features a linear model finds most useful. LASSO, decision tree, and kernel regression follow, each fit separately on the older and recent groups to test whether feature relationships shift over time, with LASSO and the decision tree also fit on the whole dataset. Kernel regression is fit on the era splits only, since fitting it on the whole dataset is computationally expensive. Each model is tuned using grid search. A random forest is fit on the older, recent, and whole-dataset splits, using the original six features and again using the six original plus the five engineered features, to test whether an ensemble model or additional features improve on the single models.

**Three-Tier Classification:**
 Because regression R-squared values are low across all models, popularity is divided into three tiers, Low, Medium, and High, using era-specific cutoffs so that class sizes stay balanced within each era. An L1-penalized logistic regression, a decision tree classifier, and a random forest classifier are each fit against a majority-class baseline to test whether audio features predict a track's general performance tier more reliably than the exact popularity score.

**Evaluation:**
Regression performance is measured using RMSE and R-squared. RMSE reports prediction error in the same units as popularity, while R-squared shows how much of the variation in popularity a model explains and is easier to compare across models since it does not depend on the scale of the target. Classification performance is measured using accuracy and macro F1, reported together so that a model relying too heavily on one tier is flagged by a low macro F1 even if its accuracy looks reasonable. Results are compared across models and across eras to determine which features are most predictive overall and whether their predictive strength has changed between older and more recent tracks.

## Key Findings

* Energy and loudness are the features most consistently tied to popularity across LASSO, the decision tree, the random forest, and SFS, with the largest LASSO coefficients and top feature importance rankings.
* This relationship is strongest in recent tracks, where energy and loudness account for roughly 60 to 70 percent of feature importance. In older tracks the signal is weaker and spread across more features, with valence and danceability carrying more weight than energy or loudness.
* Danceability's relationship with popularity reverses sign between eras, moving from negative in older tracks to positive in recent ones.
* No model explains more than about 9 percent of the variation in popularity. This holds across LASSO, decision tree, kernel regression, and random forest, and across both the original and engineered feature sets.
* Adding five engineered features and applying a Yeo-Johnson transformation each changed R-squared by less than one percent, indicating the weak relationship comes from the data itself rather than feature scaling or a lack of engineered features.
* Reframing popularity as a three-tier classification problem produced only a modest improvement over a majority-class baseline, with the same era pattern holding, loudness and energy strongest in recent tracks, weaker and more spread out signal in older tracks.

## Next Steps

* Incorporate features outside this analysis's scope, such as genre, an artist's existing popularity, and playlist placement. Genre alone showed a 12-point gap in average popularity during EDA, larger than the effect of any individual audio feature tested.
* Explore additional audio features available in the dataset but not used here, such as speechiness and instrumentalness.
* Treat the duplicate playlist entries found during data cleaning as a reminder to check for repeated tracks before treating a playlist-based dataset as a collection of unique songs.
