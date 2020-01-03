---
title: "Python-shebang"
excerpt_separator: "<!--more-->"
categories:
  - Python
tags:
  - Post Formats
  - readability
  - standard
---

## shebang이란?
- sharp(#) + bang(!) 합성어
- Unix 계열 OS(Linux, Mac)에서 (bash, python등등) 코드 최상단에서 해당 파일을 해석해줄 interpretor 절대경로를 지정

> #!인터프리터 절대 경로

- 프로그램의 경로는 시스템 경로에따라 달라 질 수 있다.
- 일반적으로 사용할 수 있는 방법이 "/usr/bin/env"파일을 이용 하는 방법이다 "#!/usr/bin/env+언어"
<pre>  
#!/usr/bin/env python \
#!/usr/bin/env bash
</pre>
## env를 사용하여 스크립트 실행하기
쉬뱅을 #!/usr/bin/python2로 설정하면 항상 파이썬2로 실행됩니다. 만약 환경변수에 설정되어있는 파이썬 버전을 사용하고 싶을 수 있습니다.

이럴 때는 #!/usr/bin/env python를 사용해야 합니다.
<pre>
#!/usr/bin/env python
import sys
print("python version: %s"%sys.version_info[0])
</pre>
먼저 테스트를 해볼께요. 현재 저의 환경변수는 파이썬3로 설정되어있습니다.
<pre>
$ python --version 
Python 3.7.0
</pre>
위처럼 쉬뱅을 변경하고 실행하면 파이썬3로 실행되는 것을 볼 수 있습니다. 만약 환경변수를 파이썬2로 변경하면 파이썬2로 실행됩니다.

<pre>
$ ./shebang.py
python version: 3
</pre>
env는 유닉스 및 유닉스 계열 운영 체제용 셸 명령어입니다. 환경 변수의 목록을 출력하거나, 다른 유틸리티를 실행하는데 사용할 수 있습니다.

위의 코드는 env를 이용하여 $PATH에 가장 먼저 검색되는 파이썬 버전으로 스크립트를 실행할 수 있습니다.

## 버전 입력과 env 사용의 장단점
버전을 직접 입력하면 환경변수에 영향을 받지 않고 항상 원하는 인터프리터 버전으로 실행할 수 있습니다. 단점은, 직접 입력한 위치에 인터프리터가 설치되어있지 않다면 실행할 수 없습니다. 다양한 환경에서 실행되는 스크립트의 경우 문제가 있을 수 있습니다.

반면에 env를 사용하면 환경변수에 설정된 인터프리터, 예를들어 파이썬으로 실행할 수 있습니다. 하지만 파이썬을 버전 2로 설치했는지 3으로 설치했는지에 따라서 다르게 동작할 수 있습니다.

그외 쉬뱅이 사용되는 케이스
쉬뱅은 아래와 같은 방식으로 사용되고 있습니다.
<pre>
#!/bin/sh: /bin/sh 경로의 본 셸 또는 호환 셸을 이용하여 파일을 실행 
#!/bin/csh -f: C 셸(csh) 또는 호환 셸을 이용하여 파일을 실행하고, 시작 시 사용자의 .cshrc 파일의 실행을 방지 
#!/usr/bin/perl: T 테인트 검사 옵션으로 펄을 이용하여 실행
</pre>