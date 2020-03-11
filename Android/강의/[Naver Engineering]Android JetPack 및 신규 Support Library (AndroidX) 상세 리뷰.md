## 출처: [Android JetPack 및 신규 Support Library (AndroidX) 상세 리뷰](https://tv.naver.com/v/4286045/list/267185)


### Jetpack

- 안드로이드 개발에 로켓을 달아주는 라이브러리 & 도구 모음집
- 이번 구글 IO에서 추가된 것은 Navigation, Slices, Paging, KTX 등이다.
![스크린샷 2020-03-11 오전 8 58 35](https://user-images.githubusercontent.com/26040955/76369315-7fd24980-6376-11ea-9ac4-42895ee35d59.png)

### Jetpack을 왜 사용해야 하냐?

- 하위 호환성 보장
  * 아래 사진 중 위의 5줄은 기존에 분기를 통해 버젼을 대응한 코드
  * 맨 아래 한 줄은 Jetpack workmanager을 이용하여 하위 호환성을 보장한 것이다.
![스크린샷 2020-03-11 오전 9 01 26](https://user-images.githubusercontent.com/26040955/76369441-e6576780-6376-11ea-8b4f-a39226a2b3b1.png)

- 개발자의 생산성을 위한 간결한 API
- IDE 통합

### AndroidX

- 기존에 지원하는 라이브러리가 너무 많다. 내가 원하는 기능이 어디에 있는지 잘 모른다...
![스크린샷 2020-03-11 오전 9 09 05](https://user-images.githubusercontent.com/26040955/76369756-f6bc1200-6377-11ea-889e-af2e30ada099.png)

- 덩치 큰 라이브러리를 각 위젯, 유즈케이스별로 분리
  * 내가 필요한 기능만 dependency를 걸고, 나머지 필요없는 코드는 안 가져올 수 있게 한다.
  * 아래와 같이 진행함으로서 내가 원하는 기능이 어느 패키지에 있는지 찾는 것도 용이해졌다.
  ![스크린샷 2020-03-11 오전 9 11 11](https://user-images.githubusercontent.com/26040955/76369832-413d8e80-6378-11ea-9fc0-9a7cc6b36f72.png)

![스크린샷 2020-03-11 오전 9 14 04](https://user-images.githubusercontent.com/26040955/76369952-a98c7000-6378-11ea-88e5-3d12c55be3f2.png)

- AndroidX와 Support Library 28과 기능이 거의 동일하고, 이름은 AndroidX가 더 간결한 것을 알 수 있다.
- 또한, 향후에 새로운 기능을 사용하려면 AndroidX를 꼭 사용해야한다.
- 기존의 버전을 AndroidX로 migration하려면 Android Stuido에 'Refator to AndroidX'기능을 사용하면 된다.<br>
(아직 완전하지 않다.. 나중에 update버전을 쓰라고 이야기함.)

- Jetifier: 빌드가 될 때, 기존의 레거시 패키지를 참조하는 바이너리를 AndroidX를 참조하도록 바꿔줌
![스크린샷 2020-03-11 오전 9 21 58](https://user-images.githubusercontent.com/26040955/76370304-c4131900-6379-11ea-9fb4-fe6eb61dc30f.png)

### 새로운 Jetpack 특징
- [WorkManager](https://tv.naver.com/v/4286184/list/267185)
- [Navigation](https://tv.naver.com/v/4286147/list/267185)
- [Paging](https://tv.naver.com/v/8457753/list/267185)
- [Slice](https://tv.naver.com/v/4286063/list/267185)

### 위의 새로운 Jetpack 특징들에 대해, 각각 영상을 보고 정리해보자.


