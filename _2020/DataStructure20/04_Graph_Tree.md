# Graph

그래프는 노드(또는 정점-vertex라고도 불린다), 그리고 노드를 연결해주는 간선(edge)로 구성되어 있다. 그래프에는 무방향(undirected)와 방향성(directed) 그래프가 있다. 진입 차수(In-degree)란 방향 그래프에서 외부 노드에서 오는 간선의 수를 가리킨다 (내차수라고도 불린다). 진출 차수(Out-degree)란 방향 그래프에서 외부 노드로 향하는 간선의 수를 가리킨다 (외차수라고도 불린다). 트리 구조와는 다르게, 그래프에서 노드는 한 개 이상의 In-degree를 가질 수 있다. In-degree가 2개이고, Out-degree가 2개인 방향 그래프를 무방향 그래프라고 한다면, 그냥 4개의 degree가 있다고 말한다. 모든 노드가 간선으로 연결된 그래프를 완전 그래프라 부르고, 그래프의 부분 집합을 부분 그래프라 부른다.
주로 지하철 노선도, 지도 어플의 최단 경로, 페이스북 팔로워 등을 그래프 자료 구조를 사용한다.

![](https://images.velog.io/images/gunwooko/post/220d1cdb-b704-41ba-b9ef-8c6c31558f97/IMG-7176.jpg)

그래프를 구현하는 방식 중에 인접 행렬 방식과 인접 리스트 방식이 있다.

## 인접 행렬 방식 (Adjacency matrix)

인접 행렬 방식은 공간을 많이 차지하지만, 간단하다. 노드의 제곱에 해당하는 공간을 차지하게 된다.

![](https://images.velog.io/images/gunwooko/post/fa235501-0939-40bc-a4df-7f10f68c6762/IMG-7177.jpg)

## 인접 리스트 방식 (Adjacency list)

각각의 노드에 인접한 노드 리스트를 입력하는 방법으로 가장 일반적인 방식이다. 연결 리스트 방식은 공간은 적게 차지하지만 복잡하다. 노드를 새롭게 추가하기가 쉽다.

![](https://images.velog.io/images/gunwooko/post/555d9d7d-67d8-41f4-bcb4-534b21ff508a/IMG-7178.jpg)

## 참고

- [그래프 관련 블로그 1](https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html)
- [그래프 관련 블로그 2](https://jwlee010523.tistory.com/entry/%EA%B7%B8%EB%9E%98%ED%94%84%EC%9D%98-%EC%9D%B4%ED%95%B4%EC%99%80-%EC%A2%85%EB%A5%98)
- [그래프 관련 블로그 3](https://medium.com/@songjaeyoung92/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-javascript-graph-%EB%9E%80-e5d3cd3f50c4)
- [그래프 관련 블로그 4](https://www.zerocho.com/category/Algorithm/post/584b9033580277001862f16c)
- [그래프 관련 블로그 5](https://kingpodo.tistory.com/46)
- [그래프 관련 영상 1](https://www.youtube.com/watch?v=1n5XPFcvxds&list=PLqM7alHXFySEaZgcg7uRYJFBnYMLti-nh)
- [그래프 관련 영상 2](https://www.youtube.com/watch?v=gXgEDyodOJU)
- [칸 아카데미 - 그래프](https://ko.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs)

# Tree

트리 자료 구조는 노드로 구성된 계층적 자료 주고이다.최상위 노트(root)를 만들고, 거기에 노드의 child를 추가하고, 거기에 또 추가하는 방식으로 구현할 수 있다. 노드와 노드를 잇는 선을 edge라 부르고, 자식이 없는 노드를 leaf라 부른다.
루트를 기준으로 다른 노드로의 접근하기 위한 거리를 depth라 부른다. 루트 높이의 깊이는 0이다. 그리고 한 노드를 기준으로 leaf 노드까지의 최대높이를 height라 부른다.
트리 구조의 대표적인 예는 DOM, dictionary, file system 등이 있다.
![](https://images.velog.io/images/gunwooko/post/4ba5bf2f-d943-4b54-8423-04bc360be736/tree%20data%20structure%20.png)
(출처: [코드스테이츠](https://www.codestates.com/))

## BST (Binary Search Tree)

이진 탐색 트리는 최대 2개의 자식 노드만 갖는다. 여기서는 노드의 값의 정렬 방식이 존재하는데, 노드의 왼쪽 서브 트리에는 노드의 값보다 작은 값이, 오른쪽 서브 트리에는 노드의 값과 같거나 큰 값이 들어가게 된다.
![](https://images.velog.io/images/gunwooko/post/fdfe3989-db1c-42b5-b75b-f5ceb22c92cc/eDw57vR.png)
이진 탐색 트리를 순회하는 방법은 크게 깊이 우선 탐색(DFS, Depth First Search)과 너비 우선 탐색(BFS, Breadth First Search) 알고리즘이 있다.

### BST 탐색 방법

- 전위 순회(Preorder Traversal): 부모 -> 좌 -> 우
- 중위 순회(Inorder Traversal): 좌 -> 부모 -> 우
- 후위 순회(Postorder Traversal): 좌 -> 우 -> 부모

### BST의 종류

- 정 이진 트리 (Full Binary Tree)
- 완전 이진 트리 (Completed Binary Tree)
- 포화 이진 트리 (Perfect Binary Tree)

## 참고

- [트리 관련 블로그 1](https://velog.io/@naseriansuzie/imcourseTIL4#5-data-structure---tree)
- [트리 관련 블로그 2](https://www.zerocho.com/category/Algorithm/post/580ed6eb77023c0015ee9686)
- [트리 관련 영상 1](https://www.youtube.com/watch?v=qH6yxkw0u78)
- [BFS-DFS 관련 블로그 1](https://medium.com/@jun.choi.4928/javascript%EB%A1%9C-%ED%8A%B8%EB%A6%AC-bfs-dfs-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-e96bcdadd1f3)
- [BFS-DFS 관련 블로그 2](https://mygumi.tistory.com/102)
- [BFS 관련 블로그 1](https://soldonii.tistory.com/95?category=862199)
- [DFS 관련 블로그 1](https://soldonii.tistory.com/96)
- [BST 관련 블로그 1](https://velog.io/@naseriansuzie/imcourseTIL5)
- [BST 관련 블로그 2](https://velog.io/@rlcjf0014/%EC%9D%B4%EB%A8%B8%EC%8B%9C%EB%B8%8C-5%EC%9D%BC%EC%B0%A8-TIL-5-Data-Structure-Link-Graph-Tree-HashT-qmk35r18cl#%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%9E%98%ED%94%84-%EB%B9%84%EC%84%A0%ED%98%95%EA%B5%AC%EC%A1%B0)
- [BST 관련 블로그 3](https://initjs.org/implement-a-binary-search-tree-in-javascript-952a44ee7c26)
- [BST 관련 영상 1](https://www.youtube.com/watch?v=5cU1ILGy6dM)
