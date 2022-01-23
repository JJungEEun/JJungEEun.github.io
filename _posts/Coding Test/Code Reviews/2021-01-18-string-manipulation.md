---
layout: post
title: "String Manipulation(LeetCode)"
date: 2021-01-11 08:44:38 -0400
category: code-reviews
subcategory: 
author: eun
short-description: 문자열을 변경하거나 분리하는 등의 여러 과정(leet code 5, 49, 344, 819, 937)
toc: true
---

문제의 더 자세한 부분이 궁금하다면 leet code를, 더 다양한 나의 코드가 궁금하다면 My code를 누르면 된다 :-)


#### lc 125. Valid Palindrome 
<a href="https://leetcode.com/problems/valid-palindrome/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap6_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EC%A1%B0%EC%9E%91/chap6_1_%EC%9C%A0%ED%9A%A8%ED%95%9C%20%ED%8C%B0%EB%A6%B0%EB%93%9C%EB%A1%AC.ipynb">  My code</a>

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

```
Example 1:
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

---

<mark>팰린드롬</mark>이란 앞뒤가 똑같은 단어나 문장으로 뒤집어도 같은 말이 되는 단어 또는 문장을 의미한다. <br>
예를 들어 'race a car', '소주 만 병만 주소'등이 있다. <br>
이러한 팰린드롬의 특징을 응용하면 여러 가지 재미있는 문제들을 만들 수 있기 때문에 코딩 테스트데 자주 출제된다. 


##### Solution
1. 데이터 전처리(클렌징): 모두 소문자로, 영문자와 숫자만
2. 팰린드롬 여부 판별: 뒤집어서 같은 말인지 확인


##### Code
**My Code**
``` ruby
def isPalindrome(s):
    strs = re.sub(r'[^a-z0-9]', '', s.lower())
    
    return strs == strs[::-1]
```

**Plus Code(Using List)**
```ruby
def isPalindrome(s):
    strs = []
    
    for char in s:
        if char.isalnum(): #isalnum(): 영문자, 숫자 여부 판별 함수
            strs.append(char.lower())
        
    #팰린드롬 여부 판별
    while len(strs) > 1:
        if strs.pop(0) != strs.pop():
            #strs.pop(0): 맨 뒷부분 pop
            return False
        
    return True
```
리스트의 pop()과 pop(0)함수를 사용하여 맨 앞부분과 맨 뒷부분을 매칭하며 일치하지 않을 경우 False를 리턴, 
모두 일치했다면 True를 리턴한다. 

**Plus Code(Using Deque)**
```ruby
def isPalindrome(s):
    #자료형 데크로 선언
    strs: Deque = collections.deque()
    
    for char in s:
        if char.isalnum():
            strs.append(char.lower())
    
    while len(strs) > 1:
        if strs.popleft() != strs.pop():
            return False
        
    return True
```
정규식이나 리스트를 사용하여 문자를 해결할 수 있지만, 데크를 사용하면 속도를 높일 수 있다.
리스트의 pop(0)은 O(n)이지만 데크의 popleft()는 O(1)이다. 
그렇기 때문에 리스트로 구현한 것과 데크로 구현한 것은 성능 차이가 크다. 

##### Part and Parcel
- isalnum(): 영문자, 숫자 여부 판별
- re.sub('찾을 패턴', '찾은 패턴을 변경할 내용', '원본') #^ = not
- list.pop(): 맨 뒷부분 가져오기
- list.pop(0): 맨 앞부분 가져오기
- deque.popleft(): list.pop(0)와 같은 기능


***
<br>


#### lc 344. Reverse String
<a href="https://leetcode.com/problems/reverse-string/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap6_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EC%A1%B0%EC%9E%91/chap6_2_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EB%92%A4%EC%A7%91%EA%B8%B0.ipynb">  My code</a>

Write a function that reverses a string. The input string is given as an array of characters s.

```
Example 1:
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```
---

##### Solution
1. 문자열을 뒤집는다

##### Code
**My code**
```ruby
def reverseString(s):
    s.reverse()
    
    return s
```
파이썬다운 방식을 사용했다. reverse 함수가 아닌 슬라이싱을 사용해서도 코드를 풀이할 수 있다.
s = s[::-1] 을 사용하면 된다. 하지만 이 문제는 공간복잡도를 O(1)으로 제한해서 이 방법을 사용하면 에러가 발생한다. 
이런 경우에는 s[:] = s[::-1]을 사용하면 해결 할 수 있다.

**Plus Code(Using Two Pointer)**

<mark>투 포인터</mark>는 2개의 포인터를 이용해 범위를 조정해가며 풀이하는 방식이다. 

![Image Alt 텍스트](/assets/images/cr00_01.png){: width="400" height="300"}

이 문제에서는 위 그림처럼 점점 더 범위를 좁혀 가며 스왑하는 형태로 풀이할 수 있다. 
```ruby
def reverseString(s):
    left, right = 0, len(s) -1
    
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
        
    return s
