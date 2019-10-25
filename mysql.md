#  MySQL database

## docker version

### Init
```
sudo docker run --name dbname -v /real/path/to/your/workspace/:/path/in/docker/to/workspace/ -v /your/path/:/var/lib/mysql -w /workspace/ -e MYSQL_ROOT_PASSWORD=password -d -p 3306:3306 mysql
```
  - database storate path in docker (default): /var/lib/mysql
### Access into docker
```
sudo docker exec -it dbname bash
```
### Access into mysql (within docker)
```
mysql -u username -p
```


## connect via python
```python
import mysql.connector
from mysql.connector import errorcode

# Connect to Database
config = {
  'user': 'user',
  'password': 'password',
  'host': '127.0.0.1',
  'raise_on_warnings': True
}

cnx = mysql.connector.connect(**config)
cursor = cnx.cursor()
```
```python
# Create Database
def create_database(cursor):
    try:
        cursor.execute(
            "CREATE DATABASE {} DEFAULT CHARACTER SET 'UTF8MB3'".format(DB_NAME))
    except mysql.connector.Error as err:
        print("Failed creating database: {}".format(err))
        exit(1)

try:
    cursor.execute("USE {}".format(DB_NAME))
    print("Database {} exists.".format(DB_NAME))
except mysql.connector.Error as err:
    print("Database {} does not exists.".format(DB_NAME))
    if err.errno == errorcode.ER_BAD_DB_ERROR:
        create_database(cursor)
        print("Database {} created successfully.".format(DB_NAME))
        cnx.database = DB_NAME
    else:
        print(err)
        exit(1)
        
cursor.close()
cnx.close()
```
```python
# general usage
cursor.execute(sql)
cursor.execute(sql,datum)
```

# Pandas + Python + MySQL
## installation
```
pip install mysql-connector-python
pip install SQLAlchemy
```
## usage

```python
import pandas as pd
import sqlalchemy as sql

connect_string = 'mysql+mysqlconnector://user:password@HOST:PORT/DBname'
sql_engine = sql.create_engine(connect_string)

query =query = "show tables"
df = pd.read_sql_query(query, sql_engine)
```

## create table via pandas
```python
userVitals = {"UserId":["xxxxx", "yyyyy", "zzzzz", "aaaaa", "bbbbb", "ccccc", "ddddd"],
            "UserFavourite":["Greek Salad", "Philly Cheese Steak", "Turkey Burger", "Crispy Orange Chicken", "Atlantic Salmon", "Pot roast", "Banana split"],
            "MonthlyOrderFrequency":[5, 1, 2, 2, 7, 6, 1],
            "HighestOrderAmount":[30, 20, 16, 23, 20, 26, 9],
            "LastOrderAmount":[21,20,4,11,7,7,7],
            "LastOrderRating":[3,3,3,2,3,2,4],
            "AverageOrderRating":[3,4,2,1,3,4,3],
            "OrderMode":["Web", "App", "App", "App", "Web", "Web", "App"],
            "InMedicalCare":["No", "No", "No", "No", "Yes", "No", "No"]};
tableName   = "UserVitals"
dataFrame   = pd.DataFrame(data=userVitals) 

############
try:
    dbConnection = sql_engine.connect()
    frame = dataFrame.to_sql(tableName, dbConnection, if_exists='fail');
except ValueError as vx:
    print(vx)
except Exception as ex:
    print(ex)
else:
    print("Table %s created successfully."%tableName);
dbConnection.close()

########
query = "select * from UserVitals"
try:
    df = pd.read_sql_query(query, sql_engine)
except ValueError as vx:
    print(vx)
except Exception as ex:
    print(ex)
else:
    print('successfully executed')
df
```
