### Semaphore

- 여러 개의 동기화 가능. 즉, 한 순간에 여러 개의 thread가 critical section에 방문 가능
- sempahore를 가지고 있는 스레가 세마포어 해제 가능.

### Mutex

- 상호 배제함으로서 critical section에 하나의 thread만 들어갈 수 있다.
- 뮤텍스를 소유하고 있어야 해제 가능.
- 보통 semaphore를 숫자 1로 두어 구현하게 된다.




### 참고
- https://www.tutorialspoint.com/mutex-vs-semaphore
- https://goodgid.github.io/What-is-Thread/
- https://about-myeong.tistory.com/34
