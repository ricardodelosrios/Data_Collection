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

## Mars News. How does it work?

The goal of this project is to use a script to extract the headlines and preview the text of the news articles it extracted and save the data to a JSON file.

The first step is to import the libraries. To run this script, it will need `Splinter` to write web browser automation scripts, `Beautiful Soup`  that is for pulling data out of HTML.

```
from splinter import Browser
from bs4 import BeautifulSoup as soup
import json
```
Launch a Chrome web browser:

```
browser = Browser('chrome')
```
Visit the Mars news website:

```
url = 'https://static.bc-edx.com/data/web/mars_news/index.html'
browser.visit(url)
html = browser.html
```
A Beautiful Soup object is created and used to extract text elements from the website.

```
text_soup = soup(html, 'html.parser')
```
```
texts = text_soup.find_all('div', class_='list_text')
```
Finally, the headlines are extracted and the text of the news articles is previewed. And the scraping results are stored in a JSON file. To do so, it will do the following steps:

Create an empty list to store the dictionaries:

```
text_list=[]
```
Loop through the text elements and extract the title and preview text from the elements:
```
for t in texts:
    title = t.find(class_='content_title').text.strip()
    preview = t.find(class_='article_teaser_body').text.strip()
```
Store each title and preview pair in a dictionary
```
    dict = {
        'title': title,
        'preview': preview
    }
```
Add the dictionary to the list
```
    text_list.append(dict)
```
Save and print the scraped data to a JSON file:
```
with open('./Outputs/mars_news_list.json', 'w') as file:
    json.dump(text_list, file, indent=3)
    
json_list = json.dumps(text_list, indent=3)
print(json_list)
```

## Mars Weather

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
