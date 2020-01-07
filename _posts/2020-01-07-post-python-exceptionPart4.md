---
title: "Python-Exception Control Part4"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - Exception
---
![예외 발생](/assets/images/exception.png)

예외를 만드는 방법은 간단하다. 그냥 Exception을 상속받아서 새로운 쿨래스를 만들면 됨, 
그리고 __init__ 메서드에서 기반 클래서의 __init__ 호출하면서 에러 메시지를 넣어주면 됨.

```python
class exception_name(Exception):
    def __init__(self):
        super().__init()__('error message')
```
예제를 보면
```python
class NoTreeNOOOOOOOOOOOOOO(Exception):
    def __init__(self):
        super().__init__("NotTreeNOOOOOOOO")

def three_mul():
    try:
        x = int(input('3의 배수를 입력하세요: '))
        if x % 3 != 0:                     # x가 3의 배수가 아니면
            raise NoTreeNOOOOOOOOOOOOOO    # NoTreeNOOOOOOOOOOOOOO 예외를 발생시킴
        print(x)
    except Exception as e:
        print('예외가 발생했습니다.', e)
 
three_mul()
```

참고로 다음과 같이 Exception만 상속받고 pass를 넣어서 아무것도 구현하지 않아도 됨.

```python
class NotThreeMultipleError(Exception):    # Exception만 상속받고
    pass                                   # 아무것도 구현하지 않음

raise NotThreeMultipleError('3의 배수가 아닙니다.')    # 예외를 발생시킬 때 에러 메시지를 넣음
```
이때는 예외를 발생시킬 때 에러 메시지를 넣어주면 됨

예외 처리는 에러가 발생하더라도 스크립트의 실행을 중단하지 않고 계속 실행하고자 할 때 사용한다는 점.