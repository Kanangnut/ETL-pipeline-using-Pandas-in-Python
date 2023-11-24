# ETL pipeline using Pandas in Python

<b>Context</b><br><br>
At the outset, I will set up an account to obtain an API key for streamlined data requests. Prioritizing security and to prevent direct embedding of the API key in the source code, I will establish a configuration file named config.py. This project focuses on constructing an ETL pipeline, encompassing data extraction, transformation, and loading processes, to collect information from The Movie Database (TMDB) website.
<br><br>
These csv file contained dataset of movies listed and including to, <br>
<b>dataset:</b> The main Movies Metadata file. Contains information of movies featured in the movie database. Features include backdrops, budget, revenue, release dates, posters, languages, production companies and countries.<br>
<b>tmdb_movies_info:</b> Contains the movie title, vote, movies plot from TMDB website. Available in the form of a stringified JSON Object.
<br><br>
![inbox_15885814_0eb0936f6b821a7d26084adf7213645d_Capture](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/ccdf51a9-b89d-4a92-8a8d-7d51706eb2dc)
<br><br>

<b>API key</b><br>
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/1d523584-5ad4-412a-a591-616762a0af98)

Create the pythonFile.py for:
 - This script extracts data from a website without any transformation or cleaning.
 - The purpose is to explore the raw data and understand its structure.
 - Your code for extracting data goes here
 - Save the raw data to a CSV file without any cleaning or transformation
 - This step helps in understanding the nature of the data and planning for the ETL process
 - Code for saving data to a CSV file

Create the pythonCSV.py for:
 - This script creates a CSV file after applying the ETL (Data Extraction, Data Transformation, Data Loading) pipeline to the data obtained from a website using an API key.
 - Import necessary libraries for data manipulation and API requests
 - Save the cleaned and transformed data to a CSV file
 - Code for saving data to a CSV file

<b>Import necessary libraries</b><br>
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/f70cdae6-2298-4d2b-b202-c7a49e66cf7b)


<b>Data Extraction</b></br>
 - The dataset has 28 column with 837 rows, with no any cleaning data.
   - create a loop that requests each movie one at a time and appends the response to a list.
   - send a single GET request to the API, receive a JSON record
{'success': False, 'status_code': 34, 'status_message': 'The resource you requested could not be found.'}




















