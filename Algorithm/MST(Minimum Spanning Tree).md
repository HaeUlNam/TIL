## 그래프 vs 트리
- 그래프: 노드와 그 노드를 연결하는 간선으로 이루어져 있다.
- 트리의 특징
  - 그래프의 일종
  - Cycle을 가지지 않는다.
  - 계층적 구조를 가진다.
  - 단 하나의 root를 가진다.
  
- 참고 자료: https://shoark7.github.io/insight/rationality/relationship-between-graph-and-tree

## Spanning Tree란?

- 그래프의 최소 연결 부분 그래프이다.
- 즉, n개 vertex에 n-1개의 edge가 있는 것을 뜻한다.

## MST(Minimum Spanning Tree)

- spanning tree 중에 사용된 간선들의 가중치 합이 최소인 것
- 통신망, 도로망 등을 최소의 비용으로 구축하고자 할때 사용된다.

## Prim's 알고리즘

- greedy 알고리즘 중에 하나로서 선택한 노드로부터 가장 작은 weight값을 가지는 edge를 골라나간다.

![스크린샷 2020-04-23 오후 7 51 38](https://user-images.githubusercontent.com/26040955/80091689-786ca580-859c-11ea-9816-fcd07f08014b.png)

- 위와 같은 상태로 그래프가 있다고 하면, 첫번째로 임의의 노드(A) 하나를 정하게 된다.
- 그럼 A를 기준으로 인접한 vertex들은 해당하는 edge 선택하게 된다.
  - B: 7, F: 10, G: 15

- 그 다음 노드는 선택한 edge들의 가중치가 가장 낮은 것(B)을 선택해서 진행한다.
  - C: 12, D: 5, H: 9

- 이와 같은 방식으로 반복적으로 하게 되면 결과는 다음과 같다.
![스크린샷 2020-04-23 오후 8 01 17](https://user-images.githubusercontent.com/26040955/80092122-33953e80-859d-11ea-8fe4-690750a9a70a.png)

- 시간복잡도: O(V)* extract-min + O(E) * decrease-key
  - extract-min: 다음 node를 정할 때, 최소값 뽑는 것
  - decrease-key: 이전에 고른 edge의 weight보다 현재가 더 작을 경우 값을 변경
  - array를 사용할 경우, extract-min은 O(V) / decrease-key는 O(1)
  - binary heap을 사용할 경우, extract-min은 O(logV) / decrease-key는 O(logV)
  - array를 사용할 때 V의 제곱 / binary heap을 사용할 때 VlogV+ ElogV = ElogV이다. 따라서, Edge가 v의 제곱만큼 많다면 array를 쓰는 것이 좀 더 좋고, 
  그렇지 않다면 binary heap을 쓰는 것이 좋을 듯하다.

## 크루스칼 알고리즘
- 그래프의 모든 edge를 정렬시키고, 가장 작은 weight를 가지는 edge 순으로 선택해나가는 방법
여기서 Union-Find 알고리즘을 통해 cycle이 발생하는지 아닌지를 체크하며 진행.

- 시간복잡도 ElogE
- Sparse하다면 크루스칼을 사용하고, Dense하다면 prim's의 Array를 사용하는 것이 더 좋다.




