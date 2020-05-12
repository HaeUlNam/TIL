### Collection
- 여러 원소들을 담을 수 있는 자료구조


### Collection 종류

- Map 인터페이스: HashMap, TreeMap
  * HashMap은 해쉬 베이스로 충돌이 나는 경우 chaining을 사용하고, 일정 threshold를 넘어갈 경우 Red-black Tree를 이용해서 충돌 처리
  * 따라서 HashMap은 최선 O(1), 최악 (logn)
  * TreeMap은 Red-black Tree 베이스로 저장하게 된다.
  * 따라서 최악 (logn)
  
- List 인터페이스: ArrayList, LinkedList, Vector, Stack
  * ArrayList와 Vector는 거의 동일하지만, not Thread safe(단일 스레드에서 더 빠름) 와 Thread safe하다는 특징으로 나뉜다.
  * Vector는 size를 넓힐 경우 2배씩 늘어나게 되고, ArrayList는 50퍼센트씩 늘어나게 된다.
  * ArrayList는 index를 통한 random access 가능하고 remove가 느리다.
  * LinkedList는 add와 remove가 빠르지만, 찾는 것이 느리다.
  
### ArrayList와 LinkedList의 좋은 점만 가지는 경우 - Hashing

- ArrayList의 빠른 random access와 LinkedList의 빠른 add와 remove 특성을 가지려면, 해싱을 결합하면 된다.
- Java HashMap을 이용해서 key를 저장하고 value에 LinkedList Pointer를 가지고 있으면 find를 최선의 O(1)시간에 할 수 있다.



### 참고자료

- [자바 컬렉션과 동기화(Java Collection Synchronization)](https://madplay.github.io/post/java-collection-synchronize)
- [Java HashMap은 어떻게 동작하는가?](https://d2.naver.com/helloworld/831311)
- [Internal Working of TreeMap in Java](https://www.dineshonjava.com/internal-working-of-treemap-in-java/)
