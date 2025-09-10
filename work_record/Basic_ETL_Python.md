# Make the ETL process by using Python

Using google collab python and snowflake, i created etl code.

First, enter the identity data in collab secrets
<img width="2129" height="1046" alt="image" src="https://github.com/user-attachments/assets/e137a67a-8212-4f13-8bd6-280a29450b4a" />


Connection code
``` python
import snowflake.connector

def return_snowflake_conn():
    # Snowflake
    conn = snowflake.connector.connect(
        user=user_id,
        password=password,
        account=account,         
        warehouse='compute_wh', 
        database='dev'         
    )
    # Create a cursor object
    return conn.cursor()

```

And define the ETL Function code

Extract code : From csv file, extract data into text 
``` python
import requests

def extract(url):
    f = requests.get(url)
    return (f.text)
```

Transform code : Transform to records that is useful to analyze
``` python
def transform(text):
    lines = text.strip().split("\n")
    records = []
    for l in lines:
      (country, capital) = l.split(",")
      records.append([country, capital])

    return records

```

Load code : load data from transform's result to database on snowflake  
```  python
def load(cur, records):
    target_table = "dev.raw_data.country_capital"
    cur.execute(f"""
    CREATE TABLE IF NOT EXISTS {target_table} (
      country varchar primary key,
      capital varchar
    )""")
    for r in records:
        country = r[0].replace("'", "''")
        capital = r[1].replace("'", "''")
        sql = f"INSERT INTO {target_table} (country, capital) VALUES ('{country}', '{capital}')"
        print(country, "-", capital, "-", sql)
        cur.execute(sql)


```




# How to use?

### Example

``` python
link = "https://s3-geospatial.s3.us-west-2.amazonaws.com/country_capital.csv"

data = extract(link)
lines = transform(data)
lines[0:10]
cur = return_snowflake_conn()
load(cur, lines)
```

However, this can not garuantee the Idempotency

When First Load : 248 rows
<img width="1308" height="763" alt="image" src="https://github.com/user-attachments/assets/71f6be2b-eede-4f64-a5e5-563fa326576f" />


When Second Load wiht same data  : 496 row

<img width="1216" height="773" alt="image" src="https://github.com/user-attachments/assets/e9b244b6-6abc-4889-8f71-c83fd7ee3fbf" />


Next, i will resolve the issue to ensure Idempotency
