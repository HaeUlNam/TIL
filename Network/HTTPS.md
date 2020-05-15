
## HTTPS란?
- HTTP 하부에 SSL과 같은 보안계층을 제공함으로써 동작한다.
![image](https://user-images.githubusercontent.com/26040955/82046001-0135b780-96eb-11ea-843c-d19e4d3bb7ee.png)
![image](https://user-images.githubusercontent.com/26040955/82046040-20cce000-96eb-11ea-9043-099fd292d08d.png)

### SSL 인증서란?
- Client와 Server 간의 통신을 공인된 제3자 업체가 보증해주는 전자화된 문서
  * 제3자 업체는 CA(Certificate Authority)라고 불리는데, Symantec이 가장 높은 점유율을 가진다.

- 장점
  * 통신 내용이 노출되는 것 방지
  * 접속하려는 사이트가 암호화되어있는지 확인 가능

### SSL 암호화
- 공개키 + 대칭키인 하이브리드 방식이라고 할 수 있다.
  * 공개키 방식: private 키와 public 키를 두 개 두어서, 외부에는 public 키를 주고 암호화된 것을 private 키로 해독하도록 한다. 키 전달을 하지 않는 대신 두 개의 키가 동일하지 않기에 암호화, 복호화 속도가 느리다.
  * 대칭키 방식: 암호,복호화 할때 key를 동일하게 사용해서 속도가 빠르다. 다만, client A가 키를 2개 생성하면 이를 client B에게 전달해줘야 하기에 도중에 탈취당할 위험성이 존재한다.
  * 따라서 SSL은 공개키 방식으로 대칭키를 전달하고, 대칭키로 통신해서 암호화와 속도 두 마리 토끼를 잡았다.

![image](https://user-images.githubusercontent.com/26040955/82047146-3c38ea80-96ed-11ea-8bf1-0bf705e7a9d5.png)

### 참고자료
- [HTTPS와 SSL 인증서, SSL 동작방법](https://wayhome25.github.io/cs/2018/03/11/ssl-https/)
