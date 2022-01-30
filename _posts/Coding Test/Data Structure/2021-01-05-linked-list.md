---
layout: post
title: "Linked List"
date: 2021-01-05 08:44:38 -0400
category:  data-structure
subcategory: 
author: eun
short-description: 데이터 요소의 선형 집합, 연결 리스트
---

#### intro
연결 리스트는 데이터 요소의 선형 집합으로, 데이터의 순서가 메모리에 물리적인 순서대로 저장되지 않는다. 컴퓨터과학에서 배열과 함께 가장 기본이 되는 대표적인 선형 자료구조 중 하나로 다양한 추상 자료형의 기반이 된다.

#### Linked List
**연결 리스트**는 노드(node)들이 한 줄로 연결되어 있는 방식의 자료구조이다. **노드**는 데이터를 묶음으로, 데이터 필드와 링크 필드로 나뉘어 진다. 제일 맨 앞에 있는 노드를 헤드(head), 제일 끝에 있는 노드를 테일(tail)이라 부른다.

![Image Alt 텍스트](/assets/images/ct01_00.png){: width="150" height="150"}
- 데이터 필드: 리스트의 원소, 즉 데이터 값을 저장하는 곳
- 링크 필드: 다른 노드의 주소값을 저장하는 장소(포인터)

[장점]
- 동적으로 새로운 노드를 삽입하거나 삭제하기 간편
- 연결 구조를 통해 물리 메모리를 연속적으로 사용하지 않아도 돼 관리하기 쉬움
- 데이터를 구조체로 묶어서 포인트로 연결한다는 개념은 다양하기 활용 가능

[단점]
- 배열과 다르게 특정 인덱스에 접근할 수 없음
- 특정 인덱스에 접근 하려면 전체를 순서대로 읽어야 하므로 상수 시간에 접근할 수 없음
    + 탐색시간: O(n) 
    + 아이템 추가, 삭제, 추출 시간: O(1)
- 다음 노드의 위치를 저정하기 위한 추가 메모리 필요


[연결 리스트의 종류]
1. 단일 연결 리스트(`Singly linked list`)
2. 이중 연결 리스트(`Doubly linked list`)
3. 원형 연결 리스트(`Circular linked list`)

#### Singly linked list
**단일 연결 리스트**는 각 노드에 한 개의 데이터 필드와 링크 필드를 가지고 있고, 각 노드의 포인터는 다음 공간을 가르킨다.

[구조]      
![Image Alt 텍스트](/assets/images/ct01_01.png){: width="500" height="80"}

[삽입]      
![Image Alt 텍스트](/assets/images/ct01_02.png){: width="500" height="120"}     
1. 새로운 노드(E)와 다음 노드(C) 연결
2. 현재 노드(B)에 다음 노드로 새로운 노드(E) 연결

[삭제]      
![Image Alt 텍스트](/assets/images/ct01_03.png){: width="500" height="80"}      
1. 이전 노드(B)와 삭제할 노드의 다음 노드(D)와 연결

[삽입 py 코드]
```python
# Node class
class Node:

	# Function to initialise the node object
	def __init__(self, data):
		self.data = data # Assign data
		self.next = None # Initialize next as null


# Linked List class contains a Node object
class LinkedList:

	# Function to initialize head
	def __init__(self):
		self.head = None


	# head에 새 노드 추가 / 시간 복잡도: O(1)
	def push(self, new_data):

		# 1. Allocate the Node & Put in the data
		new_node = Node(new_data)
		# 2. Make next of new Node as head
		new_node.next = self.head
		# 3. Move the head to point to new Node
		self.head = new_node


	# 주어진 노드(prev_node) 뒤에 새 노드 추가 / 시간 복잡도: O(1)
	def insertAfter(self, prev_node, new_data):

		# 1. check if the given prev_node exists
		if prev_node is None:
			print "The given previous node must inLinkedList."
			return

		# 2. create new node &  Put in the data
		new_node = Node(new_data)
		# 3. Make next of new Node as next of prev_node
		new_node.next = prev_node.next
		# 4. make next of prev_node as new_node
		prev_node.next = new_node


	# 맨 뒤 노드에 새 노드 추가 / 시간 복잡도: O(n)
	def append(self, new_data):

		# 1. Create a new node &&  Put in the data
		new_node = Node(new_data)

		# 2. If the Linked List is empty, then make the new node as head
		if self.head is None:
			self.head = new_node
			return

		# 3. Else traverse till the last node
		last = self.head
		while (last.next):
			last = last.next

		# 4. Change the next of last node
		last.next = new_node


	# 연결 리스트 print 
	def printList(self):
		temp = self.head
		while (temp):
			print temp.data,
			temp = temp.next



# Code execution starts here
if __name__=='__main__':
	llist = LinkedList()
	llist.append(6)
	llist.push(7)
	llist.push(1)
	llist.append(4)
	llist.insertAfter(llist.head.next, 8)

	print 'Created linked list is:',
	llist.printList()

>>> 1 7 8 6 4
```

[삭제 py 코드]
```python
# Node class 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

	# head에 새 노드 추가 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # 노드 삭제 
    def deleteNode(self, key): 
        
        # Store head node 
        temp = self.head 

        # If head node itself holds the key to be deleted 
        if (temp is not None): 
            if (temp.data == key): 
                self.head = temp.next
                temp = None
                return

        # Search for the key to be deleted, keep track of the 
        # previous node as we need to change 'prev.next' 
        while(temp is not None): 
            if temp.data == key: 
                break
            prev = temp 
            temp = temp.next

        # if key was not present in linked list 
        if(temp == None): 
            return

        # Unlink the node from linked list 
        prev.next = temp.next

        temp = None


    # 연결 리스트 print 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print (" %d" %(temp.data)), 
            temp = temp.next


# Driver program 
llist = LinkedList() 
llist.push(7) 
llist.push(1) 
llist.push(3) 
llist.push(2) 

print ("Created Linked List: ")
llist.printList() 
llist.deleteNode(1) 
print ("\nLinked List after Deletion of 1:")
llist.printList() 

>>> Created Linked List: 2 3 1 7
>>> Linked List after Deletion of 1: 2 3 7
```

#### Doubly linked list

#### Circular linked list

#### List와 Linked List 비교