```
##### Part and Parcel
- 투 포인터

---
<br>


#### lc 937. Reorder Data in Log Files
<a href="https://leetcode.com/problems/reorder-data-in-log-files/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap6_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EC%A1%B0%EC%9E%91/chap6_3_%EB%A1%9C%EA%B7%B8%20%ED%8C%8C%EC%9D%BC%20%EC%9E%AC%EC%A0%95%EB%A0%AC.ipynb">  My code</a>

You are given an array of logs. Each log is a space-delimited string of words, where the first word is the identifier.

There are two types of logs:
- Letter-logs: All words (except the identifier) consist of lowercase English letters.
- Digit-logs: All words (except the identifier) consist of digits.
Reorder these logs so that:

1. The letter-logs come before all digit-logs.
2. The letter-logs are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
3. The digit-logs maintain their relative ordering.

```
Example 1:
Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
```
---
##### Solution
1. 각 로그를 문자와 숫자로 구분한다.
2. 문자로그를 정렬 기준에 맞춰 재정렬한다
3. 문자로그와 숫자로그를 합친다.

##### Code
**Plus Code(람다와 + 연산자를 이용)**
```ruby
def reorderLogFiles(logs):
    letters, digits = [], []
    
    #문자로그, 숫자로그 구분
    for log in logs:
        if log.split()[1].isdigit():
            digits.append(log)
        else:
            letters.append(log)
    
    #재정렬
    letters.sort(key= lambda x: (x.split()[1:], x.split()[0]))
    #문자로그와 숫자로그 합치기 
    return letters + digits
```
문제 2번 조건을 살펴보면 식별자는 순서에 영향을 미치지 않지만, 문자가 동일하면 식별자 순으로 정렬해야한다. 그래서 람다 표현식을 사용하여 문자로그를 재정렬했다. 먼저 식별자를 제외한 문자열 [1:]을 키로 하여 정렬하고, 동일한 경우 후순위로 식별자 [0]를 지정해 정렬되도록 했다. 

##### Part and Parcel
+ isdigit(): 숫자 여부 판별
+ sort(key= lambda x: 조건): 람다 표현식을 사용하여 정렬

---
<br>

#### lc 819. Most Common Word
<a href="https://leetcode.com/problems/most-common-word/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap6_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EC%A1%B0%EC%9E%91/chap6_4_%EA%B0%80%EC%9E%A5%20%ED%9D%94%ED%95%9C%20%EB%8B%A8%EC%96%B4.ipynb">  My code</a>

Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.

```
Example 1:
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
```
---
##### Solution
1. 데이터 전처리(데이터 클렌징) 및 소문자 변환
2. 딕셔너리 생성(key-단어, value-count)

##### Code
**My Code**
```ruby
def mostCommonWord(paragraph, banned):
    d = {}
    for i in re.sub(r'[^\w]', ' ', paragraph).lower().split():
        if i not in banned:
            if i in d:
                d[i] += 1
            else:
                d[i] = 1
    d = sorted(d, key= lambda x :d[x], reverse=True)

    return d[0]
```

**Plus Code(리스트 컴프리헨션, Counter 객체 사용)**
```ruby
def mostCommonWord(paragraph: str, banned: List[str]) -> str:
    words = [word for word in re.sub(r'[^\w]', ' ', paragraph).lower().split()
                 if word not in banned]

    counts = collections.Counter(words)
    # 가장 흔하게 등장하는 단어의 첫 번째 인덱스 리턴
    return counts.most_common(1)[0][0]
