## OSI 7 Layer

- Layer를 나눈 이유
  * 데이터의 흐름을 한 눈에 볼 수 있다
  * 문제를 해결하기가 편리하다. 7Layer로 나누어 작은 문제로 만든다.
  * 여러 회사의 장비 혼용 가능. Layer로 나누고 표준화했기 때문에..

![image](https://user-images.githubusercontent.com/26040955/82108488-b1e29c00-9769-11ea-927a-5b59449a2485.png)


- Physical Layer: 전기적인 특성을 이용하여 통신 케이블로 데이터를 전송
  * 단지 데이터만 전달하고 에러/효과적 전송에 관여 X
  * 통신 단위: 비트(0과 1)
- Data Link Layer: 네트워크 기기 간의 데이터 전송 및 물리 주소 결정
  * Physical Layer를 통해 송,수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와주는 역할
  * 통신에서의 오류도 찾아주고 재전송 기능을 가짐
  * MAC Address를 가지고 통신
  * 대표적인 장비: 브리지, 스위치
  * 통신 단위: 프레임
- Network Layer: 다른 네트워크와 통신하기 위한 경로 설정, 논리 주소 결정, 패킷 전달
  * 대표적인 장비: 라우터
- Transport Layer: 에러 복구를 위해 패킷을 재전송하거나 Flow를 조절해서 데이터가 정상적으로 전송될 수 있도록 하는 역할
- Session Layer: 세션 체결, 통신 방식 결정
- Presentation Layer: 문자 코드, 압축, 암호화 등의 데이터를 변환
- Application Layer: Application Service를 제공

### 참고자료
- [OSI 7계층 - DataLink Layer 데이터 링크계층](http://blog.naver.com/PostView.nhn?blogId=bkcaller&logNo=221606811918&parentCategoryNo=&categoryNo=153&viewDate=&isShowPopularPosts=true&from=search)
