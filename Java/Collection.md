### Collection
- 여러 원소들을 담을 수 있는 자료구조


### Collection 종류

- Map 인터페이스: HashMap, TreeMap
  * HashMap은 해쉬 베이스로 충돌이 나는 경우 chaining을 사용하고, 일정 threshold를 넘어갈 경우 Red-black Tree를 이용해서 충돌 처리
  * 따라서 HashMap은 최선 O(1), 최악 (log n/m) (m은 bucket size)
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

### Enumeration vs Iterator

- collection framwork에 대해 각 항목들을 순차적으로 접근하는데 사용된다. Java에서는 Iterator를 더 standard한 접근법으로 보고 권장.
- Enumeration은 Vector, Hashtable 같은 초기 collection에만 지원하고, Iterator는 모두 지원
- Enumeration은 snap-shot을 통해 collection을 처리하게 되는데, 만약 enumeration을 통해 순차적으로 접근하는 경우 도중에 insert나 delete에 대해서는 처리하지 않게 된다.
- Iterator는 collection 원본 데이터에 직접 access해서 처리하게 되는데, 만약 순차적으로 접근하다가 insert, delete가 발생하면 ConcurrentModificationException이 발생하게 된다. 보통 이것을 Fail-fast라고 한다.


### Fail-fast Iterator vs Fail-Safe Iterator

- Fail-fast는 가능한 빨리 실패를 노출하고 작업을 중지하게 되며, Fail-Safe는 장애 발생시 작업을 중단하지 않고 가능한 많은 실패를 피하려고 한다.

- Fail-fast: Iterator의 remove() 메소드 이외의 코드로 기존 collection이 수정되면 fail-fast iteratiors는 예외 발생
 * 따라서 collection에서 제거 기능을 이용하려면 iterator의 remove()를 사용해야 한다.
 * ArrayList, HashMap 등과 같은 java.util 패키기의 collection에 대한 기본 반복자는 Fail-fast
- Fail-safe: 실제 Collection의 복제본을 작성하고 반복합니다. 반복자가 작성된 후 수정이 발생해도 사본은 그대로 유지. 
 * 단점1) iterator 동작 도중에 collection의 값이 변경되더라도 알 수 없다.
 * 단점2) 시간과 메모리와 관련해서 사본을 작성하는 오버헤드
 * ConcurrentHashMap, CopyOnWriteArrayList 등과 같은 java.util.concurrent 패키기의 collection에 있는 반복자들은 fail-safe하다.
 * 위에서 설명하는 Enumeration도 Fail-safe에 해당.


### HashMap vs ConcurrentHashMap

- 둘 다 해싱을 기본으로 사용하는데, HashMap은 non thread-safe이고, ConcurrentHashMap은 thread-safe하다.
- 그럼 multi-thread 환경에서 굳이 ConcurrentHashMap을 이용할 이유가 있을까? synchronized + HashMap을 사용하면 되는데?
 * ConcurrentHashMap은 map을 16개의 파트로 나누고 update 동작이 있는 동안 해당 부분만 lock을 수행한다. 즉, 16개의 thread가 동시에 map에서 기능을 수행할 수 있는 것이다.
 * 다만, ConcurrentHashMap을 잘 사용하려면 thread-safe한 코드를 짤 줄 알아야 한다. 원자성을 보장하도록...
 
 ```java
 ConcurrentHashMap<String,Long>map = new ConcurrentHashMap<>();
 
 Long oldValue = map.get(word);
 Long newValue = oldValue == nul ? 1 : oldValue + 1;
 map.put(word, newValue); //thread-safe하지 않다.
 ```
 * 만약 위와 같이 짜면 thread-safe하지 않은 코드이다. 다른 스레드에서 동시에 같은 카운트를 업데이트하고 있을지도 모르기 때문이다.
 따라서 값을 안전하게 업데이트하려면 아래와 같은 원자적인 compute메서드를 사용해야 한다.
 
 ```java
 map.compute(word, (k,v)->v == null ? 1: v+1) //atomic하기에 thread-safe하다.
 ```

### 추가적인 고찰

- 그냥 작은 프로그램에서는 thread-safe하게 코드 짜는 게 어렵지 않을 수 있는데, 프로그램이 커질 수록 굉장히 어려울 거 같다... 이 부분은 충분한 공부가 필요할 것 같다.
- 시간 날 때 [자바 병렬 프로그래밍](http://www.yes24.com/Product/Goods/3015162)을 보고 병렬 프로그래밍에 대한 이해도를 높여야겠다. 

### 참고자료

- [자바 컬렉션과 동기화(Java Collection Synchronization)](https://madplay.github.io/post/java-collection-synchronize)
- [Java HashMap은 어떻게 동작하는가?](https://d2.naver.com/helloworld/831311)
- [Internal Working of TreeMap in Java](https://www.dineshonjava.com/internal-working-of-treemap-in-java/)
- [자바 HashMap을 효과적으로 사용하는 방법](http://tech.javacafe.io/2018/12/03/HashMap/)
- [Fail-Safe Iterator vs Fail-Fast Iterator](https://simuing.tistory.com/261)
- [5 Difference Between Iterator And Enumeration With Example : Java Collections Question](https://javahungry.blogspot.com/2013/06/difference-between-iterator-and-enumeration-collections-java-interview-question-with-example.html)
- [[Java]ConcurrentHashMap 사용하기](https://m.blog.naver.com/PostView.nhn?blogId=horajjan&logNo=220584946854&proxyReferer=https:%2F%2Fwww.google.com%2F)
