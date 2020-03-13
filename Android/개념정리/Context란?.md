## Context 정의
- Application 환경에 대한 글로벌 정보 인터페이스
- Context 클래스는 추상 클래스로 실제 구현은 Android 시스템에 의해 제공된다.
- Context를 통해 어플리케이션에 특화된 리소스나 클래스에 접근할 수 있다. getPackageName(), getResoruce() 등의 메서드 사용 가능.
- Activity 실행, Intent 브로드캐스팅, Intent 수신 등 응용 프로그램 수준의 작업을 수행하기 위한 API를 호출 할 수 있다. 예를 들어, startActivity()나 bindService()

#### 따라서, Context가 있어야 리소스나 클래스에 접근하고, 안드로이드의 4대 컴포넌트 등을 시작할 수 있다.

### 그럼 왜 Context를 통해서 해당 어플리케이션의 정보에 접근해야할까?

- 일반적인 경우 어플리케이션이 프로세스와 아주 긴밀하게 연결되어 있는데, 안드로이드에서는 어플리케이션과 프로세스는 서로 독립적인 존재이기에 연결시켜줄 수 있는 Context라는 개념이 필요하게 되었다.
([[번역]구글 개발자 블로그 - Multitasking the Android Way](http://blog.naver.com/huewu/110085391353)에 더 자세한 내용이 있다.. 해당 내용은 다른 글을 통해 정리하도록 하겠다)

## Activity Manager Service (Application 정보 관리)

- [Java System Service](https://alnova2.tistory.com/1106)의 하나이며, 코어 플랫폼 서비스로 분류된다. 안드로이드 애플리케이션 컴포넌트인
액티비티, 서비스, 브로드캐스트 리시버 등을 생성하고 이들의 생명 주기를 관리하는 역할을 한다.

- 부팅 시에 실행

## 요청에 따라 Service가 생성/실행되는 과정

1) startService() 호출
2) startService()를 통해 서비스 실행 요청을 받고 Activity Manager service가 이를 수행한다.
3) Activity Manager Service는 Zygote Process에게 Application Service를 실행시키기 위한 ActivityThread 생성을 요청한다.
  * Activity Thread는 모든 안드로이드 Application의 메인 스레드로서 Activiy, Service 등의 생성및 스케줄링을 담당
  * Activity Thread가 메인 스레드로서 Application의 entry point의 역할을 한다. 따라서, Zygote는 Activity thread의 main함수를 
  호출하여 Application을 시작하게 된다.
  
4) Zygote Process는 fork를 통해 새로운 Process를 생성하고 그 위에 Activity Thread를 로딩한다. 
  * Zygote process가 새로운 Application을 실행하는 흐름
  ![image](https://user-images.githubusercontent.com/26040955/76611551-0ac16880-655e-11ea-9cd1-f051c2b5b205.png)
  * Android Application A가 생성되는 흐름
  ![image](https://user-images.githubusercontent.com/26040955/76611659-3b090700-655e-11ea-8f7b-17c441e6660f.png)

5) Activity Manager Service는 로딩된 Activity Thread에게 요청받은 service를 생성하도록 요청
6) Activity Thread는 service를 생성하고 실행한다.
  * Activity인 경우 Main UI 스레드를 실행한다.

### Context 역할

- 자신이 어떤 어플리케이션을 나타내고 있는지 알려주는 ID 역할
- ActivityManagerService에 접근할 수 있도록 하는 통로 역할

### Context의 종류

- Application Context: application lifecycle에 영향받는다.
- Activity Context: Activity lifecycle에 영향받는다. 즉, Activity에 대한 환경 정보들이 Context에 있고, 이 Context에 Intent를 
통해 다른 액티비티를 띄우면 액티비티 스택이 쌓이게 된다.

### Context type

- https://www.aurigait.com/blog/Best+practices-of-appropriate-Context-in-Android/ 을 참고해서 추가 작성하자.

## 출처
- [Context란?](https://shnoble.tistory.com/57)
- https://stackoverflow.com/questions/3572463/what-is-context-on-android
- [Activity Manager Service](https://blog.naver.com/hakssung/70118757588)
- https://alnova2.tistory.com/1104
- https://junghun0.github.io/2019/09/07/android-thread-handler/
- [Android Context](https://karrel.tistory.com/37)
- https://arabiannight.tistory.com/entry/272
- http://blog.naver.com/huewu/110085391353
- https://recipes4dev.tistory.com/143
- https://www.aurigait.com/blog/Best+practices-of-appropriate-Context-in-Android/
