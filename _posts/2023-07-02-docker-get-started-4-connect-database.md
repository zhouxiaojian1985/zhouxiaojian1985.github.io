---
layout: post
title: Docker入门教程4——连接数据库容器
categories: [docker, devops, python, mysql]
description:
keywords:
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

# 运行数据库mysql容器

首先创建一个网络，用于python应用程序容器flask和数据库容器mysql之间的通信。
```
docker network create mysqlnet
7a3cd01d4a766afd374289ed5e93e9b34fb9ff87d35cf6adfdd07a835e285b54
```

运行mysql容器
```
docker run --rm -d -v mysql:/var/lib/mysql \
  -v mysql_config:/etc/mysql -p 3306:3306 \
  --network mysqlnet \
  --name mysqldb \
  -e MYSQL_ROOT_PASSWORD=p@ssw0rd1 \
  mysql

e7f1d53d90cca7d7489d93b70b4e14c687594ce0977ffb4d241fcfee040ccbbf
```

验证mysql可以连接(输入密码p@ssw0rd1)
```
docker exec -it mysqldb mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.33 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

# 连接数据库

修改`app.py`

```
import mysql.connector
import json
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker!'

@app.route('/widgets')
def get_widgets():
    mydb = mysql.connector.connect(
        host="mysqldb",
        user="root",
        password="p@ssw0rd1",
        database="inventory"
    )
    cursor = mydb.cursor()


    cursor.execute("SELECT * FROM widgets")

    row_headers=[x[0] for x in cursor.description] #this will extract row headers

    results = cursor.fetchall()
    json_data=[]
    for result in results:
        json_data.append(dict(zip(row_headers,result)))

    cursor.close()

    return json.dumps(json_data)

@app.route('/initdb')
def db_init():
    mydb = mysql.connector.connect(
        host="mysqldb",
        user="root",
        password="p@ssw0rd1"
    )
    cursor = mydb.cursor()

    cursor.execute("DROP DATABASE IF EXISTS inventory")
    cursor.execute("CREATE DATABASE inventory")
    cursor.execute("USE inventory")

    cursor.execute("DROP TABLE IF EXISTS widgets")
    cursor.execute("CREATE TABLE widgets (name VARCHAR(255), description VARCHAR(255))")

    data = ('test_widget1', 'test widget1')
    cursor.execute("INSERT INTO widgets (name, description) VALUES (%s, %s)", data)
    mydb.commit()

    cursor.close()

    return 'init database'

if __name__ == "__main__":
    app.run(host ='0.0.0.0')
```

- `initdb`: 初始化数据库
- `widgets`: 获取数据库inventory中表widgets的数据

## 更新python-docker镜像

### 使用pip增加python的mysql库
```
pip3 install mysql-connector-python
pip3 freeze | grep mysql-connector-python >> requirements.txt

cat requirements.txt
blinker==1.6.2
click==8.1.3
Flask==2.3.2
importlib-metadata==6.7.0
itsdangerous==2.1.2
Jinja2==3.1.2
MarkupSafe==2.1.3
Werkzeug==2.3.6
zipp==3.15.0
mysql-connector-python==8.0.33
```

### 构建tag是`python-docker-dev`的镜像

```
docker build --tag python-docker-dev .
```

如果`pip`速度慢，可以加上阿里云镜像
```
# syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com

COPY . .

CMD ["python3", "-m" , "flask", "run", "--host=0.0.0.0"]

```

### 运行
```
docker run \
  --rm -d \
  --network mysqlnet \
  --name rest-server \
  -p 8000:5000 \
  python-docker-dev
695ed3748dc865f5480d7f5e89dd4d9cc52430741ceb7478d6cfca2097f0e2da
```

### 验证
```
curl http://localhost:8000/initdb
init database
```

```
curl http://localhost:8000/widgets
[{"name": "test_widget1", "description": "test widget1"}]
```


# 使用dockerc-ompose进行简化

### 构建
```
version: '3.8'

services:
 web:
  build:
   context: .
  ports:
  - 8000:5000
  volumes:
  - ./:/app

 mysqldb:
  image: mysql
  ports:
  - 3306:3306
  environment:
  - MYSQL_ROOT_PASSWORD=p@ssw0rd1
  volumes:
  - mysql:/var/lib/mysql
  - mysql_config:/etc/mysql

volumes:
  mysql:
  mysql_config:

```

### 启动
```
docker-compose -f docker-compose.dev.yml up --build
```

### 验证

```
curl http://localhost:8000/initdb
init database
```

```
curl http://localhost:8000/widgets
[{"name": "test_widget1", "description": "test widget1"}]
```
