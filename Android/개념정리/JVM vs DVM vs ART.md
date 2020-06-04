### JVM(Java Virtual Machine)

- 자바 바이트 코드를 실행할 수 있는 주체, 자바 바이트 코드는 플랫폼에 독립적이며 JVM에 의존적으로 실행.

![image](https://user-images.githubusercontent.com/26040955/83719911-085d3f00-a673-11ea-9a46-6fc37ff24cc9.png)

## JVM 특성
- 스택 기반의 가상 머신
  * 스택 기반의 가상 머신에서는 모든 연산을 아래와 같이 값을 stack에 쌓아두며 진행.
  ![image](https://user-images.githubusercontent.com/26040955/83718285-b9fa7100-a66f-11ea-8002-8a749b7cfa9b.png)
  
  <img width="149" alt="스크린샷 2020-06-04 오후 2 29 07" src="https://user-images.githubusercontent.com/26040955/83718297-c088e880-a66f-11ea-841e-f1fb7a4d8531.png">
  
- 자바 바이트코드 검증기를 통해 stack overflow, 필드 접근 규칙 위반, 지역 변수 초기화 전 사용. 

## DVM(Dalvik Virtual Machine)
- 안드로이드 애플리케이션에서 실행할 수 있는 가상 머신으로서 모바일 환경이 데스크탑보다 배터리 수명, 컴퓨팅 파워가 열악하기에 모바일에 최적화 되어서 나왔다.
- Zygote process가 각 application의 Dalvik vm을 만들게 된다.


### APK 추출 과정
![image](https://user-images.githubusercontent.com/26040955/83718830-c6cb9480-a670-11ea-8c79-c37b8b5da2e5.png)

- JVM에서 실행되는 자바 바이트 코드를 거치는 것까지는 동일하지만 마지막 두 단계가 다르다.
  * Dex 컴파일러는 여러 개의 .class 파일을 하나의 .dex파일로 변경하여 DVM에서 실행가능하도록 만든다.
  * 그 다음 Resource들과 .dex파일을 압축하여 하나의 apk를 만들게 된다.

### DVM 장점
- Register 기반의 가상 머신
  * stack을 이용하는 것이 아니라 피연산자들이 CPU의 register에 저장되어 사용된다. 스택 기반보다 메모리를 더 적게 사용하기 때문에 더 빠르다.
  ![image](https://user-images.githubusercontent.com/26040955/83732453-056c4980-a687-11ea-8785-a1d497ac3fbf.png)


## ART(Android Runtime)
- DVM에서 ART로 바꾸게 된 배경에는 컴파일러 변경을 통한 압도적 퍼포먼스 개선 때문이다.

### DVM과 ART의 컴파일 과정 비교

- DVM-JIT: 바이트 코드를 가상머신에서 기계어로 변환된 결과를 캐쉬에 저장하여 자주 사용되는 코드는 재사용을 하여 속도를 높인다. 다만, 메모리를 더 많이 사용해야 한다.
- ART-AOT: DVM의 JIT와는 달리 애플리케이션이 설치되는 시점에 애플리케이션 전체 바이트 코드를 기계어로 번역. 처음 설치는 좀 더 오래 걸리지만, 런타임 시 바이트 코드를 해석하는 부분이 없어졌기에 성능이 높아지고 배터리 수명이 늘어났다.

### DVM와 ART의 GC 비교
- 둘 다 CMS GC 알고리즘을 사용하는데 자세한 건 [Java Garbage Collection](https://d2.naver.com/helloworld/1329)을 참고하자.
- 간단하게 말하면 DVM은 stop-the-world 2회, ART은 stop-the-world 1회로 ART가 더 성능이 좋다.
  * stop-the-world가 자주 발생하면 사용자가 보는 UI 멈춤 등이 발생 가능.

- 사실 이 부분은 너무 어렵긴하다.... 여유로울 때 한번 뜯어보자!!!
  * [구글 안드로이드 - ART 가비지 컬렉션 디버깅하기](https://source.android.com/devices/tech/dalvik/gc-debug)

### 참고자료
- [JVM, DVM, ART 이해하기](https://www.charlezz.com/?p=42686)
  * 위의 대부분 내용은 해당 사이트에서 참고했다.
- [Stack based vs Register based Virtual Machine Architecture, and the Dalvik VM](https://markfaction.wordpress.com/2012/07/15/stack-based-vs-register-based-virtual-machine-architecture-and-the-dalvik-vm/)
- [java 의 jvm 구동 관련](https://okky.kr/article/670043?note=1881229)
- [Is a Dalvik virtual machine instance created for each application?](https://stackoverflow.com/questions/13577733/is-a-dalvik-virtual-machine-instance-created-for-each-application/13577973)
- [Dalvik Virtual Machine](http://beyondthegeek.com/2016/08/15/dalvik-virtual-machine/)
- [구글 안드로이드 - Android 런타임 및 Dalvik](https://source.android.com/devices/tech/dalvik)
