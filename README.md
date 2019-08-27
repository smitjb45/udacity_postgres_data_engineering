Project: Data Modeling with Postgres
===================================

In this project, I applied what I learned on data modeling with Postgres and build an ETL pipeline using Python. I defined fact and dimension tables for a star schema for a particular analytic focus, and wrote an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

Pre-requisites
--------------

- PostgresSQL
- Python 3
- psycopg2 package

Getting Started
---------------

To get started, open a console window and type "python create_tables.py" then type "python etl.py"

Support
-------

- Google+ Community: https://plus.google.com/communities/105153134372062985968
- Stack Overflow: http://stackoverflow.com/questions/tagged/android


The purpose of this database in the context of the startup, Sparkify, and their analytical goals.
-------

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. 

State and justify your database schema design and ETL pipeline.
-------

I created the user table, song table, time table, and user tables to be my dimention tables and the song play to make the schema a Star design.

Please see table schema below:
-------

songplay_table_create = ("""CREATE TABLE IF NOT EXISTS songplays 
                            (
                            songplay_id SERIAL,
                            start_time bigint, 
                            user_id int, 
                            level varchar, 
                            song_id varchar, 
                            artist_id varchar,  
                            session_id int,
                            location varchar, 
                            user_agent varchar,
                            PRIMARY KEY (songplay_id)
                            )
                        """)

user_table_create = ("""CREATE TABLE IF NOT EXISTS users (
                                                         user_id int,
                                                         fist_name varchar,
                                                         last_name varchar,
                                                         gender char, 
                                                         level varchar,
                                                         PRIMARY KEY (user_id)
                                                         )
                                                         """)

song_table_create = ("""CREATE TABLE IF NOT EXISTS songs (
                                                         song_id varchar, 
                                                         title text,
                                                         artist_id varchar,
                                                         year int,
                                                         duration float,
                                                         PRIMARY KEY (song_id)
                                                         )
                                                         """)

artist_table_create = ("""CREATE TABLE IF NOT EXISTS artists 
                                                            (
                                                             artist_id varchar, 
                                                             name varchar,
                                                             location varchar,
                                                             lattitude float,
                                                             longitude float, 
                                                             PRIMARY KEY (artist_id)
                                                             )
                                                             """)

time_table_create