## Bubble Sort

- 인접한 두 원소를 검사하여 정렬하는 알고리즘
- 시간복잡도: n 제곱
- 추가 공간을 사용하지 않기에 Inplace sort
- swap을 사용하지 않기에 stable sort이다

- 예시: 7 4 5 1 3
  - 4 5 1 3 7
  - 4 1 3 5 7
  - 1 3 4 5 7
  
## Selection Sort
- 정렬되지 않은 Data들 중 가장 작은 값을 찾아 맨 앞에 두는 방식
- 시간복잡도: n 제곱
- 추가 공간을 사용하지 않기에 Inplace sort
- swap을 사용하기에 unstable sort
- 교환횟수는 상대적으로 적지만, 부분적으로 정렬되어 있어도 min값을 계속 찾아야 하기에 비효율적일 수 있다.
- 예시: 7 4 5 1 3
  - 1 4 5 7 3
  - 1 3 5 7 4
  - 1 3 4 7 5
  - 1 3 4 5 7
  
## Insertion Sort
- 손 안의 카드를 정렬하는 방법과 유사하다.
- 시간복잡도: n제곱(최악), n(최선)
- 추가 공간을 사용하지 않기에 Inplace sort
- swap을 사용하지 않기에 stable sort
- 연속적인 공간을 참조하기에 참조 지역성이 높아서 성능이 좋다.
- 비교 횟수가 bubble sort에 비해 상대적으로 적다.
- n이 50이하일때는  insertion sort를 쓰는 것이 효율적일 수 있다.
  - 50이라는 숫자는 computer system에 따라 달라질 수 있다.
  - 참조 지역성도 좋을 뿐더러 n이 작을 경우, merge나 quick sort보다 코드 복잡성이 낮고, 함수 콜이 적어서...
  
- 예시: 7 4 5 1 3
  - 4 7 5 1 3
  - 4 5 7 1 3
  - 1 4 5 7 3
  - 1 3 4 5 7

## Merge Sort
- 분할정복 알고리즘 중 하나로 하나의 배열을 두 개로 분할하여 정렬하는 방법
- 시간복잡도: nlogn
- 보통 추가적인 공간을 사용하기에 outPlace sort
  - Linked List로 하면 inplace로도 가능하지만 많이 사용하지 않는 방법이다..
- 추가적인 공간을 사용하기에 참조지역성이 떨어진다.
- stable
- 예시: 7 4 5 1 3
  - 4 7 / 5 /1 3
  - 4 5 7 / 1 3
  - 1 3 4 5 7

## Quick Sort
- 분할정복 알고리즘 중 하나로 pivot을 기준으로 양쪽으로 정렬하는 방법
- 시간복잡도: n2(최악), nlogn(평균)
- 추가 공간을 사용하지 않기에 inplace sort
- 순차적으로 공간을 참조하기에 참조지역성이 좋다.
- swap을 사용하기에 unstable sort
- 평균적으로 nlogn 정렬 알고리즘 중에 가장 빠르다.
- 시간복잡도를 최적화하기 위해, randomized나 median of Three 등의 방법을 사용한다.
- 예시: 6 10 13 5 8 3 2 11
  - 6 5 13 10 8 3 2 11
  - 6 5 3 10 8 13 2 11
  - 6 5 3 2 8 13 10 11
  - 2 5 3 6 8 13 10 11
  ....

## Heap Sort
- complete binary tree 형태로 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조
  - full binary tree와는 다르다.
- 시간복잡도: nlogn
- inplace, unstable
- insert: 맨 끝 idx에 삽입하고 부모와 비교하며 제자리를 찾아간다.
- delete: 맨 끝 node 와 root swap한 뒤, root에 있는 값은 제자리를 찾아간다.
- 데이터가 꾸준히 들어오는 상태에서 큰 몇 개를 찾아야 하는 경우
- build min Heap하는 과정은 O(n)
  - https://stackoverflow.com/questions/9755721/how-can-building-a-heap-be-on-time-complexity
