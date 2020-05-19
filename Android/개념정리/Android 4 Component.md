
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

## Service

- 백그라운드에서 실행되는 구성 요소로, 오랫동안 실행되는 작업을 수행하거나 원격 프로세를 위한 작업을 수행하는 것. Service는 UI를 가지고 있지 않으며, 음악 재생처럼 오랜 시간동안 실행되기 위해 존재하는 component.


## ContentProvider

- ContentProvider는 공유된 앱 데이터 집합을 관리합니다. 예를 들어, Android 시스템은 사용자의 연락처 정보를 관리하는 contentprovider를 제공합니다. 따라서 적절한 권한을 가진 앱이라면 어떤 것이든 정보를 읽고 쓸 수 있다.



### 참고자료
- [찰스의 안드로이드 - 안드로이드 구성요소(4대 컴포넌트)](https://www.charlezz.com/?p=797)
- 깡샘의 안드로이드 프로그래밍
