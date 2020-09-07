# Movies: Extract Transform and Load

## Overview

This project is to extract the movies data from Kaggle and Wikipedia, perform data cleaning on the datasets and then load them in a SQL database. The wikipedia data was extracted in a JSON format and Kaggle data was extracted in CSV format.

## Data Cleanup

The Wikipedia data was in a JSON format and required the most cleanup. Below are the clean up transformations that was performed on the wikipedia dataset

- Any TV shows were filtered out from the movie list
- Any  row that did not have an IMDB link was filtered out
- All the columns that had null values were removed
- Data that were represented in multiple column were merged (Example columns Director and Directed By were merged into one Director column)
- Currency data in BoX Office and Budget columns were parsed using regular expressions and were converted to numeric values
- Release Date amd Running Time column were parsed using regular expressions and was formated accordingly

The movie metadata and ratings data were extracted from Kaggle. Both the files were in consistent format and just needed data type change/clean up

## Data Merge

The wikipedia and Kaggle metedata were first merged together. There were few duplicate/redundant columns after the merge. Each column was induvidualy analysed and necessary transformations were performed. The merged movie data was then combined with the ratings data. Any movie that dis not have a rating in the rating dataset was filled witha 0 rating.

## Load to Postgres Database

The final merged dataset with the ratings was loaded to postgres database. The raw ratings data was also loaded to the datsbase. Since the ratings dataset was huge, it was broken into chunks and loaded.