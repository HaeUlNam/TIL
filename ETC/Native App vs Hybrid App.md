## Native App vs Hybrid App
- Native App: Android, Ios를 각각 Java/Kotlin, Swift 등의 언어로 구현하는 것.
  * 좀 더 정교한 UI/UX를 구현하려 하고, 성능을 향상시키려면 Native이 더 좋다.
- Hybrid App: 크로스 플랫폼으로서 하나의 코드를 작성하면 Android/Ios 둘 다 잘 작동함.
  * 간단한 App을 만들거나 빠르게 개발해야 하는 경우 좋다. 개발 생산성에 장점
  * Flutter 핫리로드 기능과 React Native의 code push 기능을 통해 수정한 부분을 빌드하지 않더라도 App에 적용할 수 있다. 생산성 향상...

### Hybrid App 개발 단점
- Hybrid App이 큰 규모의 App을 구현하는 경우 유지보수가 어렵다. 
- 항상 여러 개의 플랫폼을 이해하고 있어야 한다. 이는 결국 코드도 하드웨어 위에서 돌아가기에 안드로이드/Ios의 하드웨어에 대한 이해가 필요하고 이를 코드로 옮겨야 한다. 따라서 Hybrid App을 개발하더라도 사용자를 생각한다면 Android/Ios를 다 이해하고 있어야 한다.
- Android/Ios/React Native라는 3가지의 트렌드/규약 등을 알고 있어야 이를 적용해서 코드를 짤 수 있다.

### 참고자료
- [[ReactNative]AirBnB는 어째서 RN을 버렸나?](https://m.blog.naver.com/PostView.nhn?blogId=bkcaller&logNo=221317627805&proxyReferer=https:%2F%2Fwww.google.com%2F)
