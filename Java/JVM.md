### Java가 왜 Platform Independent Language인지 JVM으로 설명

- JVM이 컴퓨터의 언어로 컴파일된 Byte Code를 실행
- JVM은 Platform(OS)에 종속: 개발자가 Platform과 상관없이 코드를 작성하면 platform에 맞추어 JVM이 실행하게 된다.
  - 처음에 작성한 Java 파일을 컴퓨터가 이해하기 위한 바이트 코드로 변경하기 위해 아래와 같이 compile을 하게 되는데, java파일을 class파일(바이트 코드)로 변경
  하게 된다. 이러한 class파일(바이트 코드)를 JVM에서 실행.
  - 사실 바이트 코드는 자바 언어와 기계어의 중간 단계이다.

<img width="607" alt="스크린샷 2020-05-04 오후 2 45 44" src="https://user-images.githubusercontent.com/26040955/80938956-f428e680-8e15-11ea-8ddf-5e1576270862.png">

### KeyWord check

- JVM은 컴파일된 byte code를 실행시켜주는 executor이며, platform에 dependent한 성격을 가짐.
- 이런 덕분에 개발자는 플랫폼에 상관없이 개발할 수 있는 개념인 cross Platform을 가지게 된다.

## JVM(Java Virtual Machine)

- Java 코드를 컴파일해서 얻은 바이트 코드를 해당 운영체제가 이해할 수 있는 기계어로 바꿔주는 역할을 한다.
- JVM은 크게 4가지(Class Loader, Execution Engine, Garbage Collector, Runtime Data Area)가 있다.
  * Class Loader: 컴파일된 class파일들을 os로부터 할당받은 영역인 Runtime Data Area에 적재한다.
  * Execution Engine: Class Loader에 의해 적재된 class파일들을 기계어로 변경해 명령어 단위로 실행하는 역할을 한다.
  * Garbage Collector: Heap 메모리 영역에 생성된 객체 중에 참조되지 않은 객체들을 탐색 후 제거하는 역할.
  * Runtime Data Area: 자바 애플리케이션을 실행할 때 데이터가 적재되는 곳.
  
![image](https://user-images.githubusercontent.com/26040955/80939621-35ba9100-8e18-11ea-86e9-b41fa4b31177.png)

### Execution Engine의 두 가지 컴파일 방식
- Interpreter
- JIT(Just-In-Time)

### Runtime Data Area의 세부 구조
![image](https://user-images.githubusercontent.com/26040955/80940485-e033b380-8e1a-11ea-930d-773559635150.png)

- Method Area: 클래스 이름, 타입 등의 정보랑 <b>static 변수</b>, <b>constant pool</b>, <b>final class 변수</b> 등이 생성되는 영역이다.
- Heap Area: new 키워드로 생성된 객체나 배열이 저장. GC가 참조되지 않은 메모리를 확인하고 제거하는 영역
- Stack Area: 지역 변수, 파라미터, 리턴 값 등이 저장되는 영역
  * Person p = new Person();이라는 코드를 작성했을 때, p라는 변수는 stack에 저장되며 객체의 주소값을 가지고 있고 new Person() 객체는 Heap 영역에 저장된다.
- PC Register: Thread가 생성될 때마다 새로 생겨서 각 thread가 독립적인 실행 흐름을 가질 수 있도록 한다.
- Native method stack: 자바외 언어로 작성된 네이티브 언어(C, C++)를 위한 메모리 영역
  * JNI(Java Native Interface)
- Method Area와 Heap Area는 Thread끼리 공유/ Stack, PC Register, Native method stack은 공유하지 않는다.

### Heap Area && GC(Garbage Collector)

- 힙 영역은 GC의 주요 대상이다. 과정은 Minor GC와 Major GC로 나뉜다.
- Minor GC
  * 최초에 객체가 생성되면 Eden영역에 생성.
  * Eden영역이 꽉차게 되면 GC 후에 살아남은 객체가 Survivor1으로 복사
  * Survivor1 영역이 가득 차게 되면 GC 후에 살아남은 객체를 Survivor2로 복사
  * 이 과정을 반복하다가 Survivor2에서 살아남은 것이 Old 영역으로 복사

- Full GC
  * Old 영역은 기본적으로 가득 차면 GC 실행.
  * Minor GC보다 훨씬 오래 걸리고 실행 중에 GC를 제외한 모든 쓰레드가 중지한다.(stop-the-world) 따라서 Full gc가 일어나는 정도와 소요 시간은 Application의 성능과 안정성에
  아주 큰 영향을 준다.
  * 최대한 많은 Heap 영역을 확보하기 위해 stop-the-world 시행.

### Android 개발자가 JVM에 대해 알아야 하는 이유

- 메모리 누수에 대해 잘 컨트롤하고 관리할 수 있어야 Application의 과부하나 gc로 인한 성능 저하를 막을 수 있다.
- real time service 같은 경우 full gc로 인해 잠시 멈추는 것이 사용자의 Application 사용 편의성을 해치게 된다.

### 출처
- 인프런 '호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25'
- [JVM 구조와 자바 런타임 메모리 구조 (자바 애플리케이션이 실행될 때 JVM에서 일어나는 일, 과정을 설명해줄 수 있나요?)](https://jeong-pro.tistory.com/148)
- [Naver D2 Java Garbage Collection](https://d2.naver.com/helloworld/1329)
- [JVM GC와 메모리 튜닝 (조대협)](https://5dol.tistory.com/183)
- [Why does the JVM full GC need to stop-the-world?](https://stackoverflow.com/questions/16695874/why-does-the-jvm-full-gc-need-to-stop-the-world)
- [Garbage Collection explained for Android Developers (and other JVM Platforms)](https://android.jlelse.eu/garbage-collection-explained-for-android-developers-and-any-other-jvm-language-ac5896bc8875)
