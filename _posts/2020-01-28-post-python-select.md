---
title: "Python-Select"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - sqlite
  - Select
---
```python
# section12-2
# 파이선 
# 테이블 조회

import sqlite3

# db 파일 조회
conn = sqlite3.connect('e:/Source_Code/fastcamp_exam/python_basic/src/resource/database.db') # 본인 DB경로

# 커서 바인딩
c = conn.cursor()

c.execute("SELECT * FROM users")

# 커서 위치 변경 커서의 역활이 중요함
# 1개 로우 선택
# print("one -> \n", c.fetchone())

# 지정로우 선택
# print("3 --> \n" , c.fetchmany(size=3))

# 전체 로우 선택
# print("all --> \n", c.fetchall())

# rows = c.fetchall()
# 순회 1
# for row in rows:
#     print( 'retrivew 1 > ', row)

# # 순회 2
# for row in  c.fetchall():
#     print("..... retrunv > ", row)

# # 순회 3
# for row in c.execute("SELECT * FROM users ORDER BY id desc"):
#     print("..... retrunv > ", row)

# where retrieve 1
param1 = (3,)

c.execute('SELECT * FROM users WHERE id=?', param1)
print('param1 ', c.fetchone())
print('param1 ', c.fetchall()) # 데이터 없음

# where retrieve 2
param2 = 4

c.execute('SELECT * FROM users WHERE id=%s' % param2)
print('param2 ', c.fetchone())
print('param2 ', c.fetchall()) # 데이터 없음

# where retrieve 3

c.execute('SELECT * FROM users WHERE id=:Id', {"Id": 5})
print('param3 ', c.fetchone())
print('param3 ', c.fetchall()) # 데이터 없음

# WHERE retrieve 4
param4 = (3, 5)
c.execute("SELECT * FROM users WHERE id IN(?,?)", param4)
print('param4 ', c.fetchall())

# WHERE retrieve 5
c.execute("SELECT * FROM users WHERE id IN('%d', '%d')"  %(3, 4))
print('param5 ', c.fetchall())

# WHERE retrieve 6
c.execute("SELECT * FROM users WHERE id=:id1 OR id=:id2", {'id1' : 2, 'id2' : 5})
print('param6 ', c.fetchall())

# dump 출력
with conn:
    with open("e:/Source_Code/fastcamp_exam/python_basic/src/resource/dump.sql", 'w') as f:
        for line in conn.iterdump():
            f.write('%s\n' % line)
        print('dump complete')

# f.close(), conn.close() 호출 됨
```