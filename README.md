# Project: Data Modeling with Postgres

## 1. General project information

### 1.1. Introduction

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

### 1.2. Project Description

In this project, you'll apply what you've learned on data modeling with Postgres and build an ETL pipeline using Python. To complete the project, you will need to define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

### 1.3. Schema for Song Play Analysis

Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

#### 1.3.1. Fact Table

1. songplays - records in log data associated with song plays i.e. records with page NextSong
    - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#### 1.3.2. Dimension Tables

1. users - users in the app
    - user_id, first_name, last_name, gender, level
2. songs - songs in music database
    - song_id, title, artist_id, year, duration
3. artists - artists in music database
    - artist_id, name, location, latitude, longitude
4. time - timestamps of records in songplays broken down into specific units
    - start_time, hour, day, week, month, year, weekday

### 1.4. Disclaimer

Data and project information were kindly provided by [Udacity](https://www.udacity.com/).

***

## 2. Documentation

### 2.1. Discuss the purpose of this database in the context of the startup, Sparkify, and their analytical goals

The music streaming startup Sparkify wants to understand what songs their users are listening to. Currently, all information is stored in raw JSON source files and cannot be accessed easily. The purpose of the project is a) to create a database schema, b) set up a Postgres database based on that schema and c) to migrate the existing raw data into the new database using an ETL pipeline. The new database can be queried easily by the Sparkify analytics team to answer their analytical questions and goals.

### 2.2. How to run the Python scripts

1. Execute create_tables.py on the terminal with the command ```python create_tables.py```, to create the underlying tables
2. Execute etl.py on the terminal with the command ```python etl.py```, to migrate the data into the tables
3. Run test.ipynb, to test if the migration happened correctly

### 2.3. Explanation of the files in the repository

- data/log_data
    - contains source log files in JSON format
    - used to fill songplays, users and time tables

- data/song_data
    - contains source song files in JSON format
    - used to fill songs and artists tables

- sql_queries.py
    - Python script
    - contains all SQL statements used in the project

- create_tables.py
    - Python script
    - creation of database and tables used for data storage

- etl.ipynb
    - Python Jupyter Notebook 
    - can be used used to explore the data and test the ETL process

- etl.py
    - Python script 
    - reads JSON log and song data files
    - processes the data
    - inserts data into the database

- test.ipynb
    - Python Jupyter Notebook 
    - tests for correct loading of the data
    - sanity tests with test cases

- README.md
    - Markdown file
    - general project information
    - documentation on project

### 2.4. State and justify your database schema design and ETL pipeline

The **database schema design** is a Star schema and contains one fact table *songplays* and four dimension tables *users*, *songs*, *artists* and *time*. Each dimensional table contains a primary key that is being referenced by the fact table. The Star schema offers flexibility with the aggregation analyses that the Sparkify analytics team needs to perform to answer their analytical goals.

The **ETL pipeline** contains four functions:
- The function *process_song_file* is used to extract the data from the raw song JSON file and insert the data into the tables *songs* and *artists*
- The function *process_log_file* is used to extract the data from the raw log JSON file and insert the data into the tables *time*, *users* and *songplays*
- The function *process_data* loads and processes the raw JSON files
- The function *main* creates the database connection, processes song_data and log_data information and finally closes the database connection