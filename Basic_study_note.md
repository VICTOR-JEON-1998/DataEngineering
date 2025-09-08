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
