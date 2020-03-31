
- 위상정렬이란?
  * '순서가 정해져 있는 작업'을 차례로 수행할 때 그 순서를 결정해주기 위해 사용하는 알고리즘
  * DAG(Directed Acyclic Graph)에서만 적용 가능. 따라서, 사이클이 발생하지 않는 방향 그래프에서 사용 가능.
  * 구현은 inDegree가 0인 것들을 먼저 queue에 넣고, 나머지 edge에 대해 queue push를 하며 진행한다.
  * 시간복잡도는 정점의 갯수 + 간선의 갯수만큼 소요되기에 O(V + E)
  
- 관련 문제
  * [BOJ 1005 ACM Craft](https://www.acmicpc.net/problem/1005)


- 출처
  * https://m.blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221236874984&proxyReferer=https%3A%2F%2Fwww.google.com%2F
