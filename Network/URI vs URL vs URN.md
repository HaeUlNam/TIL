
## URI, URL, URN
- 항상 헷갈리는 개념인데, REST API의 자원인 URI를 보면서 저게 뭐지...싶어서 정리하게 되었다. GoodGid님이 잘 정리해둔 것이 있어서 이를 기반으로 정리해봤다.

![image](https://user-images.githubusercontent.com/26040955/82027412-2fa59980-96cf-11ea-9d3d-0e724b9d2799.png)

### URI(Uniform Resource Identifier)
- 통합 자원 식별자로 현재 동작하고 있는 Server에서 특정 리소스에 접근하기 위해 사용하는 Path
  * 정보 리소스를 고유하게 식별하고 위치를 지정할 수 있다.
  
- URI에는 URL과 URN이라는 두가지 형태가 존재

### URL(Uniform Resource Locator)
- 통합 자원 지시자로서 특정 서버 안에서 해당 리소스에 접근할 수 있는 상대적 위치를 나타냄
- 예시) www.naver.com 네이버의 URL
- 한계: 어느 순간에 해당 리소스에 접근할 수 있는 상대적 위치를 알려준다. 따라서 만약 상대적 위치를 변경하면 이후에는 접근 불가

### URN(Uniform Resource Name)
- Unique함을 보장하기에 리소스를 옮기더라도 잘 동작한다. 하지만 현재 표준으로 채택되지 않아 잘 볼 수 없다.

### 예시
1) http://img0.gmodules.com/ig/images/korea/logo.gif
    * 위는 logo.gif라는 자원의 상대적인 위치를 뜻하는 것이기에 URI도 되고, URL도 된다.
2) http://goodgid.github.io?name=gid
    * 위는 goodgid.github.io까지만 URL이고, ?name=gid은 식별자이기에 URI은 되지만 URL은 되지 못한다.
    * URL은 상대적인 위치를 나타내는 것이기 때문이다.

### 참고자료
- [URL과 URI, URN](https://goodgid.github.io/URL-URI-URN/)
