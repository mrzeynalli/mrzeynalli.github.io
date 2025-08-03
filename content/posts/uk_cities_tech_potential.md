+++
title = "Non-capital UK Cities with High-tech Potential"
date = 2023-01-05T18:33:53+03:00
draft = false
author = "Elvin Zeynalli"
description = "An analysis of non-capital UK cities with high-tech potential using Companies House API. A data analytics project that identifies decentralized tech hubs in the UK."
tags = ["Data Analytics", "Data Science", "Data Visualization", "Companies House", "API Development", "Web Scraping"]
categories = ["Web Scraping", "Data Analytics"]
+++

**Project description**
- *Language:* Python  
- *Libraries:* requests, pandas, numpy, matplotlib, seaborn, os, math, time, datetime, json  
- *IDE:* Microsoft Visual Studio Code, Jupyter Notebook  
- *Project type:* Data analytics, Web scraping, API

---

[Companies House](https://www.gov.uk/government/organisations/companies-house) is an agency formed by the British Government to maintain the registration of all the companies in the UK. It maintains a database that stores the information of the registered companies. Each company has features such as company name, Standard Industrial Classification (SIC) code, creation date, cessation date (if ceased operating), company board and shareholder info, etc. By using an API, it is possible to scrape the data from that database by using various specifications.

This project aims to scrape the data of the tech companies in the UK and figure out the main tech areas (cities) besides London, the capital of the UK. The idea is to decentralize the tech processes from the capital city. The results of this project can be beneficial for people seeking low-competitive employment in the tech sphere or investors seeking conservative investment options in the UK tech arena.

![Photo by Rodrigo Santos on Unsplash](/images/uk_cities_tech_potential/1.webp)  
*Photo by Rodrigo Santos on Unsplash*

## Data Collection and Cleaning

The project uses the *requests* library to request data from Companies House. The scraped data is converted into *json* format and combined into a single dataframe. The following Python libraries are used:

```python
import pandas as pd
import numpy as np
import requests as rq
import json
import math
import time
import datetime as dt
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')
````

A class-based API caller function was built to collect company data and return it as a dataframe:

```python
class api_caller:
    root_url = 'https://api.companieshouse.gov.uk/'
    key = "YOUR_API_KEY"
    
    def return_dataframe(self, url_extention):
        url = self.root_url + url_extention
        query_result = rq.get(url, auth=(self.key,''))
        if query_result.status_code == 200:
            json_file = json.JSONDecoder().decode(query_result.text)
            items_file = json_file['items']
            keys = items_file[0].keys()
            companies_df = pd.DataFrame(items_file, columns = keys)
            return companies_df
        else:
            return None
```

Full SIC code lists were scraped and processed. A CSV file of SIC codes is available on [my GitHub](https://github.com/mrzeynalli/company_houses_analysis/blob/main/datasets/sic_codes_list.csv).

I created functions to query companies based on single or multiple SIC codes, as well as functions to process address data and extract 'locality' and 'postal\_code' fields from nested dictionaries.

## Data Analysis

I began by extracting SIC codes for tech-related industries using keywords like *'technology'*, *'engineering'*, *'software'*, and *'hardware'*. Duplicate entries were removed. I also extracted city names from company addresses and grouped the data by city (excluding London).

## Data Visualization and Project Results

Using *matplotlib* and *seaborn*, I visualized the distribution of tech companies across non-capital cities in the UK.

*Figure 1: Proportion of Tech Companies in TOP10 Non-Capital Cities of UK*
![Figure 1](/images/uk_cities_tech_potential/2.webp)

Manchester, Birmingham, and Bristol emerge as the top non-capital cities with tech companies, capturing 19.1%, 14.0%, and 10.6% of the share respectively.

*Figure 2: Tech Companies in TOP10 Non-Capital Cities per Company Status*
![Figure 2](/images/uk_cities_tech_potential/3.webp)

Birmingham leads in active tech companies, followed by Manchester and Cambridge.

---

## Conclusion

Manchester, Birmingham, Bristol, and Cambridge are identified as the top non-capital UK cities with high-tech potential. These cities are recommended for individuals seeking less-competitive job markets or investors targeting decentralized tech hubs.