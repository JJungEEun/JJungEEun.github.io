---
layout: post
title: "Stack, Queue(LeetCode)"
date: 2022-01-11 08:44:38 -0400
category: code-reviews
subcategory: 
author: eun
short-description: 가장 고전적인 자료구조, 스택과 큐(leet code 20, 316, 739, 225, 232, 622, 2130)
toc: true
---

스택과 큐의 개념이 궁금하다면?      
<a href="{{ site.url }}{{ site.baseurl }}/data-structure/stack-deque/">**Stack and Quque**</a>

문제의 더 자세한 부분이 궁금하다면 leet code를, 더 다양한 나의 코드가 궁금하다면 My code를 누르면 된다 :-)

#### lc 20. Valid Parentheses
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/valid-parentheses/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/chap09_20_%EC%9C%A0%ED%9A%A8%ED%95%9C%20%EA%B4%84%ED%98%B8.ipynb">  My code</a>

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
    1. Open brackets must be closed by the same type of brackets.
    2. Open brackets must be closed in the correct order.

```
Example 1:
Input: s = "()"
Output: true
```
```
Example 2:
Input: s = "()[]{}"
Output: true
```
```
Example 3:
Input: s = "(]"
Output: false
```

---

전형적인 스택 문제로, 매우 쉬위면서 기본기를 점검할 수 있는 좋은 문제이다.

##### Solution
1. (,[,{ push
2. ),],} pop


##### Code
**Code**
``` python
def isValid(self, s):
    stack = []
    table = {')':'(', '}':'{', ']':'['} #매핑 테이블
    
    #스택 이용 예외 처리 및 일치 여부 판별
    for char in s:
        if char not in table:
            stack.append(char)
        elif not stack or table[char] != stack.pop():
            return False
        
    return len(stack) == 0 
```

stack은 간편하게 파이썬 동적 배열 구현인 리스트를 사용했다.
파이썬 리스트는 스택 연산인 푸시와 팝이 O(1)에 작동하기 때문에 성능에도 문제가 없다.

Time Submitted | Status | Runtime | Memory
---|---|---|---|
02/03/2022 12:38|Accepted|28ms|13.6MB

***
<br>

#### lc 739. Daily Temperatures
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/daily-temperatures/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/chap09_22_%EC%9D%BC%EC%9D%BC%EC%98%A8%EB%8F%84.ipynb">  My code</a>

Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

```
Example 1:
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```
```
Example 2:
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```
```
Example 3:
Input: temperatures = [30,60,90]
Output: [1,1,0]
```

##### Solution
![Image Alt 텍스트](/assets/images/cr03_01.png){: width="60%" height="60%"}     
1. 스택에 인덱스 push
2. 이전보다 상승하는 지점에서 스택 꺼내 비교하기

![Gif Alt 텍스트](/assets/images/cr03_02.gif)       
예를 들어 인덱스가 5인 지점에서 스택에 [2,3,4]가 있다. 계속 온도가 떨어지고 있어 처리되지 못하고 스택에 쌓여있기 때문이다.
인덱스가 5의 온도는 72, 스택에 있는 2, 3, 4의 온도는 각각 75, 71, 69이다.
72는 71, 69보다 높기 때문에 현재 인덱스에 있는 현재 인덱스와 71의 인덱스는 2칸 차이로 정답은 2가 되고
69의 인덱스는 한 칸차이로 정답은 1이 된다. 

##### Code
**Code**
```python
def dailyTemperatures(self, T):
    stack = []
    ans = [0]*len(T)
    
    for i, t in enumerate(T):
        while stack and t>T[stack[-1]]:
            last = stack.pop()
            ans[last] = i - last
        stack.append(i)
        
    return ans
```

Time Submitted | Status | Runtime | Memory
---|---|---|---|
02/03/2022 16:07|Accepted|1525 ms|19.9 MB


***
<br>

#### lc 225. Implement Stack using Queues
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/implement-stack-using-queues/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/chap09_23_%ED%81%90%EB%A5%BC%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%EC%8A%A4%ED%83%9D%20%EA%B5%AC%ED%98%84.ipynb">  My code</a>

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:
- void push(int x) Pushes element x to the top of the stack.
- int pop() Removes the element on the top of the stack and returns it.
- int top() Returns the element on the top of the stack.
- boolean empty() Returns true if the stack is empty, false otherwise.

