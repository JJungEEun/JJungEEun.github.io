---
layout: post
title: "leetcode 5. Longest Palindromic Substring"
date: 2021-01-11 08:44:38 -0400
category: code-reviews
subcategory: 
author: eun
short-description: String Manipulation
toc: true
order: 5
---

문제의 더 자세한 부분이 궁금하다면 leet code를, 더 다양한 나의 코드가 궁금하다면 My code를 누르면 된다 :-)
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