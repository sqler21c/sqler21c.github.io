---
title: "Python-sqlite connection"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - sqlite
  - connection
---
## SQLite Connection Exam
```python

# python database 연동(SQLite)
# table create 및 삽입

import sqlite3
import datetime

# 삽입 날짜 생성
now = datetime.datetime.now()
print("now : ", now)

nowDatatime = now.strftime('%Y-%m-%d %H:%M:%S')
print('nowDatatiem : ', nowDatatime)

# sqlite3
print("sqllite3.version : ", sqlite3.version)
print("sql3.sqlte_version : ", sqlite3.sqlite_version)

# DB 생성 & Auto Commit(commit을 실행 하지 않으면 DB에 반영 되지 않음)
# rollback (이전으로 되돌리기)
# DB for SQLite

conn = sqlite3.connect('e:/Source_Code/fastcamp_exam/python_basic/src/resource/database.db', isolation_level=None)  # auto commit

# auto commit이 아니면
# conn.commit()

c = conn.cursor()
print('currsor type : ', type(c))

# table 생성(Data type : TEXT, NUMERIC, INTEGER, REAR, BLOB)
c.execute('CREATE TABLE IF NOT EXISTS users(id INTEGER PRIMARY KEY, \
                                            username text, \
                                            email text, \
                                            phone text, \
                                            website text, \
                                            regdate text)')

# 데이터 삽입
c.execute("INSERT INTO users VALUES(1, 'KIM', 'kim@dddd.ddd', '000-0000-0000', 'kim.com', ?)", (nowDatatime,))
c.execute("INSERT INTO users(id, username, email, phone, website, regdate) \
           VALUES(?, ?, ?, ?, ?, ?)", (2, 'Lee', 'lee@ddd.ddd', '111-1111-1111', 'lee.com', nowDatatime))
# Many 삽입(tuple, list)
userList = (
    (3, 'Park', 'Park@ddd.ddd', '211-1111-1111', 'park.com', nowDatatime),
    (4, 'cho', 'Park@ddd.ddd', '211-1111-1111', 'park.com', nowDatatime),
    (5, 'ju', 'Park@ddd.ddd', '211-1111-1111', 'park.com', nowDatatime)
)
c.executemany("INSERT INTO users(id, username, email, phone, website, regdate) VALUES(?, ?, ?, ?, ?, ?)",userList)
# data delete
# c.execute("DELETE FROM users")

# delete된 갯수
print("users db deleted : ", c.execute("DELETE FROM users").rowcount)

# commit : isolation_level = None설정시 오토 커밋
# conn.rollback()
conn.close()
```
