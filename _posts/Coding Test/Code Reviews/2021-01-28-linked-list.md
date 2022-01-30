---
layout: post
title: "Linked List"
date: 2021-01-28 08:44:38 -0400
category: code-reviews
subcategory: 
author: eun
short-description: 연결 리스트 - 데이터 요소의 선형 집합(leet code 234, 21, 206, 2, 24, 328, 92)
toc: true
---

문제의 더 자세한 부분이 궁금하다면 **leet code**를, 더 다양한 나의 코드가 궁금하다면 **My code**를 누르면 된다 :-)

#### lc 234. Palindrome Linked List

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/palindrome-linked-list/">leetcode</a>  /  <a href="" id="mycode1">  My code</a>

Given the head of a singly linked list, return true if it is a palindrome.

``` 
Example 1:
Input: head = [1,2,2,1]
Output: true
```
``` 
Example 2:
Input: head = [1,2]
Output: false
```
---
##### Solution

##### Code
**Code**

**Plus Code**

##### Part and Parcel

---
<br>

#### lc 21. Merge Two Sorted Lists

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/merge-two-sorted-lists/">leetcode</a>  /  <a href="">  My code</a>

You are given the heads of two sorted linked lists list1 and list2.Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists. Return the head of the merged linked list.

``` 
Example 1:
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```
``` 
Example 2:
Input: list1 = [], list2 = []
Output: []
```
``` 
Example 3:
Input: list1 = [], list2 = [0]
Output: [0]
```
---
##### Solution
- Try1) 리스트의 포인터 비교

    ![Image Alt 텍스트](/assets/images/cr02_01.png){: width="850" height="180"}     
    ![Image Alt 텍스트](/assets/images/cr02_04.png){: width="900" height="180"}       
    + 두 리스트의 포인터의 크기를 비교한다.
    1. list1의 포인터가 더 작거나 같은 경우 list1의 포인터 뒤에 list2 포인터 추가
    2. list2의 포인터가 클 경우 list1, list2 바꾸기

    (풀이 실패 이유)     
    ![Image Alt 텍스트](/assets/images/cr02_05.png){: width="400" height="140"}  
    list2의 포인터가 list1의 포인터보다 작다. 그러나 list1의 포인터 뒤에 있는 노드보다 큰 경우 발생 

- Try 2) 새로운 연결리스트에 저장   
    ![Image Alt 텍스트](/assets/images/cr02_03.png){: width="900" height="180"}  
    + 두 리스트의 포인터를 비교해 새로운 연결리스트(cursor)에 저장한다.
       
    1. list1의 포인터가 작거나 같은 경우 cursor에 list1을 저장      
    2. list2의 포인터가 작은 경우 cursor에 list2를 저장

    
##### Code
**Code**
```python
def mergeTwoLists(self, l1, l2):
    head=ListNode(-1)
    cursor=head
    
    while l1 and l2:
        if l1.val <= l2.val:
            cursor.next=l1 # Update next node
            l1=l1.next # Update l1
        else:
            cursor.next=l2 #Update next node
            l2=l2.next # Updata l2
        
        cursor=cursor.next #Move cursor
    
    
    # Last node  
    if l1!=None:
        cursor.next=l1
    else:
        cursor.next=l2
        
    return head.next
```

**Plus Code**
```python
def mergeTwoLists(self, l1, l2):
    if (not l1) or (l2 and l1.val > l2.val):
        l1, l2 = l2, l1

    if l1:
        l1.next = self.mergeTwoLists(l1.next, l2)


    return l1
```
##### Part and Parcel

---
<br>

#### lc 206. Reverse Linked List

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/reverse-linked-list/">leetcode</a>  /  <a href="" id="">  My code</a>

Given the head of a singly linked list, reverse the list, and return the reversed list.

``` 
Example 1:
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```
``` 
Example 2:
Input: head = [1,2]
Output: [2,1]
```
``` 
Example 3:
Input: head = []
Output: []
```
---
##### Solution

##### Code
**Code**

**Plus Code**

##### Part and Parcel

---
<br>

#### lc 2. Add Two Numbers

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/add-two-numbers/">leetcode</a>  /  <a href="" id="mycode1">  My code</a>

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

``` 
Example 1:
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```
``` 
Example 2:
Input: l1 = [0], l2 = [0]
Output: [0]
```
``` 
Example 3:
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```
---
##### Solution

##### Code
**Code**

**Plus Code**

##### Part and Parcel

---
<br>

#### lc 24. Swap Nodes in Pairs

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/swap-nodes-in-pairs/">leetcode</a>  /  <a href="" id="mycode1">  My code</a>

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

``` 
Example 1:
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```
``` 
Example 2:
Input: head = []
Output: []
```
``` 
Example 3:
Input: head = [1]
Output: [1]
```
---
##### Solution

##### Code
**Code**

**Plus Code**

##### Part and Parcel

---
<br>

#### lc 328. Odd Even Linked List

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/odd-even-linked-list/">leetcode</a>  /  <a href="" id="mycode1">  My code</a>

Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The first cursor is considered odd, and the second cursor is evecurscursor so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in O(1) extra space complexity and O(n) time complexity.

``` 
Example 1:
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```
``` 
Example 2:
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]
```
---
##### Solution

##### Code
**Code**

**Plus Code**

##### Part and Parcel

---
<br>

#### lc 92. Reverse Linked List II

![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/reverse-linked-list-ii/">leetcode</a>  /  <a href="" id="mycode1">  My code</a>

Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.

``` 
Example 1:
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```
``` 
Example 2:
Input: head = [5], left = 1, right = 1
Output: [5]
```
---
##### Solution

##### Code
**Code**
```python
def reverseBetween(self, head, left, right):
    start =end= head
    node = tmp =ListNode(None)
    
    for i in range(0, right):
        if i < left-1:
            start= start.next
        end = end.next
    node = end

    for i in range(0, right):
        if i < left-1:
            tmp, tmp.next, head = head, tmp, head.next
        elif left-1<=i and i<=right:
            node, node.next, start = start, node, start.next 
            
    for i in range(left-1):
        node, node.next, tmp = tmp, node, tmp.next 

    return (node)
```
**Plus Code**
```python
def reverseBetween(self, head, m, n):
    # 예외 처리
    if not head or m == n:
        return head

    root = start = ListNode(None)
    root.next = head
    # start, end 지정
    for _ in range(m - 1):
        start = start.next
    end = start.next

    # 반복하면서 노드 차례대로 뒤집기
    for _ in range(n - m):
        tmp, start.next, end.next = start.next, end.next, end.next.next
        start.next.next = tmp
    return root.next
```
##### Part and Parcel