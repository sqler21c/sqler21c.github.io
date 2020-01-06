---
title: "Python-Exception Control Part1"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Post Formats
  - readability
  - standard
---

## Exception?
예외(exception)란 코드를 실행하는 중에 발생한 에러. 다음과 같이 10을 어떤 값으로 나누는 함수 ten_div가 있을 때 인수에 따라 정상으로 동작하기도 하고 에러가 나기도 함

```python
def ten_div(x):
    return 10/x
```
0을 넣으면 runtime error가 남
```python
ten_div(0)
Traceback (most recent call last):
  File "<pyshell#121>", line 1, in <module>
    ten_div(0)
  File "<pyshell#119>", line 2, in ten_div
    return 10 / x
ZeroDivisionError: division by zero 
```
ZeroDivisionError뿐만 아니라 지금까지 만난 AttributeError, NameError, TypeError 등 다양한 에러들도 모두 예외.

예외가 발생했을 때도 스크립트 실행을 중단하지 않고 계속 실행하게 해주는 예외 처리 방법

**try except 사용 하기**
```
try:
    실행할 코드
except:
    예외가 발생했을 때 처리하는 코드
```
0으로 나누었을  때 밣생하는 예외처리
```python
try:
    x = int(input(" input the number : "))
    y = 10 / x
    print(y)
except:
    print("error ")
```
```실행결과 
input the munber : 0(input)
error 
```

**특정 예외만 처리**
```python
try:
    x = int(input(" input the number : "))
    y = 10 / x
    print(y)
except ZeroDivisionError:
    print("ZeroDeivisionError")
except IndexError:
    print("indexError")
except AttributeError:
    print("AttrivuteError")
except NameError:
    print('NameError')
```
**예외 메시지 받아오기**
```python
try:
    x = int(input(" input the number : "))
    y = 10 / x
    print(y)
except ZeroDivisionError as z:
    print("ZeroDeivisionError", z)
except IndexError as i:
    print("indexError", i)
except AttributeError as a:
    print("AttrivuteError", a)
except NameError as n:
    print('NameError', n)
```

> 참고 | 예외 계층
> 
> 예외도 클래스 상속으로 구현되며 다음과 같은 계층으로 이루어져 있습니다. 보통 
> 파이썬에서 새로운 예외를 만들 때는 Exception을 상속받아서 구현합니다.
> 전체 계층도는 파이썬 공식 문서를 참조하세요.
> Built-in Exceptions: [excption-hierarcy](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)
