# Python with MySQL 
In this Lab, you will learn how to use Python (pandas) for preprocessing your data when Imported from a SQL database and form a csv local file. By the end of this lab, you will be familiar with the connection methods and how you can run SQL Queries using Python.
## Getting Started

### Prerequisites
- Python 3.x
- pandas library
- SQLAlchemy library
- pymysql library
- MySQL database

### Installing
1. Install Python 3.x from [python.org](https://www.python.org/).
2. Install the required libraries using pip:
   ```bash
   pip install pandas pymysql SQLAlchemy

## Running the tests
### Breakdown of Tests
### Part 1: Import CSV File
This part demonstrates how to import a CSV file and filter data based on specific years.
import pandas as pd
input_file_path = r"C:\Users\Durham\Desktop\Duraham\Courses\data1202\vgsales.csv"
input_raw_data = pd.read_csv(input_file_path)
between_00_05 = input_raw_data[(input_raw_data["Year"] >= 2000) & (input_raw_data["Year"] <= 2005)]
print(between_00_05)

### Part 2: Run Simple Queries
This part shows how to connect to a MySQL database and run simple SQL queries.
import pandas as pd
import pymysql
from sqlalchemy import create_engine
engine = create_engine('mysql+pymysql://user10:foo@localhost/ap')
conn = engine.connect()
df = pd.read_sql_query("SELECT * FROM data1202.vgsales", conn)
print(df.head())
print(df.shape)
print(df.size)
print(df.columns)
print(df.dtypes)
print(df.info())

### Part 3: Run Complex Queries
This part demonstrates how to run complex SQL queries to aggregate and analyze data.
complex_df = pd.read_sql_query('''SELECT
    Round(SUM(NA_Sales)) as 'NA_Sales',
    ROUND(SUM(EU_Sales)) as 'EU_Sales',
    ROUND(SUM(JP_Sales)) as 'JP_Sales',
    ROUND(SUM(Global_Sales)) AS 'Global_Sales',
    ROUND((SUM(NA_Sales)/SUM(Global_Sales)) * 100) as 'NA_GlobalShare'
FROM
    data1202.vgsales
WHERE
    Genre = 'Action'
        AND Year>= 2005''', conn)
print(complex_df.head())

### Part 4: WHERE in Python
This part shows how to filter data using pandas.
nintendo_games = df[df['Publisher'] == 'Nintendo']
print(nintendo_games.head())
print("The number of Nintendo games is: " + str(len(nintendo_games)))

df = pd.read_csv(input_file_path)
action_05 = df[(df['Genre'] == 'Action') & (df['Year'] >= 2005)]
print(action_05.head())
print("The max sales of action games in EU after 2005 is: " + str(action_05.EU_Sales.max()))
between_00_05 = df[(df["Year"] >= 2000) & (df["Year"] <= 2005)]
print(between_00_05)

## Deployment
This project does not have a deployment step as it is intended for local analysis and testing.

## Author
Kevin Vania

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgement
Durham College for providing the dataset and support.

