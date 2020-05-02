### ThreadLocal

- 오직 한 thread에 의해 읽고 쓰여질 수 있는 변수를 생성하도록 한다. 서로 다른 thread가 각각의 ThreadLocal의 값을 볼 수는 없다...

### 사용하는 경우
- 서버에서 클라이언트 요청을 각 스레드에서 할 경우, 해당 유저의 인증이나 쿠키 정보를 저장하는데 사용된다.
- Android에서는 스레드별로 Looper를 생성해서 사용하게 된다.

### 참고

- https://parkcheolu.tistory.com/17
- https://jins-dev.tistory.com/entry/Java-%EC%9D%98-Thread-Local-%EC%9D%B4%EB%9E%80
