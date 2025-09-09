# Basic study theory

Data team ‘s role is to make added value by using reliable and high quality data 

data ⇒ decision

we focus on “⇒”

The process !

Data warehouse : Structured (SQL) | Expensive

Data lake : none Structured  | Big and cheap

ETL process : Extract , Transform , Load Data to Lake or warehouse  using pipeline

(Build pipeline is also DE’s job)

Kafka / Kinesis / Pub-sub can ETL in realtime 

Production db must be fast, so this can not be big size

So, we can not use Production db to analyze.

because DB for Analyze must have various data not only essential data, so it is always big size.

warehouse or lake can be DB for analyze 

It is general that make docker image and build the data pipeline on docker container.

Manage Docker container pipeline by K8S

Must have knowledge : Python ,SQL , Airflow

Data Lineage : ETL Flow, Data’s relationship on ETL progress

-------------------------------------------------------------------

Snowflake is data warehouse which is operating on cloud system

It serve data sharing 

Normal data warehouse should load huge data at once, so it is not effective that using INSERT INTO.

COPY INTO is more effective

Snowflake consists of  ||| Cloud service Layer  / Storage Layer / Compute Layer → Completely seperated !


-------------------------------------------------------------------

### Create DATABASE and SCHEMA in snowflake

First, Create SQL worksheet
and create database, schema like this
<img width="1541" height="704" alt="image" src="https://github.com/user-attachments/assets/03b45d66-7061-4315-865a-ac2d15f10dba" />

Generally, Data warehouse does not assure that PK's uniqueness. It just notice user to it is pk, so be carefull.

I should guarantee PK's unique attribute.


CTAS : Create Table ~ AS SELECT 

When Incremental Load, we should use "UPSERT" (No Insert)
Insert can make duplicated issue, but upsert is insert + update. so, upsert only apply the changed things


What will happen if i run the following code?

``` sql
 -- Example of UPSERT in Snowflake

-- Creating the target table
CREATE OR REPLACE TABLE target_table (
    id INT PRIMARY KEY,
    name STRING,
    value INT
);

-- Creating the staging table with new data
CREATE OR REPLACE TABLE staging_table (
    id INT PRIMARY KEY,
    name STRING,
    value INT
);

-- Inserting sample data into target table
INSERT INTO target_table (id, name, value)
VALUES 
    (1, 'Alice', 100),
    (2, 'Bob', 200);

-- Inserting new data into staging table (some new, some existing)
INSERT INTO staging_table (id, name, value)
VALUES 
    (1, 'Alice', 150), -- Existing record with updated value
    (3, 'Charlie', 300); -- New record

-- Performing the UPSERT operation
MERGE INTO target_table AS target
USING staging_table AS stage
ON target.id = stage.id
WHEN MATCHED THEN 
    UPDATE SET 
        target.name = stage.name,
        target.value = stage.value
WHEN NOT MATCHED THEN 
    INSERT (id, name, value)
    VALUES (stage.id, stage.name, stage.value);

SELECT *
FROM target_table;
`
```

<img width="782" height="183" alt="image" src="https://github.com/user-attachments/assets/3fa97fff-5802-4975-831c-98bbef56d5fa" />
