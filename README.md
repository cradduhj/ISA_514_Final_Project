# ISA_514_Final_Project

## Description
This repository contains all of the code and individual assignment submissions related to the Fall 2025 ISA 514 Final Group Project.

## Team Members
Harrison Cradduck, Marah Donahoe, Joey Endres, & William Knapp

## Project Overview
Producers/record labels make money when their signed artists and bands create popular songs, so our goal to help them get a better understanding of what makes a song “popular” or “viral” by building models to predict the success/popularity of a song on YouTube (measured as number of views) through the use of predictors like genre, artist history & type, song audio features, sentiment analysis of the lyrics and titles, and other text mining techniques.

## Repository Structure
This public repository includes the project submission files (in the `Submission` folder) in addition to the series of Jupyter notebooks necessary to collect, analyze, engineer, and model our data. Each of the files below must be run in the order that they are listed to fully and exactly reproduce the data collection, data analysis, feature engineering, and predictive modeling processes described in this project.

## README
`get_songs.ipynb`: process of web-scraping song titles, artists, and chart years from the Hot 100 Weekly Billboard Charts using the BeautifulSoup package in Python; saved dataframe with songs as `all_songs_clean.csv`

`get_lyrics.ipynb`: process of pulling song lyrics (text) for each song in the songs CSV file using the Lyrics Genius library in Python to access the Genius API; saved dataframe with songs and lyrics as `all_songs_clean_lyrics.csv`

`get_artist_features.ipynb`: process of pulling artist-related features (name, type, genre(s), country, start year of career, etc.) for each unique artist in the songs CSV file using the MusicBrainz API and Wikidata SPARQL endpoints; saved datafrmae with artists and artist-related features as `all_artists`

`get_YouTube_metrics.ipynb`: process of web-scraping publicly accessible YouTube video metadata (views, likes, comment counts) for each song in the songs CSV file using the yt-dlp package in Python; saved dataframe with songs and YouTube metrics as `all_songs_clean_youtube.csv`
* Attempted to use the YouTube Data API v3, but were met with a 100 requests per day maximum.
  
`get_Spotify_features.ipynb`: process of attempting to acquire Spotify audio features (loudness, liveness, energy, key, tempo, acousticness, etc.) for each song in the songs CSV file by merging six different Kaggle datasets with the songs dataframe; saved dataframe with songs and Spotify audio features as `6578_songs_clean_spotify.csv`
* Attempted to use the Spotify Web API, but the audio features endpoint was deprecated in November 2024.
* The six Kaggle datasets with audio features for a variety of songs were created pre-November 2024.

`MongoDB_collections.ipynb`: process of inserting all previous CSV files (lyrics, artist-related features, YouTube metrics, Spotify audio features) into collections in MongoDB
* Streamlined the MongoDB data insertion process for all team members.

`final_data.ipynb`: process of accessing all data collections in MongoDB as dataframes in Python, merging these dataframes (using `track_id` and a combination of `title` and `artist`) to combine all features for each song into one dataframe, and cleaning the features in the dataframe by imputing missing values, correcting data types, and making the data model-ready; saved final dataframe with 5,492 complete observations (songs) as `final_dataset.csv`

`final_dataset.csv`: the final dataset produced and saved from `final_data.ipynb` as a CSV file

`descriptive_summary_cradduhj.ipynb`: Harrison's descriptive summary of the final dataset, including line charts, bar plots, a heatmap, and a scatter plot

`feature_engineering_cradduhjipynb`: Harrison's feature engineering of the final dataset, including sentiment analysis, lexical features, and LDA; saved final dataframe with added features as `model_ready_dataset.csv`

`model_ready_dataset.csv`: the model-ready dataset produced and saved from `feature_engineering_cradduhj.ipynb` as a CSV file

`modeling_cradduhj.ipynb`: Harrison's modeling of the model-ready dataset, including MLR with scaled numeric variables and a log-transformed target (view_count)
