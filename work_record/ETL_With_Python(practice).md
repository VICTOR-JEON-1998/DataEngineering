# Make the ETL process by using Python

Using google collab python and snowflake, i created etl code.

First, enter the identity data in collab secrets
<img width="2129" height="1046" alt="image" src="https://github.com/user-attachments/assets/e137a67a-8212-4f13-8bd6-280a29450b4a" />


Connection code
``` python
import snowflake.connector

def return_snowflake_conn():
    # Snowflake 연결 객체 생성
    conn = snowflake.connector.connect(
        user=user_id,
        password=password,
        account=account,        # 예: 'xyz12345.us-east-1' - snowflake 로그인 url에서 앞 부분
        warehouse='compute_wh', # 본인의 설정에 맞게 변경
        database='dev'          # 본인의 설정에 맞게 변경
    )
    # Create a cursor object
    return conn.cursor()

```

Extract code
``` python

```


