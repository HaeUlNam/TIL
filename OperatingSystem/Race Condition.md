## Race Condition(경쟁 상태)

- 공유 자원에 동시에 접근하여 올바르지 않는 결과값이 나올 수 있는 상태
- 두개 또는 더 많은 Thread가 공유 자원에 접근할 수 있고, 해당 Thread들이 동시에 같은 값을 변경하려고 할 때 race condition은 일어날 수 있다.
- race condition을 해결할 수 있는 방법으로 Semaphore, Mutex, Monitor가 있다.
  * Mutex와 Monitor는 상호 배제를 함으로써 임계 구역에 하나의 쓰레드만 들어갈 수 있다.
  * Monitor는 Java에서만 제공되는 매커니즘
  * Semaphore는 binary or counting 가능. 
  
### Semaphore vs Mutex
- Semaphore는 signal을 주는 매커니즘이다. acquire(), release() 신호를 통해 자원을 획득하고, 내보낸다.
  * critical section에 들어가는 integer를 마음대로 정할 수 있다. binary semaphore는 mutex와 비슷하다고 헷갈리기 쉽지만.. Mutex와 Semaphore는 엄연히 Object lock/ Singalling 이라는 서로 다른 매커니즘을 가지고 있기에, 다르다.
- Mutex는 object 소유해서 lock을 거는 매커니즘. 외부에서 lock을 푸는 것이 불가능. Semaphore는 외부에서 signal을 통해 count++ 가능하다.
- 따라서 완전 안전하게 binary locking을 하려면 Mutex가 좋은 선택일 듯하다.

### Mutex vs Monitor
- Mutex는 다른 프로세스 간에 동기화를 위해 사용. 
  * 운영체제 커널에 의해 제공됨
  * 따라서 무겁고 느리다.
- Monitor는 하나의 프로세스 내에 다른 쓰레드 간에 동기화 할 때 사용.
  * Framework이나 라이브러리 그 자체에서 제공됨
  * 가볍고 빠르다.
  * 모든 Java 객체는 Monitor를 가지고 있다. 

### 참고
- https://www.tutorialspoint.com/mutex-vs-semaphore
- https://goodgid.github.io/What-is-Thread/
- https://about-myeong.tistory.com/34
- [위키백과 - 경쟁 상태](https://ko.wikipedia.org/wiki/%EA%B2%BD%EC%9F%81_%EC%83%81%ED%83%9C)
- [What is a race condition?](https://stackoverflow.com/questions/34510/what-is-a-race-condition)
- [Difference Between Semaphore and Mutex](https://techdifferences.com/difference-between-semaphore-and-mutex.html)
- [Monitor vs Mutex](https://stackoverflow.com/questions/38159668/monitor-vs-mutex)
