---
title: "[고급알고리즘]그리드 알고리즘"
date: 2025-05-07 14:06:00 +0900
categories: [C/C++ 이론, 고급알고리즘/STL]
tags:
  [
    github,
    자료구조,
    알고리즘,
    C언어,
    C++,
  ]
---

# 그리드 알고리즘

- 눈앞의 이익만을 추구하는 알고리즘
    
    미리 정한 기준에 따라 매번 가장 좋은 선택만 취하는 알고리즘
    
    - 여러 경우 중 하나를 결정해야 할 때마다 그 순간이 최적이라고 생각되는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달하여 해결함.
    - 각 선택의 시점에서 이루어지는 결정은 지역적으로는 최적이지만, 그것들을 계속 수집하여 최종적인 해답을 만들었다고 하여, 그것이 최적이라는 보장은 없다.
    - 일반적으로, 머리속에 떠오르는 생각을 검증 없이 바로 구현하면 Greedy 접근이 된다.
    
    최적화 문제를 해결하는 알고리즘
    

## 입력시

데이터 간의 관계를 고려하지 않음, 수행 과정에서 욕심내어 ‘최소값’ or  ‘최대값’을 가진 데이터 선택 (**’근시안적인 선택’** 이라고 말함)

그리디 알고리즘은 입력 사례를 분할하지 않음

최적의 해를 구하지 않음, 단 최악의 해도 구하진 않음

```
** 거스름 돈이 870원  동전의 개수가 최소가 되도록 거스름 돈을 주는 방법**
 10원짜리 87개를 주는 경우 -> 최악
 50원짜리 17개와 10원짜리 2개를 주는 경우
 100원짜리 8개와 10원짜리 7개를 주는 경우
 100원짜리 8개와 50원짜리 1개, 10원짜리 2개를 주는 경우
 500원짜리 1개와 100원짜리 3개, 50원짜리 1개, 10원짜리 2개를 주는경우 -> 최선
```

 최적의 해답은 동전의 개수가 최소가 되는 집합을 구하는 것

---

# MST (최소 신장 트리)

주어진 가중치 그래프에서 사이클 없이 모든 점들을 연결시킨 트리중 선분들의 **가중치 합이 최소인 트리**

<img width="615" alt="Image" src="https://github.com/user-attachments/assets/d40db63c-b7cb-425e-917a-de33c1e1cbb5" />

최소 신장 트리 (CONT’)

신장트리를 찾으려면 사이클이 없도록 모든점을 연결

→ 점의 개수가 n이면 신장 트리에는 정확히(n-1)개의 선분이 있다.

최소 → 비용적인 측면을 의미

간선의 가중치가 모두 다른값이라면, 최소 신장 트리는 유일

- **크리스컬 알고리즘**

모든 비용을 순차적으로 나열하여, 가장 적은 비용이 드는 간선들을 선택해 나가는 방식

- 크러스컬 알고리즘
    
    최소 신장 트리를 형성하기 위한 알고리즘
    
    간선을 하나씩 선택하면서 최소 신장트리를 형성
    
    모든 간선을 가중치 순으로 정렬한다.
    
    사이클이 생기지 않는 간선을 \V\-1개를 선택한다.
    
    가중치가 가장 작은 선분이 사이클을 만들지 않을 때에만 **욕심내어** 그 선분을  추가시킨다
    
- **프림 알고리즘**

 임의의 꼭지점을 선택하고, 연결된 가장 적은 비용의 정점을 선택하도록 n-1개의 간선을 하나씩 추가시켜 트리를 구성하는 방식

**시간복잡도는 O(mlogm)**

# 프림 알고리즘

모든 꼭지점을 포함하면서 각 변의 비용이 합이 최소가 되는 부분 그래프인 트리

임의의점 하나를 선택한 후,(n-1)개의 선분을 하나씩 추가시켜 트리를 생성

새로운 선분을 추가하면서, 연결시킬때 ‘욕심을 내어서’항상 최소의 가중치로 연결되는 선분을 추가시킴

---

# 그래프

현상과 사물을 vertex(정점)과 간선(edge)로 표현하는것

객체와 그 연관성을 모델링 하는 방법

→ 현실의 많은 문제를 해결하는 알고리즘의 주요 자료구조

- 정점 : 대상 또는 객체를 표현
    
    간선 : 정점들 간의 관계를 표현
    

→두 정점이 간선으로 연결되어 있으면, ‘ 두 정점은 인접하다 ‘ 

- 간선은 두 정점의 관계를 나타냄
    
    두 정점의 관계에 대한 가중치를 부여하여 **관계의 정도를 표현할 수 있음.**
    

그래프는 G라고 표현하고 아래와 같이 표시함

Graph G = ( V,E )

V:정점들의 집합

E: 간선들의 집합

## 간선의 방향성

정점을 연결하는 간성은 방향성을 가질수 있다.

→ 양방향으로 이동 가능(A,B)와 같이 표현

무방향 간선 : 양방향으로 이동가능 (A,B)와 같이표현 || 괄호로 표현

- (A,B) = (B,A)

방향간선 : 한쪽 방향으로만 이동 가능 <A,B>로 표현

- <A,B> ≠ <B,A)

완전 그래프 : 정점의 개수가 V개 일때, 간선의 수는 V(V-1)/2인 그래프

밀집 그래프 : 정점에 많은 수의 간선을 갖는 그래프

희소 그래프 : 정점에 비해 적은 수의 간선을 갖는 그래프

- 간선의 종류에 따른 그래프 분류
    
    무방향 그래프 : 무방향 간선으로 이루어진 그래프
    
    방향 그래프 : 방향 간선이 존재하는 그래프
    
    가중치 그래프 : 간선에 가중치가 부여된 그래프
    
    네트워크 : 방향 그래프 중에 가중치가 부여된 그래프
    

<img width="400" alt="Image" src="https://github.com/user-attachments/assets/7f749f66-6757-4dcb-9bf5-f0bdb536f4e7" />

## 그래프 용어

인접 정점 : 간선에 의해 연결된 정점

차수 : 정점에 연결된 간선의 수

경로 : 정점의 나열로 표현 → 단순경로(0,1,2,3) 사이클(0,1,2,0)

경로의 길이 : 경로를 구성하는데 사용된 간선의수

완전 그래프 : 모든 정점이 연결되어 있는 그래프

<img width="510" alt="Image" src="https://github.com/user-attachments/assets/8f7c7839-ba28-4656-8fe8-8b38a8f4ff8c" />

# 행렬의 표현 장단점 :

표현하기쉽고,이해하기 쉽다.

N^2의 공간이 필요하다는것은 단점이다.

## 가중치가 부여된 방향성이 있는 그래프의 인접 행렬 표현

<img width="575" alt="Image" src="https://github.com/user-attachments/assets/749106a3-f657-4524-9ad9-1d4fff2fcca0" />

# 그래프의 탐색 방법 [2가지]

BFS(너비 우선 탐색),Breadth-First-Search

DFS(깊이 우선 탐색),Depth-First-Search

<img width="364" alt="Image" src="https://github.com/user-attachments/assets/d3da6553-881e-4d8d-b052-f821ad9f651a" />
