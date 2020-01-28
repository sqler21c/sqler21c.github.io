---
title: "Python-Table value delete, edit"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - sqlite
  - CRUD
---
```python
# section12-3
# Table edit, delete

import sqlite3
# DB 생성(파일 생성)
conn = sqlite3.connect('e:/Source_Code/fastcamp_exam/python_basic/src/resource/database.db')

# cursor 연결
c = conn.cursor()

# data 수정 1
c.execute("UPDATE users SET username = ? WHERE id = ? ", ('niceman', 2))

# data 수정 2
c.execute("UPDATE users SET username = :name WHERE id = :id ", {'name': 'goodman', "id" : 5})

# data 수정 3
c.execute("UPDATE users SET username = '%s' WHERE id = '%s' " %("badboy", 3))

#중간 데이터 확인
for user in c.execute("SELECT * FROM users"):
    print(user)
# conn.commit()

# Raw delete 1
c.execute("DELETE FROM users WHERE id = ? ", (2,))

# Raw delete 2
c.execute("DELETE FROM users WHERE id = :id ", {'id':5})

# Raw delete 3
c.execute("DELETE FROM users WHERE id = '%s' " %(4,))

conn.commit()
print()

#중간 데이터 확인
for user in c.execute("SELECT * FROM users"):
    print(user)

# 테이블 전체 데이터 삭제
print("users db deleted : " , conn.execute("DELETE FROm users").rowcount, " rows")

conn.commit()
conn.close()
```