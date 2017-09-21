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
result_reversed=result[-2::2]
```

>답

```python
result = list(range(1,21)) #제일 간단한 방법
result_reversed = result[-2::-2]  # step 사용 방법 = -1을 주면 거꾸로 갈 수 있다.
# 거꾸로 처음부터 끝까지 - [-1::-1]
```

2. today = '우울한 하루'일 때 변수 today를 활기찬 하루 로 만드시오. 단 문자열 내장함수 split과 join 사용하시오

```python


today = '우울한 하루'
today_list=today.split(' ')
today_list[0] = '활기찬'
today = ' '.join(today_list)

```
>답

```python
today = '우울한 하루'
today.split() #아무것도 안 넣으면 공백 - 리스트로 저절로 만들어짐

today[0] = '활기찬'
today=" ".join(today)


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
>답

```python
def myfunc(*args): # 변수개수가 몇개든 받을 것
  length = len(args) #인자의 개수를 변수로 만들어 처리
  if length ==1:
    return args[0] **2
  elif length ==2:
    return args[0]*args[1]
  else:
    print('Invalid arguments') #반환하는 값은 없음.

```


4. 리스트 컴프리헨션을 이용하여 짝수 구구단을 출력하시오


```python
result=['%d x %d = %d' % (x,y,x*y) for x in range(2,10,2) for y in range(1,10) ]
```


9.19일자

1. n개의 숫자를 입력받아 제일 큰 수를 반환하는 'mymax' 함수를 만드시오


```python
def mymax(*args):
  max_args= 0 #특정한 값을 주지 말자. 입력받은 값을 초기값으로 주자.
  max_index =len(args) #무슨 값이 입력될지 모르므로...
  for i in range(0,max_index):
    if max_args < args[i]:
      max_args, args[i] = args[i], max_args

  return max_args
```
>답

```python
def mymax(*args): #순회가능하고 끝이 정해져 있지 않은 객체이므로 for문을 사용
  max_args = args[0] #처음부터 끝까지 비교하므로 비교의 초기값이 필요함 - 처음 값을 주자
  for i in args:
    if max_args<i: #args를 바로 순회하기 때문에 i를 인덱스로 사용할 필요가 없다.
      max_args = i #순회하는 이터러블이 인덱스의 숫자가 아니라 인자들 자체이므로
  return max_args  #i와 max_args를 바로 비교하면 된다.

2. 1번에서 만든 'mymax'함수에서 숫자가 아닌 값을 입력하면 오류가 난다. invalid argument출력하도록

```python

try:
  s =! type(int)
  mymax(s)
except ValueError:다
  print('Invaild arguments')
```

>답

```python
def mymax(*args):
  max_args = args[0]
  try:
    for i in args:
      if max_args<i: # 여기서 str과 int를 비교할 수 없어서 오류가 나는 것!
        max_args = i # 오류가 나는 부분을 파악해서 try로 감싸야 함.
    return max_args  
  except:
    print('Invalid arguments')  #try except를 함수 내부에 집어넣고
                                #try 내부에서 오류가 나면 except로 바로 가므로
                                #Invalid arguments를 출력하도록 만들면 됨.
```



3. mymax 함수에 입력된 인자의 개수를 출력하는 mydecorator를 작상하시오

```python
  def mydecorator(func):
    def innerfunc(*args,**kwargs):
      indexlen =len(*args) + len(**kwargs)
      print('mymax함수의 인자 갯수는 {}입니다.'.format(indexlen))

    return innerfunc
```
>답

```python
# 데코레이터의 기본 구조 - 외우자
def mydecorator(func):
  def innerfunc(*args):
    return func(*args)
  return innerfunc

#인자의 개수 - 즉 args의 len을 출력하면 된다.
  def mydecorator(func):
    def innerfunc(*args):
      print(len(args),"개")
      return func(*args) # 이걸 !!꼭!! 써 주어야 한다. 왜냐하면 !!기존의 함수!!를 실행
    return innerfunc  # 하면서 데코레이터가 동작해야 하므로....

```

9-20일자


1. Monster클래스를 만들고 pikachu, ggobugi 인스턴스끼리 메소드를 사용해 보자.

```python
class Monster():
  """docstring for ."""
  def __init__(self, name, hp, damage):
    self.name = name
    self.hp = hp
    self.damage = damage
  def attack(self, target):
    if isinstance(target, Monster):#객체의 상속관계까지 포함해낼 수 있음
    #혹은 if type(target) is Monster: - 객체의 상속관계까지는 포함하지 못함.
      target.hp -= self.damage)
      print('{}가 {}를 공격해 {}의 피해를 입혔다.'.format(self.name,target.name,self.damage))
    #target.attr가 오류가 뜨지 않는 경우 - 해당 attr를 갖고 있는 경우에만
    #같은 클래스의 인스턴스끼리 엮여서 사용하는 걸 전제로 만들어진 메소드이므로...
      if target.hp <= 0:
        print('{}의 남은 체력 0'.format(target.name))
        print('{}가 죽었다.'.format(target.name))
      else:
        print('{}의 남은 체력 {}'.format(target.name,target.hp))
    else:
      print('같은 몬스터끼리만 싸울 수 있습니다.')
  def __str__(self): # 인스턴스를 print할 때 어떻게 나오는지 만드는 메소드
    return '{}: 공격력 {}'.format(self.name,self.damage)

  @staticmethod
  def make():
    return Monster('피카츄',240, 130)

pikachu=Monster('피카츄',240, 130)
ggobugi=Monster('꼬부기',360, 100)

pikachu.attack(ggobugi)


#In print(instance)    


#In: instance.attack
```

2.


```python

```
