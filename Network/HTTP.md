## HTTP
- 인터넷상에서 데이터를 주고 받기 위한 프로토콜로서 Application Level의 프로토콜로서 TCP/IP 모델 위에서 돌아간다.

### HTTP Server/Client 구조

![image](https://user-images.githubusercontent.com/26040955/82032310-fa507a00-96d5-11ea-875e-7bc50f74fd2c.png)

### URL
- 서버에서 자원의 상대적 위치를 확인하여 자원을 얻게 된다.

![image](https://user-images.githubusercontent.com/26040955/82032088-b8bfcf00-96d5-11ea-92d8-5498cdcbf95c.png)

### HTTP 메소드
- GET: 존재하는 자원에 대한 요청
- POST: 새로운 자원 생성
- PUT: 존재하는 자원 변경
- DELETE: 자원 삭제


### Status Code
- 2xx번대는 대부분 성공
- 404는 요청한 자원이 Server에 없다는 것

### 멱등성(Post vs Put)
- Post와 Put 모두 없는 것에 대해 생성하는 것은 동일하나 반복적으로 요청했을 때, Post는 멱등성을 만족하지 못하고 Put은 멱등성을 만족한다.
- 멱등성을 만족하는 Put을 사용했을 때, 요청을 보내다가 네트워크가 끊어진다면 Server에 제대로 전달됐는지는 상관없이 다시 보내도 된다. 어차피 같은 결과를 내기 때문에... 하지만 Post는 이러한 상황에서 다시 보낸다면 새로운 결과를 만들어낸다. 이러한 것이 Put의 장점이라고 할 수 있을 것 같다.
- Put은 URL을 보내고, Put은 보내지 않는다.

### Post, Put 정의 - [PUT vs. POST in REST에서 가져왔다](https://stackoverflow.com/questions/630453/put-vs-post-in-rest)

(1) POST to a URL creates a child resouce at a server defiend URL
(RFC 2616 POST)
(2) PUT to a URL create/replaces the resource in is entirely at the client defined URL
(RFC 2616 PUT)

### Safe Method
- 리소스를 수정하지 않는 GET, Head등의 Method 등이 Safe라고 한다.

### 참고자료
- [HTTP 프로토콜이란?](https://shlee0882.tistory.com/107)
- [프런트엔드 개발자가 알아야하는 HTTP 프로토콜 Part 1](https://joshua1988.github.io/web-development/http-part1/)
- [post vs put](https://multifrontgarden.tistory.com/245)
- [HTTP 함수 - Post vs Put vs Patch](https://goodgid.github.io/HTTP-Method-Post-vs-Put-vs-Patch/)
