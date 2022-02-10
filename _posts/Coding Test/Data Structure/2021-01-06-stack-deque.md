---
layout: post
title: "Stack, Quque"
date: 2021-02-05 08:44:38 -0400
category:  data-structure
subcategory: 
author: eun
short-description: 가장 고전적인 자료구조, 스택과 큐
---

#### intro
스택은 LIFO(`Last-In-First-Out`), 큐는  FIFO(`First-In-First-Out`)로 처리된다. 

파이썬은 스택 자료형을 별도로 제공하지는 않지만, 리스트가 사실상 스택의 모든 연산을 지원한다. 큐 또한 마찬가지다. 리스트는 큐의 모드 연산을 지원한다. 다만 리스트는 동적 배열로 구현되어 있어 큐 연산을 하기 효율적이지 않다. 때문에 큐를 위해 데크(`Deque`)라는 별도의 자료형을 사용해야 좋은 성능을 낼 수 있다. 


#### Stack
**Stack**: 쌓아 올린다는 것으로, 책을 쌓는 것처럼 차곡차곡 쌓아 올린 형태의 자료구조
- push(): 요소를 컬렉션에 추가
- pop(): 가장 최근에 삽입된 요소 제거       
![Image Alt 텍스트](/assets/images/ct02_01.png){: width="70%" height="70%"}


![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/Stack.ipynb">stack을 list와 linkedlist로 구현한 코드는 깃헙에서 볼 수 있다.</a>


<p style="font-size: 1.12em">📌스택의 특징 </p>
- 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있음
- top: 가장 위에 있는 자료, 즉 가장 최근에 들어온 자료
- top으로 정한 곳을 통해서만 접근 가능
- 새로 삽입되는 자료는 top 위에 쌓이게 됨
- 삭제, 삽입 연산 또한 top을 통해서만 가능
- **LIFO: 가장 마지막에 들어온 자료가 먼저 삭제**

<p style="font-size: 1.12em">📌스택의 활용 예시</p>
스택은 거의 모든 애플리케이션을 만들 때 사용된다.
- 콜 스택: 컴퓨터 프로그램의 서브루틴에 대한 정보 저장하는 자료 구조
- 컴파일러 에러 출력: 맨 마지막 에러가 가장 먼저 출력
- 아키텍처 레벨의 하드웨어 스택: 메모리 영역에서 LIFO 형태로 할당 접근하는 구조
- 스택 버터 오버플로우: 꽉 찬 스택에 요소를 삽입하고자 할 때 스택에 요소가 넘쳐서 에러가 발생하는 것
- 웹 브라우저 방문기록(뒤로가기): 가장 나중에 열린 페이지부터 보여줌
- 실행 취소: 가장 나중에 실행된 것부터 실행 취소


개발자들이 즐겨 이용하는 즐의응답 서비스 사이트인 스택오버플로의 명칭도 여기서 유래됐다.



#### Quque
**Quque**: 줄 서서 기다린다는 것으로, 선입선출 방식의 자료 구조

![Image Alt 텍스트](/assets/images/ct02_02.png){: width="60%" height="60%"}
- 스택과 달리 양방향 작업
- **front**: DeQueue(삭제 연산)만 되는 곳, 가장 첫 원소(가장 먼저 들어온 원소)
- **rear**: EnQueue(삽입 연산)만 되는 곳, 가장 끝 원소(가장 마지막에 들어온 원소)

<p style="font-size: 1.12em">📌큐의 특징 </p>
- rear로 들어오지만 front로 나간다
- 가장 첫 원소와 끝 원소로만 접근 가능
- 파이썬의 리스트는 큐의 모든 연산 지원, 하지만 성능이 좋지 않음
- 연산이 모두 O(1)인 데크를 사용하는 것을 추천

<p style="font-size: 1.12em">📌큐의 활용 예시</p>
- 큐의 변형인 데크나 우선순위 큐는 여러 분야에서 매우 유용함
- BFS이나 캐시 등 구현
- 우선순위가 같은 작업(ex 프린터 인쇄 대기열)
- 은행업무
- 콜센터 고객 대기 시간

#### Circular Queue
**Circular Queue**: 선형큐의 단점을 보완할 수 있는 큐로 원형큐, 링버퍼라고 부른다. 

![Image Alt 텍스트](/assets/images/ct02_05.png){: width="20%" height="20%"}     
- FIFO의 구조
- rear만 데이터 삽입이 가능했던 기존 선형 큐의 단점을 보완한 구조
    + rear, front 모두 데이터 삽입, 삭제 가능
    + dequeue로 인해 발생한 배열의 빈공간 활용 불가
    + 원형큐는 포인터 증가 방식이 (rear+1)&arraysize 형식으로 앞 배열 빈공간에 데이터 삽입 가능
- 마지막 위치가 시작 위치와 연결되는 다음 원형 같은 구조    


[리스트로 구현한 Circular Queue]    
![Image Alt 텍스트](/assets/images/ct02_03.png){: width="60%" height="60%"}     
![Image Alt 텍스트](/assets/images/ct02_06.png){: width="60%" height="60%"}     
![Image Alt 텍스트](/assets/link.png){: width="50" height="50"} <a href="https://github.com/JJungEEun/CodingTest/blob/main/interviews/chap9_%EC%8A%A4%ED%83%9D%2C%ED%81%90/circular%20queue.ipynb">Circular Queue를 구현한 코드는 깃헙에서 볼 수 있다.</a>