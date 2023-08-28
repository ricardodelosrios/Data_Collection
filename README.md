# Data_Collection

## Introduction

In this project, two exercises related to web scraping will be carried out. Which will identify HTML elements, their id and class attributes, and extract information using automated navigation with Splinter and HTML parsing with Beautiful Soup. Additionally, HTML tables will be extracted.

## Folders and files

  * It will find **2 Files** in this project:
  
    * [part_1_mars_news.ipynb](https://github.com/ricardodelosrios/Data_Collection/blob/main/part_1_mars_news.ipynb). In this file you will find the code to extract information from the Mars News website.
    * [part_2_mars_weather.ipynb](https://github.com/ricardodelosrios/Data_Collection/blob/main/part_2_mars_weather.ipynb). You will find the code to scrape and analyze Mars weather data.

* It is going to find a **folder** in this project:

   * The folder called `Outputs` will find 1 CSV file ans 1 json file which were the exportable files of the two exercises. Listed below are the names of the files you will find:

      * [mars_news_list.json](https://github.com/ricardodelosrios/Data_Collection/tree/main/Outputs)
      * [Mars_Temperature.csv](https://github.com/ricardodelosrios/Data_Collection/tree/main/Outputs)
    
## Installation

To run this program you will need to install the following tools to explore and scrape websites, run the following command in the terminal:

it will need to install the `Beautiful Soup` library along with a parser like `lxml` and `html5lib`. You can install these libraries using pip:
```diff
+ pip install beautifulsoup4
+ pip install lxml
+ pip install html5lib
```

Furthermore, it will need to install `Splinter`, a tool that automates our web browser actions, which allows it to automatically scan and repeat interactions on websites.

```diff
+ pip install "splinter[selenium4]"
```

Finally, it will need to install `ChromeDriver`, which enables automation in the Chrome browser. To do so, it will need to follow the [directions](https://splinter.readthedocs.io/en/latest/install/external.html) according with your operating system.

## Analyze and Explore the Climate Data

It was used the files (`climate_starter.ipynb` and `hawaii.sqlite`) to complete your climate analysis and data exploration.

To complete this part of the exercise, the `SQLAlchemy` module is used, which is part of a Python library that is used to work with relational databases in a more efficient and readable way. As you can see below:

```
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, func, inspect

```
Below you will find the explanation of the functions that were used from the sqlalchemy module.

* `automap_base`: This is a part of SQLAlchemy's Object Relational Mapping (ORM) system. It provides a way to automatically map database tables to Python classes.
* `Session`: The Session class is part of SQLAlchemy's ORM system as well. It represents a workspace for your database operations. You create a session when you want to interact with the database, and it keeps track of changes and transactions.
* `create_engine`: This function is used to create a database engine. The engine serves as the foundation for interacting with the database. It establishes a connection to the database and manages database connections and transactions.
* `func`: The func module allows you to use SQL functions in your SQLAlchemy queries. This is especially useful when you need to perform calculations or aggregate data within your queries.
* `inspect`: The inspect module is used to inspect database objects, such as tables, and gather information about them. It can be helpful when you need to dynamically query and analyze the database structure.

If you want to know more about SQLAlchemy you can use the following [documentation](https://docs.sqlalchemy.org/en/20/).

## Design Your Climate App

You will design a Flask API based on the queries you just developed. To do so, use Flask to create your routes as follows:

1. `/`
   * Start at the homepage.
   * List all the available routes.

2. `/api/v1.0/precipitation`
   *Convert the query results from your precipitation analysis (i.e. retrieve only the last 12 months of data) to a dictionary using date as the key and prcp as the value.
   *Return the JSON representation of your dictionary

3. `/api/v1.0/stations`
   *Return a JSON list of stations from the dataset.

4. `/api/v1.0/tobs`
   * Query the dates and temperature observations of the most-active station for the previous year of data.
   * Return a JSON list of temperature observations for the previous year.
  
5. `/api/v1.0/<start>` and `/api/v1.0/<start>/<end>`
