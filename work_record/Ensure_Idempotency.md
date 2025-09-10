# How to ensure Idempotency

Before INSERT record, delete the all record.
But there are still some issues if error occured when loading process.

Transaction can solve these issues.

# Transaction
Using below !
| BEGIN 
| COMMIT 
| ROLLBACK

create is unrelated to transaction

Edit load function
``` python

def load_v2(con, records):
    target_table = "dev.raw_data.country_capital"
    try:
        con.execute(f"CREATE TABLE IF NOT EXISTS {target_table} (country varchar primary key, capital varchar);")
        con.execute("BEGIN;") # Transaction start! 
        con.execute(f"DELETE FROM {target_table};") # Way to avoid duplication
        for r in records:
            country = r[0].replace("'", "''")
            capital = r[1].replace("'", "''")
            print(country, "-", capital)

            sql = f"INSERT INTO {target_table} (country, capital) VALUES ('{country}', '{capital}')"
            con.execute(sql)
        con.execute("COMMIT;")
    except Exception as e:
        con.execute("ROLLBACK;")
        print(e)
        raise e
```
