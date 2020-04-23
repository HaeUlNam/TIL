## BST(Binary Search Tree)

![image](https://user-images.githubusercontent.com/26040955/80094926-1151ef80-85a2-11ea-912d-a87e0b5ebdad.png)
<br>[이미지 출처]: https://yeolco.tistory.com/55

- bst는 부모 노드 기준으로 좌측은 부모 노드보다 작은 값을 가진 집단, 우측은 부모 노드보다 큰 값을 가진 집단이다.
- 위를 기준으로 하면 5 기준으로 작은 것(좌측 자식) 큰 것(우측 자식)으로 나뉜다.
- 검색, 삽입, 삭제: O(height)
- 순회: O(n)
  - 오름차순으로 정렬하려면 inorder 순회

- 삭제는 3가지 case가 존재
  - degree 0 (leaf node)인 경우 그냥 삭제
  - degree 1 인 경우 부모 노드와 자식 노드 연결시켜주고 삭제
  - degree 2 인 경우 좌측 subtree에서 가장 큰 값 or 우측 subtree에서 가장 작은 값 둘 중에 하나를 골라서 대체한다.

- 한계점: skewed한 형태로 bst가 구성될 때는 시간복잡도가 O(n)
  - ex) 1 2 3 4 5 6 7 형태로 데이터가 들어올 때는 검색, 삽입, 삭제 모두 O(n)이다.
  - 따라서 트리의 입력과 삭제 단계에서 트리 전체의 균형을 맞추기 위해 AVL Tree가 등장했다.

## AVL Tree

- subtree의 높이를 적절하게 제어해서 전체 트리가 어느 한쪽으로 늘어지지 않도록 하는 이진탐색트리의 일종
- balance fator: 왼쪽 서브트리의 높이에서 오른쪽 서브 트리 높이를 뺀 것.
- 참고자료: https://ratsgo.github.io/data%20structure&algorithm/2017/10/27/avltree/

- 시간복잡도: 항상 balanced tree이기에 검색, 삽입, 삭제에 대해 O(logn)
- 단점: Disk에 데이터가 저장되어 있을 때, Data의 크기가 커진다면 트리의 depth가 깊어져서 disk 탐색 시간이 올라간다.
  - 이러한 문제점을 대응하기 위해 나온 것이 m-way search tree(b+ tree)이다.
