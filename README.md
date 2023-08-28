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

The first step is to import the libraries. To run this script, it will need `Splinter` to write web browser automation scripts, `Beautiful Soup`  that is for pulling data out of HTML, and it will use `Json` to export a file.

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

## Mars Weather. How does it work?

The goal of this project is to use a script to analyze Mars weather data and export the DataFrame to a CSV file.

This project imports the libraries and then launches a Chrome web browser, after which, visits the Mars Facts website.

Then, Create a Beautiful Soup object and use it to scrape the data in the HTML table, and extract all rows of data.

To store the data, it creates an empty list, traverses the extracted data to create a list of rows, identifies and prints headers, and stores other rows as data values.

```
# Create an empty list
mars_temperature= []
# Loop through the scraped data to create a list of rows
for row in rows:
    #identify and print headers
    th = row.find_all('th')
    if th:
        headers = [h.text for h in th]
        print(headers)
    
    # Store other rows as data values
    else:
        td = row.find_all('td')
        values = [v.text for v in td]
        mars_temperature.append(values)
```
Create a Pandas DataFrame by using the list of rows and a list of the column names and print it.

```
df = pd.DataFrame(mars_temperature, columns=headers)
mars_table
```
Finally, it will answer the following questions:

1. How many months exist on Mars?
2. How many Martian (and not Earth) days worth of data exist in the scraped dataset?
3. What are the coldest and the warmest months on Mars (at the location of Curiosity)? To answer this question:
   * Find the average the minimum daily temperature for all of the months.
   * Plot the results as a bar chart.
4. Which months have the lowest and the highest atmospheric pressure on Mars? To answer this question:
   * Find the average the daily atmospheric pressure of all the months.
   * Plot the results as a bar chart.
5. About how many terrestrial (Earth) days exist in a Martian year? To answer this question:
   * Consider how many days elapse on Earth in the time that Mars circles the Sun once.
   * Visually estimate the result by plotting the daily minimum temperature.





