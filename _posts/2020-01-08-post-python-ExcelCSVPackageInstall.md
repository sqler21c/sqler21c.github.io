---
title: "Python-Read/Write Excel, CSV and Package install "
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - Exception
---
## csv읽기
``` python
with open('./src/resource/sample1.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader) # header skip을 하기 위해 사용

    for c in reader:
        print(c)
```
csv파일을 dic으로 변환

```python
with open('./src/resource/sample1.csv', 'r') as f:
    reader = csv.DictReader(f)

    for c in reader:
        for k, v in c.items():
            print(k, v)
        print('===================')
```
실행결과
```
번호 1
이름 김정수
가입일시 2017-01-19 11:30:00
나이 25
```
## csv 쓰기

```python
w = [[1,2,3],[4,5,6],[7,8,9],[10,11,12],[13,14,15],[16,17,18]]

with open('./src/resource/sampel_1.csv', 'w', newline='') as f:
    wt = csv.writer(f)

    for v in w:
        wt.writerow(v)

# ex5
with open('./src/resource/sampel_2.csv', 'w', newline='') as f:
    wt = csv.writer(f)
    wt.writerows(w)
```
## Package Install
exel을 이용할 수 있는 paackage는 주로 **xlrd**, **openpyxl**, **xlswriter**, **xlwt**등 
`pandas`에 xlrd, openpyxl을 주로 사용 함
<pre>
pip install xlrd
pip install openpyxl
pip install pandas
</pre>

사용법
```python
import pandas as pd
# sheetname= '시트명' 또는 '숫자', header=숫자,  skiprow = 숫자
# pandas excel
# xlsx = pd.read_excel('./src/resource/sample.xlsx', skiprow = )
xlsx = pd.read_excel('./src/resource/sample.xlsx')

# 상위 데이터 확인
print(xlsx.head())
print()

# 데이터 확인
print(xlsx.tail())

# data 확인
print(xlsx.shape) # 행, 열

# excel or csr re write
xlsx.to_excel('./src/resource/result.xlsx', index=False)
xlsx.to_csv('./src/resource/result.csv', index=False)
```