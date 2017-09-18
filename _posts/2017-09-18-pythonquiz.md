---
layout: post
title: Python quiz 모음
tags: [개발공부]
description: >
  Python 퀴즈 모음
author: Yamoong
---

9.18일자

1. 1부터 20까지의 정수를 갖는 'result' 리스트를 만들고 슬라이스 연산으로 해당 리스트를 홀수만 가지며 역순이 되도록 하시오.

```python
result = [x for i in range(1,21)]
result_reversed=list.reverse(result[1:19:2])
```

2. today = '우울한 하루'일 때 변수 today를 활기찬 하루 로 만드시오. 단 문자열 내장함수 split과 join 사용하시오

```python

today = '우울한 하루'

today_list=today.split(' ')
today_list[0] = '활기찬'
today = ' '.join(today_list)

```

3. 숫자를 받아 곱을 계산하여 반환하는 myfunc 함수를 만드시오.(숫자가 1개만 들어오면 제곱 2개가 들어오면 두수의 곱 3개 이상 invalid argument 출력)

```python

def myfunc(*args):
  if len(args) == 1:
    return args[0] **2
  elif len(args) == 2:
    return args[0] * args[1]
  else:
    print("Invalid argument")
```

4. 리스트 컴프리헨션을 이용하여 짝수 구구단을 출력하시오


```python
result=['%d x %d = %d' % (x,y,x*y) for x in range(2,10,2) for y in range(1,10) ]
```