```
Example 1:
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

<Explanation>
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
```

##### Solution
1. push: x를 넣고 재정렬
2. top: 맨 앞에 요소가져오기
3. pop: 맨 앞에 꺼내오기
4. empty: 길이 확인하기        

![Image Alt 텍스트](/assets/images/cr03_03.png){: width="20%" height="20%"}  ![Image Alt 텍스트](/assets/images/cr03_04.png){: width="20%" height="20%"}  

##### Code
**Code**
```python
class MyStack(object):
    def __init__(self):
        self.q = collections.deque()

    def push(self, x):
        self.q.append(x)
        for _ in range(len(self.q)-1):
            self.q.append(self.q.popleft())
        

    def pop(self):
        return self.q.popleft()

    def top(self):
        return self.q[0]
        

    def empty(self):
        return len(self.q)==0
```

Time Submitted | Status | Runtime | Memory
---|---|---|---|
02/03/2022 16:21|Accepted|21 ms|13.4 MB


***
<br>

#### lc 232. Implement Queue using Stacks
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/implement-queue-using-stacks/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/chap09_24_%EC%8A%A4%ED%83%9D%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%EC%8A%A4%ED%83%9D%20%EA%B5%AC%ED%98%84.ipynb">  My code</a>

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

- void push(int x) Pushes element x to the back of the queue.
- int pop() Removes the element from the front of the queue and returns it.
- int peek() Returns the element at the front of the queue.
- boolean empty() Returns true if the queue is empty, false otherwise.

```
Example 1:
Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]

<Explanation>
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

##### Solution
2개의 스택을 만든다
1. push: q1에 넣기
2. peek: 뒤집어준 후 맨 마지막 
3. pop: peek()한 후 pop
4. empty: 길이 확인하기   

![Image Alt 텍스트](/assets/images/cr03_05.png){: width="19%" height="19%"}  ![Image Alt 텍스트](/assets/images/cr03_06.png){: width="15%" height="15%"}  ![Image Alt 텍스트](/assets/images/cr03_07.png){: width="15%" height="15%"}  

##### Code
**Code**
```python
class MyQueue(object):

    def __init__(self):
        self.q1 = []
        self.q2 = []

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.q1.append(x)
        

    def pop(self):
        self.peek()
        return self.q2.pop()

    def peek(self):
        if not self.q2:
            while self.q1:
                self.q2.append(self.q1.pop())
        return self.q2[-1]

    def empty(self):
        return len(self.q1)==0 and len(self.q2)==0
