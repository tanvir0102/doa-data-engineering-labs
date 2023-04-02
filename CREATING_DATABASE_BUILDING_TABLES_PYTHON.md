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
## Let's connect to our database and get the new cursor
```
try:
    conn.close()
except psycopg2.Error as e:
    print(e)

try:
    conn = psycopg2.connect("host=127.0.0.1 dbname=myfirstdb user=postgres password=root")
except psycopg2.Error as e:
    print("Error: could not make connection to the Postgres database")
    print(e)
    
try:
    cur = conn.cursor()
except psycopg2.Error as e:
    print("Error: could not get the curser to the Database")
    print(e)

conn.set_session(autocommit=True)
```
## Create a Table for students which includes below columns
student_id
name
age
gender
subject
marks

```
try:
    cur.execute("CREATE TABLE IF NOT EXISTS students (student_id int, name varchar,\
    age int, gender varchar, subject varchar, marks int);")
except psycopg2.Error as e:
    print("Error: Issue creating table")
    print(e)
```
## Insert two rows in the table
```
try:
    cur.execute("INSERT INTO students (student_id, name, age, gender, subject, marks)\
               VALUES (%s, %s, %s, %s, %s, %s)", \
                (1, "Raj", 23, "Male", "Python", 85))
except psycopg2.Error as e:
    print("Error: Inserting rows")
    print(e)
    
try:
    cur.execute("INSERT INTO students (student_id, name, age, gender, subject, marks)\
               VALUES (%s, %s, %s, %s, %s, %s)", \
                (2, "Priya", 22, "Female", "Python", 86))
except psycopg2.Error as e:
    print("Error: Inserting rows")
    print(e)
 ```
 ## Validate your data was inserted into the table
 ```
 try:
    cur.execute("SELECT * FROM students")
except psycopg2.Error as e:
    print("Error: select *")
    print(e)

row = cur.fetchone()
while row:
    print(row)
    row = cur.fetchone()
```
## And Finally close your cursor and connection.
```
cur.close()
conn.close()
```
