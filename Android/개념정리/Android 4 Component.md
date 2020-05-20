
## 4대 컴포넌트
- Activity, BroadCastReceiver, ContentProvider, Service
- Intent: Activity, BroadCastReceiver, Service를 실행하도록함.
  * 코드 상에서 Intent를 준비하고 시스템에 의뢰하면 시스템에서 인텐트 정보에 맞는 컴포넌트를 실행하는 구조.

## Activity

- UI가 있는 단일 화면을 나타냄. 사용자와 interaction을 하는 component로서 Activity는 main UI Thread를 시작과 동시에 생성되게 되고, ANR(Application Not Response)가 나지 않도록 Background thread들을 적절히 사용해야 합니다.

- setContentView()함수를 통해 UI가 생성되게 됩니다. 만약 onResume()까지 불리지 않는다면, UI에 아무것도 그려지지 않는다.

- 회전 회전의 경우: onSaveInstanceState 함수로 UI 데이터를 저장하고, onRestoreInstanceState 함수로 UI 데이터를 복원

- Activity는 절대 싱글턴이 아니다. 어디서든지 Intent로 불린다면 새로 생성되어 Activity Stack에 올려진다.

## BroadCastReceiver

- 시스템 범위의 브로드캐스트 알림에 응답하는 구성 요소를 말합니다. 대다수의 브로드캐스는 시스템에서 시작하는데, 화면 꺼짐/배터리 잔량 부족/ 사진 캡쳐 등의 브로드 캐스트가 있습니다. 
- App도 브로드캐스트를 통해 다른 여러 앱에게 알리는 역할을 하게 된다.
 * 정적 BroadCastReceiver: AndroidManifest.xml에 고정해서 리시버를 등록하고 받는다.
 * 동적 BroadCastReceiver: 동적으로 리서버를 할당하고 해제한다. 따라서 등록되는 component의 Lifecycle이 끝나면 (unregisterReceiver()가 호출되면) 더 이상 수신할 수 없다.
 
### 동적 Receiver 장점
- 시스템에 큰 부하를 주지 않는 점
- 다른 Component 내에 소스가 존재한다는 것: 해당 component로부터 쉽지 접근 가능

### 정적 Receiver 장점
- 동적 Receiver는 특정 Activit나 Service가 구동 중에만 의미 있을 때 사용하지만, 정적은 구동 중이 아닐 때도 Receiver가 동작한다.

### Receiver에서는 간단한 작업만 해야 하는 이유
- 아래 그림과 같이 ActivityManager가 10초를 초과한 Receiver에 대해서는 ANR을 발생시킨다.
- 그럼 속한 component도 같이 죽는다.

![image](https://user-images.githubusercontent.com/26040955/82398679-65130400-9a8e-11ea-850f-5ba27c2b98bc.png)


## Service

- 백그라운드에서 실행되는 구성 요소로 오랫동안 실행되는 작업을 수행할 때 사용. Service는 UI를 가지고 있지 않으며, 음악 재생처럼 오랜 시간동안 실행되기 위해 존재하는 component.
 * Forground Service: 알림을 사용하며 사용자에게 잘 보이는 몇몇 작업 수행. ex) 음악 재생
 * Background Service
 * Bind Service: Client-Server 인터페이스를 제공하여 구성 요소가 서비스와 상호작용하도록 함. 바인딩이 해제되면 서비스는 소멸.

### Service와 Activity 통신
- BroadCastReceiver 사용
- Bind Service 사용

## ContentProvider

- ContentProvider는 공유된 앱 데이터 집합을 관리합니다. 예를 들어, Android 시스템은 사용자의 연락처 정보를 관리하는 contentprovider를 제공합니다. 따라서 적절한 권한을 가진 앱이라면 어떤 것이든 정보를 읽고 쓸 수 있다.
 * 이미지 예시: [MVVM 패턴과 Paging으로 수퍼 빠른 이미지 피커 만들기 – 찰스](https://www.charlezz.com/?p=44145#comment-336)


### 참고자료
- [찰스의 안드로이드 - 안드로이드 구성요소(4대 컴포넌트)](https://www.charlezz.com/?p=797)
- 깡샘의 안드로이드 프로그래밍
