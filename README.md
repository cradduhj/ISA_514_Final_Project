# ISA_514_Final_Project

## Description
This repository contains all of the code and individual assignment submissions related to the Fall 2025 ISA 514 Final Group Project.

## Team Members
Harrison Cradduck, Marah Donahoe, Joey Endres, & William Knapp

## Project Overview
Producers/record labels make money when their signed artists and bands create popular songs, so our goal to help them get a better understanding of what makes a song “popular” or “viral” by building models to predict the success/popularity of a song on YouTube (measured as number of views) through the use of predictors like genre, artist history & type, song audio features, sentiment analysis of the lyrics and titles, and other text mining techniques.

## README
`get_songs.ipynb`: process of web-scraping song titles, artists, and chart years from the Hot 100 Weekly Billboard Charts using the BeautifulSoup package in Python; saved dataframe with songs to CSV file

`get_lyrics.ipynb`: process of pulling song lyrics (text) for each song in the songs CSV file using the Lyrics Genius library in Python to access the Genius API; saved dataframe with songs and lyrics to CSV file

`get_artist_features.ipynb`: process of pulling artist-related features (name, type, genre(s), country, start year of career, etc.) for each unique artist in the songs CSV file using the MusicBrainz API and Wikidata SPARQL endpoints; saved datafrmae with artists and artist-related features to CSV file
* attmepted

`get_YouTube_metrics.ipynb`: process of web-scraping publicly accessible YouTube video metadata (views, likes, comment counts) for each song in the songs CSV file using the yt-dlp package in Python; saved dataframe with songs and YouTube metrics to CSV file

`get_Spotify_features.ipynb`: process of acquiring Spotify audio features (loudness, liveness, energy, key, tempo, acousticness, etc.) for each song in the songs CSV file by merging six comprehensive Kaggle datasets

`MongoDB_collections.ipynb`: 

`final_data.ipynb`: 

`final_dataset.csv`: the final dataset produced and saved from `final_data.ipynb` as a .csv file

`descriptive_summary_cradduhj.ipynb`: 
