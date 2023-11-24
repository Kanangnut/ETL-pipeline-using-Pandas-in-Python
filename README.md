# ETL pipeline using Pandas in Python

<b>Context</b>
At the outset, I will set up an account to obtain an API key for streamlined data requests. Prioritizing security and to prevent direct embedding of the API key in the source code, I will establish a configuration file named config.py. This project focuses on constructing an ETL pipeline, encompassing data extraction, transformation, and loading processes, to collect information from The Movie Database (TMDB) website.
These csv file contained dataset of movies listed and including to, dataset: The main Movies Metadata file. Contains information of movies featured in the movie database. Features include backdrops, budget, revenue, release dates, posters, languages, production companies and countries.
tmdb_movies_info: Contains the movie title, vote, movies plot from TMDB website. Available in the form of a stringified JSON Object.
