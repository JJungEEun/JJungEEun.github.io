---
layout: post
title: "String Manipulation"
date: 2021-01-11 08:44:38 -0400
category: code-reviews
subcategory: 
author: eun
short-description: 문자열을 변경하거나 분리하는 등의 여러 과정(leet code 5, 49, 344, 819, 937)
toc: true
---

##### <a href="https://leetcode.com/problems/valid-palindrome/">lc 125. Valid Palindrome</a>    

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

```
Example 1:
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

<br>

##### <a href="https://leetcode.com/problems/reverse-string/">lc 344. Reverse String</a> 

Write a function that reverses a string. The input string is given as an array of characters s.

```
Example 1:
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

<br>

##### <a href="https://leetcode.com/problems/reorder-data-in-log-files/">lc 937. Reorder Data in Log Files</a> 
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

<br>

##### <a href="https://leetcode.com/problems/most-common-word/">lc 819. Most Common Word</a> 
Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.

```
Example 1:
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
```

<br>

##### <a href="https://leetcode.com/problems/group-anagrams//">lc 49. Group Anagrams</a>
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

```
Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

<br>

##### <a href="https://leetcode.com/problems/longest-palindromic-substring/">lc 5. Longest Palindromic Substring</a>
Given a string s, return the longest palindromic substring in s

```
Example 1:
Input: s = "babad"
Output: "bab"
```