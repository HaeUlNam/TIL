### REST API
- Representational State Transfer라는 약자로 웹(HTTP)의 장점을 최대한 활용할 수 있는 아키텍처입니다.
- REST: HTTP 통신에서 어떤 자원에 대한 CRUD 요청을 Resource와 Method로 표현하여 특정한 형태로 전달하는 방식
  * CRUD: Create, Read, Update, Delete

### REST API 구성
1) 자원: URI
   * URI vs URL
2) 행위: HTTP METHOD
   * HTTP METHOD는 GET,POST,PUT,DELTE 등의 4개 메소드 존재
3) Representation of Resource
   * 자원(URI)의 표현방법: JSON, XML, Text...

### REST API 특징 
- Uniform Interface(일관된 인터페이스): Resource(URI)에 대한 요청이 통일되고 한정적으로 수행하는 아키텍처 스타일을 뜻함. 이 덕분에 플랫폼에 종속되지 않고, HTTP를 사용하는 어느 플랫폼이든 REST API를 사용 가능
- Stateless(무상태성): REST API에서는 세션이나 쿠키정보를 활용하여 작업을 위한 상태 정보를 저장 및 관리하지 않는다. 따라서 서비스의 자유도가 높고, 구현이 단순하다.
- 캐싱 가능: REST API의 큰 특징 중 하나가 HTTP라는 웹 표준을 사용하기에 HTTP의 캐싱 사용 가능
  * HTTP 표준에서 지원하는 Last-modified Tag 또는 E-Tag를 통해 캐싱을 구현할 수 있고, 대량 요청을 효율적으로 처리할 수 있도록 한다.
- Client-Server 구조: Client와 Server부분이 개발할 것이 명확하다.
  * 따라서 서로 간의 의존성을 줄일 수 있다.
- 자체 표현 구조: 요청 메세지만 보고도 쉽게 파악할 수 있는 구조로 되어 있다.

```json
HTTP POST , http://localhost:8080/insertBoardInfo

{

  "boardVO":{

      "title":"제목",

      "content":"내용"

  }

}

```

- Layered System(계층 구조): 보안, 로드 밸런싱, 암호화 등을 위해 계층적으로 구조를 설정할 수 있다. 또한 Proxy, Gateway등의 중간 매체를 사용할 수 있도록 해서 Client는 원래 서버인지 중간계층인지 모르도록 할 수 있다.

### 참고자료
- [REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)
- [REST API ?](https://medium.com/@dydrlaks/rest-api-3e424716bab)
- [[Restful API] Rest API란?](https://mangkyu.tistory.com/46)