```
내가 짠 코드는 수동으로 count하여 value값에 저장했다. 하지만 Counter 객체를 사용할 시 간단하게 딕셔너리를 생성할 수 있다. 그리고 람다 표현식을 사용하여 정렬하여 가장 높은 value의 key 값을 리턴하는게 아니라 most_common(1)을 사용할 시 간단하게 가장 흔하게 등장하는 단어를 추출할 수 있다 

##### Part and Parcel
+ collections.Counter(): key가 등장하는 빈도수를 value에 저정하는 객체
+ .most_common(1): 가장 흔하게 등장하는 단어의 첫 번째 인덱스 추출

---
<br>

#### lc 49. Group Anagrams
<a href="https://leetcode.com/problems/group-anagrams//">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap6_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EC%A1%B0%EC%9E%91/chap6_5_%EA%B7%B8%EB%A3%B9%20%EC%95%A0%EB%84%88%EA%B7%B8%EB%9E%A8.ipynb">  My code</a>

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

```
Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```
---
##### Solution
애너그램을 판단하는 가장 간단한 방법은 정렬하여 비교하는 것이다. 애너그램 관계의 단어들을 정렬하면 같은 값을 갖기 때문이다. 풀이는 다음과 같다.
1. 단어 정렬하기 
2. 닥셔너리 생성(key: 정렬 단어, value: 같은 정렬 단어를 갖는 단어들)

ex) ["eat", "ate", "tea"] ---> ["aet", "aet", "aet]      
key-"aet" / value-["eat", "ate", "tea"]

##### Code
**My Code**
```ruby
def groupAnagrams(strs):
    words = [''.join(sorted(word)) for word in strs]
    d = collections.defaultdict(list)
    for s, w in zip(strs, words):
        d[w].append(s)
        
    return d.values()
```
sorted()를 이용하여 문자열을 정렬할 경우 결과를 리스트 형태로 리턴한다. 이를 다시 한 단어로 만들기 위해 join() 함수를 사용했다. 존재하지 않은 키를 삽입할 때 KeyError가 발생하지 않도록 딕셔너리의 디폴트 값을 list로 생성했다.

**Plus Code(정렬하여 딕셔너리에 추가)**
```ruby
def groupAnagrams(strs):
    anagrams = collections.defaultdict(list)
    
    for word in strs:
        anagrams[''.join(sorted(word))].append(word)
                
    return list(anagrams.values())
```
내가 짠 코드와 동일한 방식이지만 이처럼 조금 더 간단하게 코드를 정리 할 수 있다.

##### Part and Parcel
+ collections.defaultdict(): 디폴트 값을 지정하여 딕셔너리 생성하기(list, int, string 등)
+ defaultdict을 사용하면 매번 키 존재 여부를 체크하지 않아도 된다
+ sorted()함수를 사용하여 단어를 정렬할 경우 list로 반환하기 때문에 join() 필수

---

<br>

#### lc 5. Longest Palindromic Substring
<a href="https://leetcode.com/problems/longest-palindromic-substring/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap6_%EB%AC%B8%EC%9E%90%EC%97%B4%20%EC%A1%B0%EC%9E%91/chap6_6_%EA%B0%80%EC%9E%A5%20%EA%B8%B4%20%ED%8C%B0%EB%A6%B0%EB%93%9C%EB%A1%AC%20%EB%B6%80%EB%B6%84%20%EB%AC%B8%EC%9E%90%EC%97%B4.ipynb">  My code</a>

Given a string s, return the longest palindromic substring in s

```
Example 1:
Input: s = "babad"
Output: "bab"
```
---
##### Solution
투포인터가 중앙을 중심으로 확장하는 형태로 풀이했다. 팰린드롬을 판별만 하면 된다는 점을 이용하여, 팰린드롬이 매칭이 될 때 중앙을 중심에서 점점 확장하는 방식을 사용했다.

![Image Alt 텍스트](/assets/images/cr00_02.png){: width="300" height="200"}

위 그림처럼 2칸, 3칸으로 구성된 투 포인터가 슬라이딩 왼도우처럼 앞으로 진전한다. 이 투포인터에 있는 문자열이 팰린드롬인 경우 투 포인터가 점점 확장하는 방식이다. bb인 경우도, bab인 경우도 모두 팰린드롬이기 때문에 짝수, 홀수 형태로 처음 포인터를 설정했다. 

![Image Alt 텍스트](/assets/images/cr00_03.png){: width="400" height="300"}

위 그림처럼 포인터가 이동하며 팰린드롬을 판별하고 가장 긴 팰린드롬을 저장하는 방식이다. 


##### Code
**Plus Code(중앙을 중심으로 확장하는 풀이)**
```ruby
def longestPalindrome(s: str) -> str:
    # 팰린드롬 판별 및 투 포인터 확장
        def expand(left: int, right: int) -> str:
            print("1: ", left, right)
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            print("return: ", s[left+1:right])
            return s[left + 1:right]

        # 해당 사항이 없을때 빠르게 리턴
        if len(s) < 2 or s == s[::-1]:
            return s

        result = ''
        # 슬라이딩 윈도우 우측으로 이동
        for i in range(len(s) - 1):
            result = max(result,
                         expand(i, i + 1),
                         expand(i, i + 2),
                         key=len)
        return result
```
---