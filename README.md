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
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/8bcff468-0d7c-4680-b9a9-35f10dc72b49)

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
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/e65568dd-b7fc-4ebb-93b8-7822bda4b8a6)

<b>Data Extraction</b></br>
 - The dataset has 28 column with 837 rows, with no any cleaning data.
   - create a loop that requests each movie one at a time and appends the response to a list.
   - send a single GET request to the API, receive a JSON record
{'success': False, 'status_code': 34, 'status_message': 'The resource you requested could not be found.'}

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/a7cf7e76-b5d7-40e1-84c5-4257c360116a)

<b>Data Tranformation</b><br>
 - List of column names we want to work with from the main dataframe df_columns = ["column1", "column2", "column3", ...] # Replace with actual column names
 - Select only the columns specified in df_columns
 - Code for selecting columns from the raw data
 - Save the selected columns to a CSV file
 - Code for saving selected data to a CSV file

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/e875affb-ce04-4c3b-bfcf-1322aad6225a)

<b>Data Loading</b><br>
Define a function to extract the English name of spoken languages def get_spoken_languages(row):
 - Extract the spoken languages information spoken_languages = row['spoken_languages']
 - Check if the spoken_languages field is not empty if spoken_languages:

    - Iterate through the list of dictionaries to find the 'english_name' field for language in spoken_languages: if 'english_name' in language:
        return language['english_name']
    - Return None if 'english_name' is not found return None

 - Apply the function to the 'spoken_languages' column to create a new column with cleaned data
 - df['cleaned_spoken_languages'] = df.apply(get_spoken_languages, axis=1)
 - Save the cleaned and transformed data to a CSV file
 - Code for saving data to a CSV file

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/b806f6a5-aaaf-4ad1-a737-964b039992bd)

Define a function to extract the production country name def get_production_countries(row):
 - Extract the name of the production country production_countries = row['production_countries']
 - Check if the production_countries field is not empty if production_countries:
   
    - Iterate through the list of dictionaries to find the 'name' field with the value 'United Kingdom' for country in production_countries: if 'name' in country and country['name'] == 'United Kingdom':
        return 'United Kingdom'
    - Return None if 'United Kingdom' is not found return None

- Apply the function to the 'production_countries' column to create a new column with cleaned data
- df['cleaned_production_countries'] = df.apply(get_production_countries, axis=1)
- Save the cleaned and transformed data to a CSV file
- Code for saving data to a CSV file
  
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/bb4cc990-9e9d-48a0-b1e8-c0ba30f6dad2)

Define a function to create genre columns def create_genre_columns(row, genres):
 - Extract the genres information movie_genres = row['genres']
 - Initialize a dictionary to store the genre columns genre_columns = {genre['name']: 0 for genre in genres}
 - Check if the genres field is not empty if movie_genres:
   - Iterate through the list of dictionaries to find the 'name' field for genre in movie_genres: if 'name' in genre:
       Set the corresponding genre column to 1 if the movie belongs to that genre
     genre_columns[genre['name']] = 1
   return genre_columns

- List of genres you want to create columns for genre_list = ['Crime', 'Drama', 'Thriller', ...] # Replace with actual genre names
- Apply the function to create genre columns and merge them with the main dataframe
  - genre_columns_df = df.apply(create_genre_columns, axis=1, genres=genre_list)
  - df = pd.concat([df, genre_columns_df], axis=1)
- Save the cleaned and transformed data to a CSV file
- Code for saving data to a CSV file

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/6b06df68-ebb3-4e78-a56c-43f10869f661)

Creat list of unique genres to explode out
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/1d018101-4e75-49c9-8127-9b4658697695)

In the process of preparing our data for analysis or machine learning, we've enhanced our dataset. First, we expanded the list of columns we're working with, including unique genres identified through the get_unique_genres function. Next, we broke down the 'genres_all' column into individual rows, allowing us to represent each movie's genres more granularly. To make this information suitable for analytical and machine learning algorithms, we utilized pd.crosstab to generate binary columns for each unique genre. In this binary representation, a value of 1 indicates that a specific genre is associated with a movie, while a value of 0 indicates its absence. This approach simplifies the categorical genre data, making it easier to process and analyze in our tasks.

 - create a list of column names called df_columns that allows us to select the columns we want from the main dataframe. df_columns = ['title', 'spoken_languages', 'production_countries',
![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/f645dd58-d17a-4b23-912d-26cf44b46d6f)
 - add column genres name df_columns.extend(get_unique_genres(genres_list))
 - break the [genres] into peaces s = df['genres_all'].explode()
 - make 0,1 in to each genres df = df.join(pd.crosstab(s.index, s))

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/1cc31d24-ebba-4490-8ba4-a17577a881a1)

Then finalized the process by persisting the data into a table. The data has been written to CSV files, which are stored in the same directory as my script.

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/17973552-b23e-47d4-89e2-a0368c723c5d)

This is the result from ETL pipeline.

![image](https://github.com/Kanangnut/ETL-pipeline-using-Pandas-in-Python/assets/130201193/07857b58-47a9-4f71-9f5d-f4671e34b26c)

Source: https://www.kaggle.com/code/kanangnuts/etl-pipeline-using-pandas-in-python (My kaggle)









