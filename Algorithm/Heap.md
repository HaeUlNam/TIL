### Heap 자료구조란?

- complete binary tree의 형태로 자료들 중에 최솟값이나 최댓값을 빠르게 찾기 위해 만들어진 자료구조
- Heap에서는 중복된 값을 허용한다.
- 삽입 연산(lg n): 처음엔 맨 끝 idx에 위치시키고 부모와 비교하여 자신의 자리를 찾아간다.
- 삭제 연산(lg n): 맨 끝 idx와 root와 swap해서 큰 값은 pop하고, root에서 max_heapify 시행.

### Max Heapify
- 만약 A[i]가 max heap property를 위반한다면, 왼쪽이나 오른쪽 자식 중에 더 큰 element와 swap을 진행한다.
  - 아래와 같이 구성되어 있을 때, Max Heapify를 하면 A[2]가 4인데 Max heap property를 위반하기에 자식 중에 더 큰 A[4]와 swap한다. 그 다음은 바뀐 A[4]와 A[8]을 swap
  - 따라서 Max Heapify 시간복잡도는 O(logn)이다.
<img width="624" alt="스크린샷 2020-05-02 오전 11 57 32" src="https://user-images.githubusercontent.com/26040955/80853459-1bdc4b00-8c6c-11ea-9389-e51e2a4d2bd2.png">
<img width="619" alt="스크린샷 2020-05-02 오후 12 00 50" src="https://user-images.githubusercontent.com/26040955/80853529-92794880-8c6c-11ea-8644-541cf45f34cf.png">

### Build Max Heap

- 배열에서부터 Max Heap을 만들기 위한 과정이다. 이를 시행하려면 n/2부터 1까지 Max Heapify를 진행해야 한다.
  - n/4 (1 c) + n/8 (2 c) + n/16 (3 c) + … + 1 (lg n * c)
  - n/4 = 2의 k승으로 치환하면, c * 2의 k승 * ( 1/(2의 0승) + 2/(2의 1승) + 3/(2의 2승) + … (k+1)/2의 k승 )
  - 따라서 멱급수의 공식에 의해 계산하면 O(n)
  - 사실 level의 노드 개수 같은 경우 디테일하게 계산하면 홀수일 때 n/4 + 1, 짝수일 때 n/4인데 +1은 시간복잡도 계산할 때 상수로 큰 의미가 없기에 괜찮다.

### 왜 Build Max Heap할 때 Heapify를 1부터 하지 않고, n/2부터 하는가?

- 아래와 같이 있다고 할 때, 1부터 Heapify를 진행하면 Heap property를 보장할 수 없다. 즉, 16이 절대 root로 올 수 없다. 따라서 뒤에서부터 진행해야 Heap property를 보장할 수 있다.
- n/2부터라고 하는 이유는 leaf node 같은 경우 heapify가 o(1)이기 때문이다.
<img width="369" alt="스크린샷 2020-05-02 오후 12 06 49" src="https://user-images.githubusercontent.com/26040955/80853664-690cec80-8c6d-11ea-8ba0-1bc451eeb673.png">


### 참고자료

- https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html
- https://www.cs.bgu.ac.il/~ds122/wiki.files/Presentation09.pdf
- https://www.youtube.com/watch?v=MiyLo8adrWw

