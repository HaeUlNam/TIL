### ThreadLocal

- 오직 한 thread에 의해 읽고 쓰여질 수 있는 변수를 생성하도록 한다. 서로 다른 thread가 각각의 ThreadLocal의 값을 볼 수는 없다...

### 사용하는 경우
- 서버에서 클라이언트 요청을 각 스레드에서 할 경우, 해당 유저의 인증이나 쿠키 정보를 저장하는데 사용된다.
- Android에서는 스레드별로 Looper를 생성해서 사용하게 된다.
```java
  ThreadLocal<Looper> 에 set() 메서드로 새로운 Looper를 추가하고, get() 메서드로 스레드를 가져올 때 스레드별로 다른 Looper가 반환된다.
  Looper Prepare로 각각 thread별 Looper를 생성. 
  Main thread 경우 Looper.prepareMainLooper()를 호출하여 생성. 
```

### 참고

- https://parkcheolu.tistory.com/17
- http://egloos.zum.com/sweeper/v/1985738
- https://jins-dev.tistory.com/entry/Java-%EC%9D%98-Thread-Local-%EC%9D%B4%EB%9E%80
