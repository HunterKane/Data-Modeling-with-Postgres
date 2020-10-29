# Summary of project

Startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

In order to enable Sparkify to analyze their data, a Relational Database Schema was created, which can be filled with an ETL pipeline.

# How to run the python scripts

To create the database tables and run the ETL pipeline, you must run the following two files in the order that they are listed below

To create tables:
```bash
python3 create_tables.py
```
To fill tables via ETL:
```bash
python3 etl.py
```

# Files in the repository
* **[data](data)**: Folder containing data of songs and logs 
* **[create_tables.py](create_tables.py)**: Python script to perform SQL-Statements for (re-)creating database and tables
* **[sql_queries.py](sql_queries.py)**: Python script containing SQL-Statements used by create_tables.py and etl.py
* **[etl.py](etl.py)**: Python script to extract the needed information from Song and Log data inside the data folder and parsing/inserting them to the created database schema and tables

# The purpose of this database

Using a database makes it easier to analyze the data. By using SQL and the star scheme, joins and aggregations, the data can be searched and summarized quickly and easily.  By using a relational database, Sparkify can also perform ad hoc analysis of its database. 

# The database schema design and ETL pipeline.

In order to enable Sparkify to analyze their data, a Relational Database Schema was created, which can be filled with an ETL pipeline.

The so-called star scheme enables the company to view the user behaviour over several dimensions.
The fact table is used to store all user song activities that contain the category "NextSong". Using this table, the company can relate and analyze the dimensions users, songs, artists and time.

In order to fill the relational database, an ETL pipeline is used, which makes it possible to extract the necessary information from the log files of the user behaviour as well as the corresponding master data of the songs and convert it into the schema.

* **Fact Table**: songplays
* **Dimension Tables**: users, songs, artists and time.

Fact Table

songplays - records in log data associated with song plays i.e. records with page NextSong

songplay_id (INT) PRIMARY KEY: ID of each user song play
start_time (DATE) NOT NULL: Timestamp of beggining of user activity
user_id (INT) NOT NULL: ID of user
level (TEXT): User level {free | paid}
song_id (TEXT) NOT NULL: ID of Song played
artist_id (TEXT) NOT NULL: ID of Artist of the song played
session_id (INT): ID of the user Session
location (TEXT): User location
user_agent (TEXT): Agent used by user to access Sparkify platform
Dimension Tables

users - users in the app

user_id (INT) PRIMARY KEY: ID of user
first_name (TEXT) NOT NULL: Name of user
last_name (TEXT) NOT NULL: Last Name of user
gender (TEXT): Gender of user {M | F}
level (TEXT): User level {free | paid}
songs - songs in music database

song_id (TEXT) PRIMARY KEY: ID of Song
title (TEXT) NOT NULL: Title of Song
artist_id (TEXT) NOT NULL: ID of song Artist
year (INT): Year of song release
duration (FLOAT) NOT NULL: Song duration in milliseconds
artists - artists in music database

artist_id (TEXT) PRIMARY KEY: ID of Artist
name (TEXT) NOT NULL: Name of Artist
location (TEXT): Name of Artist city
lattitude (FLOAT): Lattitude location of artist
longitude (FLOAT): Longitude location of artist
time - timestamps of records in songplays broken down into specific units

start_time (DATE) PRIMARY KEY: Timestamp of row
hour (INT): Hour associated to start_time
day (INT): Day associated to start_time
week (INT): Week of year associated to start_time
month (INT): Month associated to start_time
year (INT): Year associated to start_time
weekday (TEXT): Name of week day associated to start_time

# Dataset used

The first dataset is a subset of real data from the [Million Song Dataset](http://millionsongdataset.com/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.