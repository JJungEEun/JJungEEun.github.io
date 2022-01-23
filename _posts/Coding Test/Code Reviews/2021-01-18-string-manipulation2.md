---
layout: post
title: "String Manipulation(Programmers)"
date: 2021-01-11 08:44:38 -0400
category: code-reviews
subcategory: 
author: eun
short-description: 문자열을 변경하나거나 분리하는 등의 여러 과정(programmers 12903, 12930, 81301. 12925)
toc: true
---

문제의 더 자세한 부분이 궁금하다면 **leet code**를, 더 다양한 나의 코드가 궁금하다면 **My code**를 누르면 된다 :-)

#### 12903. 숫자 문자열과 영단어
(2021 카카오 채용 연계형 인턴쉽)

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://programmers.co.kr/learn/courses/30/lessons/81301">programmers</a>  /  <a href="" id="mycode1">  My code</a>

[문제 설명]     
네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

- 1478 → "one4seveneight"
- 234567 → "23four5six7"
- 10203 → "1zerotwozero3

이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.

참고로 각 숫자에 대응되는 영단어는 다음 표와 같습니다.

|숫자|영단어|
|---|---|
|0|zero|
|1|one|
|2|two|
|3|three|
|4|four|
|5|five|
|6|six|
|7|seven|
|8|eight|
|9|nine|

``` 
입출력 예)
s = "one4seveneight", result = 1478
s = "23four5six7", result =	234567
s = "2three45sixseven", result = 234567
s = "123" result = 123
```
---
##### Solution
1. 영단어와 숫자의 딕셔너리 생성
2. 숫자일 경우 ans에 추가
3. 영어일 경우 단어를 계속 합치며, 딕셔너리에 있는지 확인
    딕셔너리의 key와 일치할 경우 ans에 추가

##### Code

**Code**
```python
def solution(s):
    
    answer = ''
    strs = ''
    dict = {'zero':0, 'one':1, 'two':2, 'three':3, 'four':4, 'five':5, 'six':6, 'seven':7, 'eight':8, 'nine':9}

    for i in s:
        if i.isdigit():
            answer += i
        else:
            strs = strs + i
            if strs in dict.keys():
                answer = answer + str(dict[strs])
                strs =''
        
    return int(answer)
```
딕셔너리의 value는 int고 answer는 str 형태이기 때문에 str로 변환하여 합쳐야한다.    
그러나 result의 형태가 str이 아닌 int이다. 따라서 answer을 int로 변환하여 출력해야한다.

**Plus Code**
```python
def solution(s):
    num_dic = {"zero":"0", "one":"1", "two":"2", "three":"3", "four":"4", "five":"5", "six":"6", "seven":"7", "eight":"8", "nine":"9"}

    for key, value in num_dic.items():
        s= s.replace(key, value)
    return int(s)
```
key값을 value값으로 바꿔주는 replace 메소드를 사용하면 더 간단하게 풀이할 수 있다.

##### Part and Parcel
+ replace(oldvalue, newvalue): oldvalue를 newvalue로 replace한다.

---
<br>

#### 12930. 가운데 글자 가져오기
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://programmers.co.kr/learn/courses/30/lessons/12903"> programmers</a>  /  <a href="">  My code</a>

[문제 설명]     
단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

[제한사항]
- s는 길이가 1 이상, 100이하인 스트링입니다.

``` 
입출력 예
s = "abcde", return = "c"
s= "qwer". return = "we"
``` 
---
##### Solution
1. 문자열의 길이가 짝수인지 홀수인지 판별
2. 슬라이싱을 이용해 가운데 글자 추출

##### Code
**Code**
```python
def solution(s):
    div = int(len(s)/2)
    
    if len(s)%2 == 0:
        return (s[div-1:div+1])
    else:
        return s[div]
```

**Plus Code**
```python
def solution(s):
    return str[(len(str)-1)//2:len(str)//2+1]
```
python의 // Operator을 활용하면 더 간단하게 슬라이싱 할 수 있다.

##### Part and Parcel
- a[i:j]: i부터 j까지 슬라이스의 길이만큼 k개의 요소를 가져온다**(j번째 인덱스는 포함 X)**
- x // y: 버림 나눗셈, 나눗셈 몫(소수점 이하는 버림)

---
<br>

#### 81301. 이상한 문자 만들기
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://programmers.co.kr/learn/courses/30/lessons/12930"> programmers</a>  /  <a href="">  My code</a>

[문제 설명]     
문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

[제한 사항]     
- 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
- 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

``` 
입출력 예
s = "try hello world", return = "TrY HeLlO WoRlD"
```
---
##### Solution
1. 공백을 기준으로 split 하가
2. 짝수는 소문자로, 홀수는 대문자로 바꾸기

##### Code
**Code**
```python
def solution(s):
    answer = []
    s = s.split(' ')

    for i in range(len(s)):
        result = ''
        for j in range(len(s[i])):
            if j % 2 == 0:
                result += s[i][j].upper()
            else:
                result += s[i][j].lower()

        answer.append(result)

    return ' '.join(answer)
```

---
<br>

#### 12925. 문자열을 정수로 바꾸기
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://programmers.co.kr/learn/courses/30/lessons/12925">programers</a>  /  <a href="">  My code</a>

[문제 설명]     
문자열 s를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.

[제한 조건]     
s의 길이는 1 이상 5이하입니다.
s의 맨앞에는 부호(+, -)가 올 수 있습니다.
s는 부호와 숫자로만 이루어져있습니다.
s는 "0"으로 시작하지 않습니다.

``` 
입출력 예
s="1234", return=1234
s="-1234", return=-1234
```
---
##### Solution
1. 숫자로 바꾼다 (.. 너무 간단해서 민망하군요)

##### Code
**Code**
```python
def solution(s):
    return int(s)
```
int()를 사용하면 문제를 간단하게 풀이할 수 있다.      
만약 int()를 사용하지 못한다는 제한 조건이 있다면 어떻게 해야할까?

**Plus Code**
```python
def solution(s):
            
    def StringToNum(number):
        n = 0
        for i, j in enumerate(number):
            n += pow(10,len(number)-i-1) * int(j)
        return n

    if s[0] == "-":
        return StringToNum(s[1:])*(-1)
    elif s[0] == "+":
        return StringToNum(s[1:])
    else:
        return StringToNum(s)
```

다음과 같이 pow() 함수를 이용해 문제를 풀이했다.