```

Time Submitted | Status | Runtime | Memory
---|---|---|---|
02/04/2022 16:00|Accepted|37 ms|13.2 MB


***
<br>

#### lc 622. Design Circular Queue
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/design-circular-queue/">leetcode</a>  /  <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/chap09_25_%EC%9B%90%ED%98%95%ED%81%90%EB%94%94%EC%9E%90%EC%9D%B8.ipynb">  My code</a>

Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Implementation the MyCircularQueue class:
- MyCircularQueue(k) Initializes the object with the size of the queue to be k.
- int Front() Gets the front item from the queue. If the queue is empty, return -1.
- int Rear() Gets the last item from the queue. If the queue is empty, return -1.
- boolean enQueue(int value) Inserts an element into the circular queue. Return true if the operation is successful.
- boolean deQueue() Deletes an element from the circular queue. Return true if the operation is successful.
- boolean isEmpty() Checks whether the circular queue is empty or not.
- boolean isFull() Checks whether the circular queue is full or not.

```
Example 1:
Input
["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
[[3], [1], [2], [3], [4], [], [], [], [4], []]
Output
[null, true, true, true, false, 3, true, true, true, 4]

<Explanation>
MyCircularQueue myCircularQueue = new MyCircularQueue(3);
myCircularQueue.enQueue(1); // return True
myCircularQueue.enQueue(2); // return True
myCircularQueue.enQueue(3); // return True
myCircularQueue.enQueue(4); // return False
myCircularQueue.Rear();     // return 3
myCircularQueue.isFull();   // return True
myCircularQueue.deQueue();  // return True
myCircularQueue.enQueue(4); // return True
myCircularQueue.Rear();     // return 4
```

##### Solution
배열을 이용해 문제를 풀이했다.      

![Image Alt 텍스트](/assets/images/ct02_03.png){: width="60%" height="60%"}     
![Image Alt 텍스트](/assets/images/ct02_06.png){: width="60%" height="60%"}

front와 rear포인터를 사용해 위 그림처럼 구현했다.

##### Code
**Code**
```python
class MyCircularQueue(object):

    def __init__(self, k):
        self.q = [None] * k
        self.maxlen = k
        self.front = 0
        self.rear = 0

    def enQueue(self, value):
        if self.isFull():
            return False
        else:
            self.q[self.rear] = value
            self.rear = (self.rear + 1) % self.maxlen
            return True
            
    def deQueue(self):
        if self.isEmpty():
            return False
        else:
            self.q[self.front] = None
            self.front = (self.front+1) % self.maxlen
            return True
        

    def Front(self):
        if self.isEmpty():
            return -1
        else:
            return self.q[self.front]
        

    def Rear(self):
        if self.isEmpty():
            return -1
        else:
            return self.q[self.rear-1]

    def isEmpty(self):
        return self.front == self.rear and self.q[self.front] is None

    def isFull(self):
        return self.front == self.rear and self.q[self.front] is not None
```
원형 큐의 개념이 궁금하다면?      
<a href="{{ site.url }}{{ site.baseurl }}/data-structure/stack-deque#circular-queue">**Circular Quque**</a>


Time Submitted | Status | Runtime | Memory
---|---|---|---|
02/06/2022 15:43|Accepted|89 ms|13.8 MB


***
<br>

#### lc 2130. Maximum Twin Sum of a Linked List
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/">leetcode</a>  /  <a href="http://localhost:8888/notebooks/Desktop/2022/%EC%BD%94%ED%85%8C%20%EC%8A%A4%ED%84%B0%EB%94%94/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%20%ED%81%90/leetcode%202130.ipynb">  My code</a>

In a linked list of size n, where n is even, the ith node (0-indexed) of the linked list is known as the twin of the (n-1-i)th node, if 0 <= i <= (n / 2) - 1.
- For example, if n = 4, then node 0 is the twin of node 3, and node 1 is the twin of node 2. These are the only nodes with twins for n = 4.
The twin sum is defined as the sum of a node and its twin.

Given the head of a linked list with even length, return the maximum twin sum of the linked list.

```
Example 1:
Input: head = [5,4,2,1]
Output: 6
Explanation:
Nodes 0 and 1 are the twins of nodes 3 and 2, respectively. All have twin sum = 6.
There are no other nodes with twins in the linked list.
Thus, the maximum twin sum of the linked list is 6. 
```
```
Example 2:
Input: head = [4,2,2,3]
Output: 7
Explanation:
The nodes with twins present in this linked list are:
- Node 0 is the twin of node 3 having a twin sum of 4 + 3 = 7.
- Node 1 is the twin of node 2 having a twin sum of 2 + 2 = 4.
Thus, the maximum twin sum of the linked list is max(7, 4) = 7. 
```
```
Example 3:
Input: head = [1,100000]
Output: 100001
Explanation:
There is only one node with a twin in the linked list having twin sum of 1 + 100000 = 100001.
```
##### Solution
![Image Alt 텍스트](/assets/images/cr03_08.png){: width="40%" height="40%"}     

1. slow-fast runner을 사용해 half 배열 만들기
2. half 배열 역순 정렬
3. 기존 배열과 2번에서 만든 배열 더하기

##### Code
**Code**
```python
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
        
class Solution(object):    
    def pairSum(self, head):
        # 역순으로 정렬하기
        def reverse(head):
            node, prev = head, None
            while node:
                next, node.next = node.next, prev
                prev, node = node, next  
                
            return prev
            
        
        ans = []
        slow = head
        fast = head
        
        #배열 반만
        while fast and fast.next:
            print(fast, slow)

            slow = slow.next
            fast = fast.next.next
        rev = reverse(slow)
        
        while rev:
            ans.append(rev.val + head.val)
            head = head.next
            rev = rev.next
            
        ans.sort()
        return ans[-1]
```

Time Submitted | Status | Runtime | Memory
---|---|---|---|
02/06/2022 16:56|Accepted|1756 ms|72.3 MB

