### HTTP
- Client의 요청이 있을 때만 서버가 응답하여 해당 정보를 전송하고 곧바로 연결을 종료하는 방식
- Client -> Server로의 단방향 통신으로 필요한 경우에만 Server로 접근하는 콘텐츠 위주의 데이터를 사용할 때 용이

### Socket
- Server와 Client가 특정 Port를 통해 실시간으로 양방향 통신을 하는 방식
- 연결지향형 통신이기 때문에 실시간 통신(Streaming 서비스)이 필요한 경우에 자주 사용된다.
  * 만약 HTTP로 실시간 통신을 구현한다고 하면 지속적인 연결 요청 때문에 과부하가 걸리게 된다.

### 참고자료
- [[통신 방식] Http 통신과 Socket 통신 차이](https://mangkyu.tistory.com/48)
