# Udacity_Project1_DataModeling
Use postgresql to do data modeling

# DataBase Modeling for StartUp Sparkify


## Table of Contents

* [Project Purpose](#project-purpose)
* [Technologies](#technologies)
* [Data Source](#data-source)
* [Design of sparkifydb Database](#design-of-sparkifydb-database)
* [Files Launch & ETL Pipeline](#files-launch-&-etl-pipeline)


## 1. Project Purpose

The establishment of this database aims to create the analysis basis of users' music listening behaviours in the Sparkify music streaming app.

The listeners' preference e.g. favourite artists, music listening periods during a day, intention to purchase a membership may be analyzed based 
on this database, so that the app could push the recommendation more precisely. Giving the customers or listners what they want the most is definitely 
an important goal for a startup like Sparkify to open the market.


## 2. Technologies

RDBMS: postgresql
Driver: python3


## 3. Data Source

Format: .json
Song data: detailed infos about available songs and corresponding artists are included.
Log data: detailed infos about users and their music listening behaviours are included.

There are duplicates in data, which can be prevented with sql insert "on conflict do nothing" commando.
![Duplicates in song data](pics/song_data_duplicates.JPG)


## 4. Design of sparkifydb Database

The database has the star schema:
- songplays table --> fact table
- dimension tables --> users, songs, artists & time tables


## 5. Files Launch & ETL Pipeline

Execution sequence: sql_queries.py --> create_tables.py --> etl.py

### 5.1 file sql_queries.py

contains the order strings of the table creation, insertation and search queries.

### 5.2 create_tables.py

drops and creats the tables for a new start to run the etl pipeline (using creation queries from sql_queries.py).

### 5.3 etl.py

contains the funtions to execute all etl steps file by file (using insertation & search queries from sql_queries.py).

#### 5.3.1 main()

calls process_data twice to process song data and log data.

#### 5.3.2 process_data()

can call process_song_file() & process_log_file() to process the song files and log files sequentially.

#### 5.3.3 process_song_file()

handles single song data file to extract song + artist data and inserts them seperately into songs and artists tables.

#### 5.3.4 process_log_file()

handles single log data file to extract user + time + songplays data and inserts them seperately into users, time and songplays tables.

since there must be multiple logs of one user, it is better to drop the duplicates in the first place, so that the sql insert try for the duplicates is not necessary.
