---
layout: post
title: Model field 정리정돈
tags: [개발공부]
description: >
  Model field 정리입니다.
author: Yamoong
---

## Model field reference

 Field는 데이터베이스의 테이블에서 열이다. 필드를 생성하기 위해서는 django의 model 클래스의 속성을 정의하여야 한다.

1. Field options

   필드에 적용하여 필드의 설정들을 변경할 수 있다.

+ null and blank

  `blank`:True 일 때 해당 필드는 빈 값이 들어갈 수 있음. - admin 페이지에 관리하는 옵션

  `null`:True 일 때 데이터베이스에서 빈 값이 오면 null 값이 저장될 수 있음 - 데이터베이스 테이블과 관련된 옵션

+ choices

  길이가 2인 튜플의 리스트 혹은 튜플을 선택지 변수로 저장할 수 있다.


+ db_column

  해당 필드에 사용할 데이터베이 이름. 없으면 필드 변수명을 이름으로 사용. SQL 예약어 사용도 가능

+ db_index

  True일 때 이 필드를 위해 데이터베이스 인덱스를 생성

+ default

  필드의 기본값을 설정. 값 혹은 함수임. 함수라면 인스턴스가 생성될 때마다 실행.

  default 값은 list, set처럼 mutable한 값을 사용할 수 없음. 함수는 모듈 로드시 한 번의 인자를 가져오므로 인스턴스가 한 리스트를 공유하지 않아야 함.

+ editable

  기본은 True이며 해제되어 있을 경우 값을 바꿀 수 없음. admin 페이지나 다른 form에서 보이지 않음.

+ unique

  필드에 고유한 값만이 들어갈 수 있도록 한다.  ManyToManyField, OneToOneField에 사용할 수 없다.

+ primary_key

  필드를 기본 키로 설정한다.  기본키를 설정하지 않으면 고유한 정수를 가지는 id 필드가 생성된다.  

+ unique_for_date

  DateField나 DateTimeField에 사용해서 날짜값이 중복되지 않게 한다. `unique_for_date='pub_date'` 이면 pub_date 값은 인스턴스로 생성될 수 없게 한다.

  year/month - 연과 월이 겹치지 않게 한다.  

+ verbose_name

  관계설정 필드를 제외한 모든 필드타입들은 첫 번째 위치 인자로 문자열을 받을 수 있다. 이 문자열은 필드를 좀 더 구체적으로 나타내는 이름이 된다. verbose_name 을 설정하지 않는 경우, 기본값으로 _ 를 공백문자로 치환한 변수이름이 verbose_name 이 된다.

+ help_text

  필드에 대한 설명을 추가한다.

+ 필드 이름으로 지정할 수 없는 경우

  + Python 예약어
  + 언더스코어 두 개 __ (Django 쿼리셋 문법과 겹침)

2. Field Types

+ AutoField

  적절한 ID 값에 맞게 자동으로 증가하는 정수 필드이다. 이것을 직접적으로 쓸 일은 많이 없는데, 보통 장고에서 이 필드를  사용한 id값을 자동생성하기 때문이다.

+ BooleanField

  True/False 필드이다. 이 필드에 대응되는 기본 form은 CheckboxInput이다. null 값을 받을 필요가 있다면 NullBooleanField를 사용한다.

  기본값을 지정해주지 않으면 None으로 초기화된다.

+ CharField(max_length=None)

  크고 작은 문자열에 대응하는 문자열 필드이다. 긴 글의 경우 `TextField`를 사용한다. 기본 form은 TextInput이다. 그리고 최대 길이를 지정하는 `max_length`인자를 꼭 가져야 한다.

+ DateField(auto_now=False, auto_now_add=False, **options)

  datetime.date 인스턴스가 저장된다. 몇몇 인자를 가지고 있다.

  + auto_now

    인스턴스가 저장될 때마다 자동으로 시간을 새로 지정한다. 최근 수정된 timestamp를 다룰 때 유용하다.

    이 필드는 save() 메서드를 사용할 때마다 자동으로 업데이트 되며, QuerySet.update()와 같이 다른 필드를 업데이트하는 방법으로는 변경되지 않는다.

  + auto_now_add

    객체가 생성되었을 때 값을 업데이트한다. 생성 timestamp를 만들 때 유용하다. 언제나 현재값이 사용되며 오버라이드할 수 없다.

  auto_now_add / auto_now / default는 두 개 이상 같이 사용할 수 없다.

+ DateTimeField

  위의 DateField와 비슷하지만 datetime.datetime의 객체로 시간까지 저장한다.

+ DurationField(**options)

  시간의 경과를 저장하는 필드이다. 파이썬의 `timedelta`를 사용한다. Postgresql을 제외한 모든 데이터베이스에서 DurationField와 DateTimeField는 연산이 되지 않는다.

+ EmailField(max_lengh=)

  값이 적절한 이메일 주소인지 확인하는 CharField다. 값을 검증하기 위해 EmailValidator를 사용한다.

+ FileField(upload_to=None, max_length=100,)

  파일을 업로드하는 필드이다. primary_key와 unique 속성을 받을 수 없다.

+ FloatField

  소수를 표현하는 필드로 파이썬의 `float` 인스턴스를 표현한다. DecimalField와 다르다.

+ ImageField(upload_to=None, height_field=None, width_field=None, max_length)

  FileField의 모든 속성과 메소드를 상속받고, 추가로 적절한 이미지인지도 확인한다. FileField에만 적용되는 특수한 속성과 `height_field` ,`width_field`속성도 가지고 있다.

+ IntegerField

  정수를 담는 필드이다. 양수만을 담는 PositiveIntegerField가 있고, 값이 커진 BigIntegerField가 있다.

+ GenericIPAddressField(protocol='both', unpack_ipv4=False)

  IPv4나 IPv6 주소를 문자열 형식으로 담는 필드이다.

  특수한 인자가 있다.


3. 관계 필드

+ OneToOneField

  필드가 타겟 테이블과 일대일 관계를 맺는다.

  관계 대상 모델과 필드의 레코드 삭제 시 연관되어 삭제되는지 설정이 필요하다.

+ ManyToManyField

  필드가 대상 테이블과 다대다 관계를 맺는다.

+ Foreignkey

  필드를 외래키로 설정한다. 다른 테이블의 레코드와 일대다 관계를 맺는다.

  관계 대상 모델과 필드의 레코드 삭제 시 연관되어 삭제되는지 설정이 필요하다.ㅈ


# QuerySet method

django에서는 model Manager를 이용해서 Queryset 객체나 모델 객체로 데이터를 받는다.



Queryset 사용법

모델 객체를 반환하는 메서드

get(조건)

키워드 인자로 데이터를 찾고, 있으면 그 데이터의 인스턴스 객체를 반환. 없으면 DoesNotExist 예외



count()

데이터의 개수 반환

first()

첫번째 객체 반환

last()

마지막 객체 반환

update()

지정한 필드만 갱신(일부 데이터만 변경하더라도 save()로 저장하면 모델의 필드 전체 변경)

delete()

데이터베이스 삭제

get_or_create(조건, default=)

지정한 데이터를 가져오고 없을 경우 생성.

생성될 데이터의 값은 dict 객체로 지정

update_or_create(조건, default=생성될 데이터의 값)

업데이트하거나 생성



QuerySet 객체를 반환하는 메서드

all()

모든 데이터를 Queryset으로 반환

filter(조건)

조건식으로 데이터를 찾음.
