# Connectors

## Overview

PandasAI mission is to make data analysis and manipulation more efficient and accessible to everyone. This includes making it easier to connect to data sources and to use them in your data analysis and manipulation workflow.

PandasAI provides a number of connectors that allow you to connect to different data sources. These connectors are designed to be easy to use, even if you are not familiar with the data source or with PandasAI.

To use a connector, you first need to install the required dependencies. You can do this by running the following command:

```console
# Using poetry (recommended)
poetry add pandasai[connectors]
# Using pip
pip install pandasai[connectors]
```

## SQL connectors

PandasAI provides connectors for the following SQL databases:

- PostgreSQL
- MySQL

Additionally, PandasAI provides a generic SQL connector that can be used to connect to any SQL database.

### PostgreSQL connector

The PostgreSQL connector allows you to connect to a PostgreSQL database. It is designed to be easy to use, even if you are not familiar with PostgreSQL or with PandasAI.

To use the PostgreSQL connector, you only need to import it into your Python code and pass it to a `SmartDataframe` or `SmartDatalake` object:

```python
from pandasai.connectors.sql import PostgreSQLConnector

postgres_connector = PostgreSQLConnector(
    config={
        "host": "localhost",
        "port": 5432,
        "database": "mydb",
        "username": "root",
        "password": "root",
        "table": "payments",
        "where": [
            # this is optional and filters the data to
            # reduce the size of the dataframe
            ["payment_status", "=", "PAIDOFF"],
        ],
    }
)

df = SmartDataframe(postgres_connector)
df.chat('What is the total amount of payments in the last year?')
```

### MySQL connector

Similarly to the PostgreSQL connector, the MySQL connector allows you to connect to a MySQL database. It is designed to be easy to use, even if you are not familiar with MySQL or with PandasAI.

To use the MySQL connector, you only need to import it into your Python code and pass it to a `SmartDataframe` or `SmartDatalake` object:

```python
from pandasai.connectors.sql import MySQLConnector

mysql_connector = MySQLConnector(
    config={
        "host": "localhost",
        "port": 3306,
        "database": "mydb",
        "username": "root",
        "password": "root",
        "table": "loans",
        "where": [
            # this is optional and filters the data to
            # reduce the size of the dataframe
            ["loan_status", "=", "PAIDOFF"],
        ],
    }
)

df = SmartDataframe(mysql_connector)
df.chat('What is the total amount of loans in the last year?')
```

### Generic SQL connector

The generic SQL connector allows you to connect to any SQL database that is supported by SQLAlchemy.

To use the generic SQL connector, you only need to import it into your Python code and pass it to a `SmartDataframe` or `SmartDatalake` object:

```python
from pandasai.connectors.sql import SQLConnector

sql_connector = SQLConnector(
    config={
        "dialect": "sqlite",
        "driver": "pysqlite",
        "host": "localhost",
        "port": 3306,
        "database": "mydb",
        "username": "root",
        "password": "root",
        "table": "loans",
        "where": [
            # this is optional and filters the data to
            # reduce the size of the dataframe
            ["loan_status", "=", "PAIDOFF"],
        ],
    }
)
```

## Snowflake connector

The Snowflake connector allows you to connect to Snowflake. It is very similar to the SQL connectors, but it has some differences.

To use the Snowflake connector, you only need to import it into your Python code and pass it to a `SmartDataframe` or `SmartDatalake` object:

```python
from pandasai.connectors.snowflake import SnowFlakeConnector

snowflake_connector = SnowFlakeConnector(
    config={
        "account": "ehxzojy-ue47135",
        "database": "SNOWFLAKE_SAMPLE_DATA",
        "username": "test",
        "password": "*****",
        "table": "lineitem",
        "warehouse": "COMPUTE_WH",
        "dbSchema": "tpch_sf1",
        "where": [
            # this is optional and filters the data to
            # reduce the size of the dataframe
            ["l_quantity", ">", "49"]
        ],
    }
)

df = SmartDataframe(snowflake_connector)
df.chat("How many records has status 'F'?")
```

## Yahoo Finance connector

The Yahoo Finance connector allows you to connect to Yahoo Finance, by simply passing the ticker symbol of the stock you want to analyze.

To use the Yahoo Finance connector, you only need to import it into your Python code and pass it to a `SmartDataframe` or `SmartDatalake` object:

```python
from pandasai.connectors.yahoo_finance import YahooFinanceConnector

yahoo_connector = YahooFinanceConnector("MSFT")

df = SmartDataframe(yahoo_connector)
df.chat("What is the closing price for yesterday?")
```
