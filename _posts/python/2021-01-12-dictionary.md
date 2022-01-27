---
layout: post
title: "Dictionary"
date: 2020-01-12 08:44:38 -0400
category: python
subcategory: 
author: eun
short-description: 키/값 구조로 이루어진 자료형, 딕셔너리
---

### 딕셔너리
파이썬의 **딕셔너리**: 키/값 구조로 이루어진 딕셔너리   

### 다양한 기능과 시간 복잡도
- 입력 순서가 유지되며, 내부적으로 해시 테이블(`Hash Table`)로 구현되어 있다.
- 인덱스를 숫자로만 저장할 수 있는 리스트와 달리 와 달리 숫자 뿐만 아니라 문자, 집합까지 불변 객체로 모두 키로 사용 가능(**해싱**)
- 해시 테이블을 이용해 자료를 저장
- 입력과 조회가 모두 O(1)에 가능
- 최악의 경우 O(n)이 될 수 있으나 대부분 훨씬 빨리 실행됨, 분할 상환 분석에 따른 시간 복잡도는 O(1)

![Image Alt 텍스트](/assets/images/py00_02.png){: width="600" height="200"}

<a href='{{ site.baseurl }}/data-structure/bigO'>시간 복잡도의 정의가 궁금하다면?  **Big-O 개념** 확인하기</a> 

### 활용 방법
[선언방법]
```
a = dict()
a = {}
```
[초기값 지정]
```
a = {'key1':'value1', 'key2':'value2'}
a['key3'] = 'value3'
```
[키값 조회]
```
a['key3']
a['key4'] #KeyError

for k, v in a.items():
    print(k,v)
```
[키값 삭제]
```
del a['key3']
del a['key4'] #KeyError
```

### 딕셔너리 모듈
**defaultdict 객체**       
존재하지 않는 키를 조회할 경우, 에러 메세지를 출력하는 대신 디폴트 값을 기준으로 해당 키에 대한 딕셔너리 아이템을 생성한다
```
a = collections.defaultdict(int)
a['A'] = 5
a['B'] = 4
```
현재 딕셔너리에는 A와 B가 할당되어 있다. 존재하지 않은 C를 정의하면 KeyError가 발생한다. 하지만 defaultdict 객체는 에러 없이 바로 연산이 가능하다.
```
a[C] += 1
a
>>> defaultdict(<class 'int'>, {'A': 5, 'B': 4, 'C': 1})
```
디폴트인 0을 기준으로 자동으로 생성한 후 여기에 1을 더해 최종적으로 value가 1로 저장된다. 

**Counter 객체**    
아이템에 대한 개수를 계산해 딕셔너리로 리턴한다
```
a =[1,2,3,4,5,5,5,6,6]
b = collections.Counter(a)
b
>> Counter({5:3, 6:2, 1:1, 2:1, 3:1, 4:1})
```
이처럼 키에는 아이템의 값이, 값에는 해당 아이템의 개수가 들어간 딕셔너리를 생성한다. 
```
type(b)
>>> <class 'collections.Counter'>
```
실제로 위와 같이 딕셔너리를 한 번 더 래핑한 collections.Counter 클래스를 갖는다.
```
b.most_coomon(2)
>>> [(5,3),(6,2)]
```
most_common()을 사용하면 Counter 객체에서 가장 빈도 수가 높은 요소를 추출할 수 있다.

**OrderDict 객체**      
대부분의 언어에서 해시 테이블을 이용한 자료형은 입력 순서가 유지되지 않는다. 입력 순서가 유지되는 OrderDict라는 별도의 객체를 제공한다
```
collections.OrderDict({'banana':3, 'apple':4, 'pear':1, 'orange'2})
```
하지만 파이썬 3.7부터 딕셔너리는 내부적으로 인덱스를 이용하며 입력 순서가 유지되도록 개선됐다. 따라서 더 이상 OrderDict을 사용할 필요가 없다.