---
title: "Python-Exception Control Part2"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - Exception
---

만약 복수 Exception들이 동일한 except 블럭을 갖는다면, 아래와 같이 이들 Expception들을 하나의 except 문에 묶어서 쓸 수도 있다.
```python
def calc(values):
    sum = None
    try:
       sum = values[0] + values[1] + values[2]
    except (IndexError, ValueError):
        print('오류발생')
 
    print(sum)
```
`에러무시와 에러생성`
발생된 Exception을 그냥 무시하기 위해서는 보통 pass 문을 사용하며, 또한 개발자가 에러를 던지기 위해서는 raise문을 사용한다.

raise 뒤에 아무것도 없는 경우는 현재 Exception을 그대로 던지게 된다. 또한 raise 뒤에 특정한 에러타입과 에러메시지 (Optional)를 넣어 개발자가 정의한 에러를 발생시킬 수 있다. 예를 들어 아래 예제는 raise 뒤에 Exception 에러타입과 에러메시지를 넣어 특별한 에러메시지를 전달하고 있다.

`pass 를 사용한 예`
```python
try:
   check()
except FileExistsError:
    pass
```
`raise 를 사용한 예`
```python
if total < 0:
    raise Exception('Total Error')
```

파일 에러 처리 예제
아래 예제는 전형적인 파일 에러 처리를 보여주는 코드이다. 파일을 오픈할 때 에러가 발생하면, except IOError 블록을 실행한다. 파일오픈을 성공하면, try 블럭을 실행하고, finally 블럭에서 파일을 닫게 된다.

```python
try:
   fp = open("test.txt", "r")
   try:
      lines = fp.readlines()
      print(lines)
   finally:
      fp.close()
except IOError:
   print('파일에러')
```
참고로 다음은 with 문을 써서 해당 블럭이 끝나면 자동으로 파일을 닫는 코드의 예이다. Python의 with 문은 C#의 using 문과 비슷한 것으로 with 블럭이 끝날 때 자동으로 리소스를 해제하는 역활을 하는데, 특히 주목할 점은 with 블럭 내에서 어떤 Exception이 발생하더라도 반드시 리소스를 해제한다는 점이다.
```python
with open('test.txt', 'r') as fp:
    lines = fp.readlines()
    print(lines)
```