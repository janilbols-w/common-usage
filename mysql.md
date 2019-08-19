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
  'user': 'root',
  'password': 'abc1234',
  'host': '10.246.67.165',
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

