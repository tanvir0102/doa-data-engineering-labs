# PostgreSQL: Creating a database, table and load the data into table using Python
Install PostgreSQL
Python 3.6 or later version
Jupyter Notebook

## Import the library
```
pip install psycopg2
import psycopg2
```
## Create a connection to the database
```
try:
    conn = psycopg2.connect("host=127.0.0.1 dbname=postgres user=postgres password=root")
except psycopg2.Error as e:
    print("Error: could not make connection to the Postgres database")
    print(e)
```
## Use the connection to get the cursor that can be used to execute queries
```
try:
    cur = conn.cursor()
except psycopg2.Error as e:
    print("Error: could not get the curser to the Database")
    print(e)
```
## Set automatic commit to be true so that each action is committed without having to call conn.commit() after each command.
```
conn.set_session(autocommit=True)
```
## Create a database to do the work in
```
try:
    cur.execute("create database myfirstdb")
except psycopg2.Error as e:
    print(e)
```
