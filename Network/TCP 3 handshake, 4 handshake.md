## TCP 3 Handshake
- 전송 계층의 TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전 정확한 데이터 전달을 보장하기 위해 end to end 세션을 수립하는 과정
- 전송 시 실패, 오류 등을 바로 잡기 위해 TCP 사용.


### TCP 3 Handshake - 과정
- 이 과정으로 TCP가 신뢰성 있는 통신을 보장할 수 있게 된다.
- Client -> Server: SYN
  * SYN 패킷을 보내면 Client는 SYN-SENT 상태가 된다.
  * SYN 패킷은 연결 요청 패킷으로서 sequence번호를 임의로 설정해서 보낸다.
- Server -> Client: SYN ACK
  * 다시 잘 받았다고, ACK와 SYN을 보내면 Server는 SYN-SENT 상태가 된다.
  * Server로부터 ACK와 SYN을 받으면 Client는 Established가 된다.
- Client -> Server: ACK
  * Client로부터 ACK를 받으면 Server는 Established가 된다.

![image](https://user-images.githubusercontent.com/26040955/82014074-c74abe00-96b6-11ea-8397-5c8d252b30e5.png)


## TCP 4 Handshake
- TCP 통신에서 세션을 종료하기 위해 하는 행동

### TCP 4 Handshake - 과정
- 이 과정에서 가장 먼저 FIN을 보내는 주체는 Client 뿐만 아니라 Server도 될 수 있다.
  * Client가 먼저 FIN: Active Close
  * Server가 먼저 FIN: Passive Close
- FIN 패킷은 종료할 때 보는 패킷으로서 더이상 보낼 데이터가 없다는 것을 뜻함.

- Client -> Server: FIN
  * Server에게 종료할 것이라는 FIN패킷을 보낸다.
- Server -> Client: ACK
  * Server는 Client에게 알겠다고 ACK를 보내고, 그와 동시에 Server에 해당 포트와 연결된 Application을 Close() 요청한다.
- Server -> Client: FIN
  * Application들이 모두 close되면, Client에게 FIN 패킷을 보낸다.
- Client -> Server: ACK
  * Client는 ACK를 받은 뒤 FIN 패킷을 기다리다가 받게 되면 ACK를 보내며 TIME_WAIT 상태로 변하게 된다.
  * TIME_WAIT는 일정 시간이 지나면 CLOSED된다.
  * Server는 ACK를 받으면 CLOSED 된다.

![image](https://user-images.githubusercontent.com/26040955/82014891-7f2c9b00-96b8-11ea-8815-46f4d59a7a31.png)


### TIME_WAIT가 필요한 이유
- FIN 패킷 이후에 Server에서 보낸 데이터가 도착할 수도 있기 때문이다.
  * 그 이유는 전송 지연이나 재전송 등의 이슈 때문
  * 따라서 TIME_WAIT(default 240초) 동안 기다리고 CLOSED하도록 해서 늦어진 패킷을 버리는 경우가 없도록 한다.


### 비정상종료 상황
- Application close() 제대로 하지 못해서 Server가 CLOSE_WAIT로 남아있는 경우
- ACK를 받지 못해서 FIN_WAIT 1로 남아있는 경우
  * 양방향 통신이 이루어지지 않았기에 아마 Server 쪽에 문제가 있는 것으로 판단된다.(네트워크나 방화벽 문제..)
  * 일정 시간이 지나면 TIME_OUT으로 CLOSED된다.
- ACK를 받지 못해서 FIN_WAIT 2로 남아있는 경우
  * 이 경우는 첫번째 비정상종료 상황과 비슷한 것 같다.
  * 양방향 통신이 이루어졌기에, 확실히 네트워크 문제는 아니다.
  * 일정 시간이 지나면 TIME_OUT으로 CLOSED된다.


### 참고자료
- [TCP 3-way Handshake, 4-way Handshake](https://goodgid.github.io/TCP-IP-3Way-4Way/)
- [TCP flag(URG, ACK, PSH, RST, SYN, FIN)](https://mindgear.tistory.com/206)
