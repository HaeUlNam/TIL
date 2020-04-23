## 다익스트라
- 다익스트라는 greedy 알고리즘 중 하나로서 음수 weight가 없는 그래프에서 하나의 source로부터 모든 destination의 최단거리를 구할 때 사용한다.
  - greedy인 이유는 iteration이 진행되면서 그 순간에 최적해가 결정되기에 그렇다.
![스크린샷 2020-04-23 오후 10 57 40](https://user-images.githubusercontent.com/26040955/80107275-d6f24d80-85b5-11ea-85b1-3c86437496ef.png)

- 여기서 초기 node를 정하고 모든 vertex에 대해 진행해나가면서, d[v] < d[u] + w(u,v) 이면 해당하는 노드의 최단거리를 변경해주게 된다.

![스크린샷 2020-04-23 오후 10 58 02](https://user-images.githubusercontent.com/26040955/80107330-e4a7d300-85b5-11ea-827f-64a4eb56b77f.png)

1)  // A: 0(초기)
2) A // B: 10 C: 3
3) C // B: 7 D: 11 E: 5
4) E // 변경 X
5) B // D: 9

- 시간복잡도: O(V) * extract-min + O(E) * decrease-key
  - array일 경우 V의 제곱 + E
  - binary heap일 경우 VlogV + ElogV

- 음수의 weight에 있는 그래프에서 사용불가.
  - 이유: greedy 개념이기에 이전까지 거쳐 온 노드들이 최단거리임이 보장되어야 하는데(greedy property), 음수 가중치가 있으면 예외 경우가 생기기에 사용할 수 없다.
- 만약 weight가 없는 그래프의 경우 BFS와 동일

## 벨만포드
- DP 알고리즘 적용한 것으로 다익스트라와 동일하게 하나의 source로부터 모든 destination의 최단거리를 구할 때 사용하는데, 특히 음수 가중치가 존재할 때 사용할 수 있다.
- optimal substructure에 의해 D(s,v) = D(s,u) + w(u,v)를 만족한다.
- 벨만포드 알고리즘은 간단하게 V - 1번 edge relaxation해주면 된다. 그 후 음수 cycle이 있는지 확인하기 위해 한번 더 edge relaxation을 진행해주는데, 이때 
값이 변경되면 음수 사이클이 있기에 최단거리를 구할 수 없다.
  - V - 1번 시행하는 이유: 그래프가 줄처럼 늘어져있는 형태로 되어있다면 V - 1번은 시행해야 최단거리를 구할 수 있기 때문이다.
  - 음수 사이클이 있으면 최단거리를 구할 수 없는 이유: 이렇게 되면 optimal substructure가 만족하지 않기에, 제대로 된 최단거리를 구할 수 없다.

- 시간복잡도: O(V*E)
- 다익스트라보다 시간복잡도가 느리다.

  
  
  
  
### 참고하면 좋을 자료
- 다익스트라: https://www.youtube.com/watch?v=XB4MIexjvY0
- 벨만포드: https://www.youtube.com/watch?v=FtN3BYH2Zes
- 영어자료지만 설명을 잘해서 들어볼만하다. 추천!
  
  
  
  
  
