![image](https://user-images.githubusercontent.com/26040955/82063711-c93c6d80-9706-11ea-8002-9b0aa9d92407.png)

### TCP(Transmission Control Protocol) & UDP(User Datagram Protocol)
- TCP: 연결형 서비스를 지원하는 프로토콜로서 패킷을 추적 및 관리하게 된다.
  * 흐름제어(Flow control): 송신 측이 수신측보다 빨라서 도착하는 데이터의 손실이 나는 것을 막는다.
  * 혼잡제어(Congestion control): 송신 측의 데이터 전달과 네트워크의 데이터 처리 속도 차이를 해결하기 위한 것.
  * TCP는 신뢰성이 높아야 하는 서비스에 꼭 필요하다.
  * 3,4 handshake로 논리적 통로를 연결하고 해제.
- UDP: 비연결형 프로토콜로서 각각의 패킷이 따로 전송되고, 독립적으로 처리하게 된다.
  * UDP는 실시간 서비스에 적합.

### 참고자료
- [[TCP/UDP] TCP와 UDP의 특징과 차이](https://mangkyu.tistory.com/15)
- [TCP 흐름제어 혼잡제어](https://slenderankle.tistory.com/230)
