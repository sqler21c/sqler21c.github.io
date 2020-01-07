---
title: "Python-Exception Control Part3"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Python
  - Exception
---

## 예외 발생 시키기
예외를 발생시킬 때는 `raise`에 예외를 지정하고 에러메시지를 넣음(에러 메시지는 생략 가능)

> raise 예외('에러메시지')

```python
try:
    x = int(input(" 3의 배수를 입력 하세요 : "))
    if x % 3 != 0:
        raise Exception('3의 배수가 아님')
    print(x)
except Exception as e:
    print('예외가 발생 했습니다', e)
```
실행 결과는 아래와 같다
```
3의 배수를 입력 하세요 : 5(입력)
예외가 밣생 했습니다 3의 배수가 아닙니다.
```
5는 3의 배수가 아니므로 raise Exception('3의 배수가 아닙니다.')로 예외를 발생시킴. 이때 Exception에 넣은 에러 메시지는 except Exception as e:의 e에 들어감.

그리고 raise로 예외를 발생시키면 raise 아래에 있는 코드는 실행되지 않고 바로 except로 넘어갑니다. 따라서 try의 print(x)는 실행되지 않음

참고로 이 예제에서는 예외로 Exception을 사용했는데 RuntimeError, NotImplementedError 등 다른 예외를 사용해도 상관없다.

## raise 처리 과정
이번에는  raise처리 과정을 알아 보자. 다음은 함수 안에서  raise를 사용 하지만 함수 안에는 try, except가 없는 상태

```python
def tree_mul():
    x = int(input(" 3의 배수를 입력 " ))
    if x % 3 != 0:
        raise Exception('3의 배수가 아님')
    print(x)

try:
    tree_mul()
except Exception as e: 
    print("error :", e)
```
실행 결과 
```
3의 배수를 입력 하세요 : 5(입력)
예외가 밣생 했습니다 3의 배수가 아닙니다.
```
tree_mul함수 안에는 try, except가 없는 상태에서 raise로 예외를 발생, 이렇게 되면 함수 바깥에 있는 except에서 예외처리가 됨, 즉 예외가 발생 하더라도 코드 불록에서 처리해줄 except가 없다면 except가 나올때까지 계속 상위 코드 블록으로 올라 감

만약 함 수 바깥에도 처리해줄 except가 없다면 코드 실행은 중지되고 에러가 표시.

```
>>> three_mul()
3의 배수를 입력하세요: 5 (입력)
Traceback (most recent call last):
  File "<pyshell#5>", line 1, in <module>
    three_multiple()
  File "C:\project\try_except_function_raise.py", line 4, in three_multiple
    raise Exception('3의 배수가 아닙니다.')    # 예외를 발생시킴
Exception: 3의 배수가 아닙니다.
```

## 현재 예외 다시 발생 시키기
이번에는 try, except에서 처리한 예외를 다시 발생 시키는 방법이다, except안에서 raise를 사용하면 현재 예외를 다시 발생(re-raise)

```python
def tree_mul():
    try:
        x = int(input(" 3의 배수를 입력 " ))
        if x % 3 != 0:
            raise Exception('3의 배수가 아님')
        print(x)
    except Exception as e:
        print('tree_mul함수에서 예외 발생', e)
        raise # raise로 현재 예외를 다시 발생시켜서 상위 코드 블록으로 넘김
        raise RuntimeError('RuntimeError') 
              # 다른 예러 미시지를 넣을 수도 있다

try:
    tree_mul()
except Exception as e: 
    print("error :", e)
```
참고로 raise만 사용하면 같은 예외를 상위 코드 블록으로 넘기지만 raise에 다른 예외를 지정하고 에러 메시지를 넣을 수도 있다.

<pre>
참고 || assert로 예외 발생시키기
예외를 발생 기키는 방법 중에는 assert를 사용 하는 방법, 
assert는 지정된 조건식이 거짓일 때 AssertionError예외 발생, 조건식이 참이면 그냥 넘어감
보통 assert는 나와서는 안 되는 조건을 검사할때
assert 조건식
assert 조건식, 에러메시지
<code>
x = int(input('3의 배수를 입력하세요: '))
assert x % 3 == 0, '3의 배수가 아닙니다.' 
# 3의 배수가 아니면 예외 발생, 3의 배수이면 그냥 넘어감
print(x)
</code>
3의 배수를 입력하세요: 5 (입력)
Traceback (most recent call last):
  File "C:\project\assertion.py", line 2, in <module>
    assert x % 3 == 0, '3의 배수가 아닙니다.'
AssertionError: 3의 배수가 아닙니다.
<code>
</code>
assert는 디버깅 모드에서만 실행 됨, 특히 파이션은 기본적으로 디버깅 모드이며 (__debug__의 값이 True) assert가 실행되지 않게 하려면 python -O(대문자 o) 스크립트파일.py
</pre>

