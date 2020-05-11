### Collection
- 여러 원소들을 담을 수 있는 자료구조


### Collection 종류

- Map 인터페이스: HashMap, TreeMap
  * HashMap은 해쉬 베이스로 충돌이 나는 경우 chaining을 사용하고, 일정 threshold를 넘어갈 경우 Red-black Tree를 이용해서 충돌 처리
  * 따라서 HashMap은 최선 O(1), 최악 (logn)
  * TreeMap은 Red-black Tree 베이스로 저장하게 된다.
  * 따라서 최악 (logn)
  
- List 인터페이스: ArrayList, LinkedList, Vector, Stack
  * ArrayList와 Vector는 거의 동일하지만, not Thread safe 와 Thread safe하다는 특징으로 나뉜다.

### 참고자료

- [자바 컬렉션과 동기화(Java Collection Synchronization)](https://madplay.github.io/post/java-collection-synchronize)
- [Java HashMap은 어떻게 동작하는가?](https://d2.naver.com/helloworld/831311)
- [Internal Working of TreeMap in Java](https://www.dineshonjava.com/internal-working-of-treemap-in-java/)
