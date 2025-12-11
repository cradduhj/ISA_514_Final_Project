# ISA_514_Final_Project

## Description
This repository contains all of the Jupyter notebooks and individual assignment submissions related to the Fall 2025 ISA 514 Final Group Project.

## Team Members
Harrison Cradduck, Marah Donahoe, Joseph Endres, & William Knapp

## Project Overview
Producers/record labels make money when their signed artists and bands create popular songs, so our goal to help them get a better understanding of what makes a song “popular” or “viral” by building models to predict the success/popularity of a song on YouTube (measured as number of views) through the use of predictors like genre, artist history & type, song audio features, sentiment analysis of the lyrics and titles, subjectivity analysis, and LDA topic modeling.

## Repository Structure
This public repository includes the project submission files (in the `Submission` folder) in addition to the series of Jupyter notebooks necessary to collect, analyze, engineer, and model our data. Each of the files below must be run in the order that they are listed to fully and exactly reproduce the data collection, data analysis, feature engineering, and predictive modeling processes described in this project.

## Technical Requirements
To fully reproduce this project, one will need JupyterLab (or another Python IDE capable of opening .ipynb files). All libraries and packages required to run all of the code are installed and loaded at the beginning of each notebook. One will also need access to a MongoDB database capable of inserting and pulling collections.

## Additional Downloadable Datasets
Incorporating Spotify audio features data into this project requires the downloading of 6 separate Kaggle datasets from the Web. As these files are too large to include in this repository, the links to download these datasets are listed below:
* https://www.kaggle.com/datasets/julianoorlandi/spotify-top-songs-and-audio-features
* https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset
* https://www.kaggle.com/datasets/tomigelo/spotify-audio-features
* https://www.kaggle.com/datasets/rodolfofigueroa/spotify-12m-songs
* https://www.kaggle.com/datasets/rohitgrewal/spotify-youtube-data

## Jupyter Notebooks
`get_songs.ipynb`: This notebook demonstrates the process of web-scraping song titles, artists, and chart years from the Hot 100 Weekly Billboard Charts by year using the BeautifulSoup package in Python; it produces a saved dataframe with songs named `all_songs_clean.csv`.

`get_lyrics.ipynb`: This notebook demonstrates the process of pulling song lyrics (text) by matching `title` and `artist` for each song in the songs CSV file using the Lyrics Genius library in Python to access the Genius API; it inserts the dataframe into a MongoDB collection named LYRICS; it produces a saved dataframe with songs and lyrics named `all_songs_clean_lyrics.csv`.

`get_artist_features.ipynb`: This notebook demonstrates the process of pulling artist-related features (name, type, genre(s), country, start year of career, etc.) for each unique artist in the songs CSV file using the MusicBrainz API and Wikidata SPARQL endpoints; it inserts the dataframe into a MongoDB collection named ARTISTS; it produces a saved dataframe with artists and artist-related features names `all_artists.csv`.

`get_YouTube_metrics.ipynb`: This notebook demonstrates the process of web-scraping publicly accessible YouTube video metadata (views, likes, comment counts) by matching `title` and `artist` for each song in the songs CSV file using the yt-dlp package in Python; it lightly cleans the YouTube data and inserts the dataframe into a MongoDB collection named YOUTUBE; it produces a saved dataframe with songs and YouTube metrics named `all_songs_clean_youtube.csv`.
* Attempted to use the YouTube Data API v3, but were met with a 100 requests per day maximum.
  
`get_Spotify_features.ipynb`: This notebook demonstrates the process of acquiring Spotify audio features (loudness, liveness, energy, key, tempo, acousticness, etc.) by matching `track_id`, then `title` and `artist`, for each song in the songs CSV file with Kaggle datasets, and merging the six different Kaggle datasets with the songs dataframe; it lightly cleans the merged columns and inserts the dataframe into a MongoDB collection named SPOTIFY; it produces a saved dataframe with songs and Spotify audio features named `6578_songs_clean_spotify.csv`.
* Attempted to use the Spotify Web API, but the audio features endpoint was deprecated in November 2024.
* The six Kaggle datasets with audio features for a variety of songs were created pre-November 2024, allowing us to bypass the endpoint deprecation and use the Kaggle datasets as a proxy source.

`MongoDB_collections.ipynb`: This notebook demonstrates the process of inserting all previous CSV files (lyrics, artist-related features, YouTube metrics, Spotify audio features) into collections in MongoDB.
* FYI: The code in this notebook does not need to be run completely or at all if the data from the previous notebooks has been properly inserted into MongoDB collections.
* This notebook is a check to ensure all data is inserted into MongoDB collections.
* If unsure of data integrity and completion in MongoDB, delete all related collections in MongoDB and run this notebook.
* Streamlined the MongoDB data insertion process for all team members.

`data_cleaning.ipynb`: This notebook demonstrates the process of accessing all data collections in MongoDB as dataframes in Python, merging these dataframes (using `track_id` and a combination of `title` and `artist`) to combine all features for each song into one dataframe, and cleaning the features in the dataframe by imputing missing values, correcting data types, dummy-coding factors, and mapping genres; it produces a saved dataframe with 5,492 complete observations (songs) named `final_dataset.csv`.

`exploratory_data_analysis.ipynb`: This notebook performs exploratory data analysis on the final cleaned dataset, `final_dataset.csv`, produced from `data_cleaning.ipynb`, by creating descriptive summaries of songs, artists, lyrics, chart years, and audio features using tables, plots (bar, line, column, heatmap, scatter), and dictionaries (MongoDB). This is to inform feature engineering decisions and begin to formulate expectations for predictive modeling in terms of model selection and performance.

`summary_statistics`: This notebook compiles the relevant statistics based on the predictor type for all predictors in the datasets and puts them in a presentation-ready format.

`feature_engineering.ipynb`: This notebook takes the final cleaned dataset, `final_dataset.csv`, produced from `data_cleaning.ipynb`, and applies feature engineering/text mining techniques like sentiment analysis (of both song titles and lyrics), subjectivity analysis, lexical analysis (word count, average word length, unique word count, etc.), and LDA topic modeling to the data to make it model-ready; it produces a saved dataframe with the model-ready data (5,395 complete songs, 60 predictors) named `model_ready_dataset.csv`.

`DecisionTree_modeling`: This notebook fits and evaluates decision tree models on the data using cross-validation and a grid search for hyperparameter tuning. The first model considers `view_count` as the original, continuous response variable. The second model considers `viral` as a created binary response variable with `1` indicating viral (greater than 100,000,000 views) and `0` indicating not viral (less than or equal to 100,000,000 views).

`RandomForest_modeling`: This notebook fits and evaluates Random Forest models on the data using cross-validation and a grid search for hyperparameter tuning. The first model considers `view_count` as the original, continuous response variable. The second model considers `viral` as a created binary response variable with `1` indicating viral (greater than 100,000,000 views) and `0` indicating not viral (less than or equal to 100,000,000 views).

`XGBoost_modeling`: This notebook fits and evaluates XGBoost models on the data using cross-validation and a grid search for hyperparameter tuning. The first model considers `view_count` as the original, continuous response variable. The second model considers `viral` as a created binary response variable with `1` indicating viral (greater than 100,000,000 views) and `0` indicating not viral (less than or equal to 100,000,000 views).

`SupportVector_modeling`: This notebook fits and evaluates Support Vector models on the data using cross-validation and a grid search for hyperparameter tuning. The first model considers `view_count` as the original, continuous response variable. The second model considers `viral` as a created binary response variable with `1` indicating viral (greater than 100,000,000 views) and `0` indicating not viral (less than or equal to 100,000,000 views).
