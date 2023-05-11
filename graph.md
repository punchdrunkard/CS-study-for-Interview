# Graph

## 정의

객체 사이의 연결관계를 표현할 수 있는 자료구조로 실제 세계의 현상이나 사물을 정점과 간선으로 표현한 것

## 용어

- vertex(or node) : 정점
- edge : 간선
  - directed : 방향이 있는 간선
  - undirected : 방향이 없는 간선
- degree : 정점에 연결된 간선의 수(차수)

## 종류

- Undirected graph(무방향 그래프) : 간선의 방향이 없어 두 정점간 자유롭게 이동이 가능한 그래프
- Directed graph(방향 그래프) : 간선의 방향이 있어 두 정점 중 한쪽 방향으로만 이동이 가능한 그래프

  - In degree : 한 정점으로 들어오는 방향의 간선의 수
  - out degree : 한 정점에서 나가는 방향의 간선의 수

![directed-undirected](https://chamdom.blog/static/43dcc5ebdae930f808c5563ac31f4159/c5bb3/directed-and-undirected.png)

- Weighted graph(가중치 그래프) : 정점과 정점간의 연결강도를 표현한 그래프
- Connected graph(연결 그래프) : 무방향 그래프에 있는 모든 정점에 대해 항상 경로가 존재하는 그래프
- Disconnected graph(비연결 그래프) : 특정 정점에 대한 경로가 없는 그래프
- Complete graph(완전 그래프) : 모든 정점이 서로 다른 정점들과 연결되어 있는 그래프
  - 완전 그래프의 정점 수 → N , 간선 수 → N\*(N-1)/2
- Sub graph(부분 그래프) : 어떤 그래프의 부분 그래프
- Tree는 사이클을 가지지 않는 연결 그래프이며, 모든 정점에 대해 이동할 수 있는 경로가 1개 존재한다.

## 표현 방법

- Adjacency matrix(인접 행렬)

  - 2차원 배열로 각 노드의 연결관계를 표현할 수 있다. (연결 : 1, 연결 안됨 : 0)
  - 정점간의 연결 여부를 O(1)로 파악할 수 있다.
  - 모든 관계를 기록하기 떄문에 정점 수가 많을수록 메모리 낭비가 일어날 수 있다.
    - Space Complexity -> O(V^2)
  - ex) connected = graph[A][B] (정점 A와 정점 B의 연결 여부)
    ![matrix](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1hTUj%2Fbtrr2Tz84x0%2FgzQkMr2lqFo0z3B1SKwwkk%2Fimg.png)

- Adjacency List(인접 리스트)

  - 각 정점당 하나의 리스트나 연결 리스트로 연결관계를 표현할 수 있다.
    - 연결된 경우 : graph[0] = [1,2,3]
    - 연결되지 않은 경우 : graph[1] = []
  - 정점간의 연결 여부를 파악하려면 연결된 정점을 모두 확인해야한다.
  - 연결된 정점들만 저장하기 때문에 메모리 낭비가 없다.

    - Space Complexity -> O(V + E)

    ![List](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdtEp7J%2Fbtrr16z87fn%2Feuc9Rjrb7C64IBkXEK81Bk%2Fimg.png)
