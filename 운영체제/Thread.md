## Thread란?

- 프로그램 실행의 단위로 하나의 프로세스는 여러 개의 스레드로 구성이 가능하다.
- 아래 사진을 보면 thread는 각자 고유의 stack과 register를 가지고, code/heap 등의 영역은 공유한다.
- context switching: 기존의 thread 상태 정보를 register와 stack에 저장하고 다음 실행할 thread를 가져오는 것.
- 보통 싱글 CPU에서는 한순간에 하나의 thread만 실행되지만, 요즘 같은 멀티 CPU 환경에서는 한순간에 여러 thread 실행이 가능하다.

![image](https://user-images.githubusercontent.com/26040955/80710265-846edf00-8b29-11ea-9b9d-5effe9cb643f.png)


### register와 stack의 역할

- stack의 역할: 함수 호출 시 전달되는 인자, 되돌아갈 주소값 및 함수 내에서 선언하는 변수 등을 저장하기 위한 메모리 공간

- register의 역할: pc(program counter)의 경우 현재 명령어를 어디까지 수행했는지를 나타내준다. 따라서 context switching하여 cpu를 할당받았다 빼앗기게
 된다면 어디까지 명령어를 실행했는지를 pc에 저장한다. 이외에도 여러 register들을 저장해두고, 꺼내쓰게 된다. 
 
- 위와 같은 stack와 register의 역할 덕분에 각각의 thread는 독립적인 실행 흐름을 가지게 된다.


### Thread의 장점 
- <b>프로세스</b>보다 쓰레드간 context switching 시간이 짧다. 자원을 공유하기도 하면서 PCB를 통째로 불러오지 않아도 되기에..
- <b>IPC(Inter Process Communication)</b>와 달리 Heap 등의 자원을 공유하기에 커널의 도움없이 상호간에 통신이 가능하다.
- 프로그램 반응성 향상
  * Android에서 <b>main thread에서 UI 처리</b>, background thread에서 네트워크 처리를 통해 사용자가 답답함을 느끼지 않도록 할 수 있다.

### Thread의 단점
- 공유 자원에 접근하는 멀티 스레드 코드를 디자인하는 것은 굉장히 어렵다..
- 자원 소비의 증가: 많은 스레드를 생성하는 것은 시스템 과부하를 일으키기도 한다.

### Critical Section(임계 영역)

- 다수의 스레드가 같은 공유 자원에 접근할 때 발생한다. 다만, 쓰기 작업이 아니고 읽기 작업이라면 상관없다.
- 공유 자원에 대해 원자성(atomic)을 보장하더라도 동기화는 꼭 해야할 필요성이 있다. 그 이유는 가시성 때문이다.

### 가시성(visibility)

- 대부분 현대 시대 시스템은 여러 CPU를 탑재하고 있는데, 이러한 CPU는 아래와 같이 각각 다른 Cache Memory를 가지게 된다.
- 그런데 프로그램 로직에 의해 데이터가 변경되어 Cache에 저장된다고 해서, 이 값이 바로 main memory로 저장되는 것이 아닙니다. 따라서, 
아래 그림과 같은 경우 각 CPU 간의 로컬 Cache가 불일치하는 Cache coherence가 발생하게 됩니다.

![image](https://user-images.githubusercontent.com/26040955/80720701-3f05de00-8b38-11ea-80f6-1ba0d442c92d.png)

### 가시성을 보장하기 위한 방법

(1) [volatile](https://github.com/HaeUlNam/TIL/blob/master/Java/volatile.md) 선언: 특정 변수에 대한 읽기 작업은 반드시 메인 메모리로부터 수행하고, 쓰기 작업은 항상 메인 메모리에 즉각 반영하도록 
 강제할 수 있다.
다른 CPU로부터 변경된 값을 읽어올 수 있도록 하기 위해 하는 것.

(2) <b>synchronization</b> 키워드: volatile는 가시성만 보장할 수 있지만, synchronization 키워드는 가시성뿐만 아니라
하나의 한 스레드만 접근할 수 있도록 한다. (경합 조건의 해결책)

### 동시성과 병렬성의 차이

- 동시성: 싱글 코어에서 멀티 스레드를 작동시키기 위함.
- 병렬성: 멀티 코어에서 멀티 스레드를 작동시키기 위함.

### 참고 자료

- [goodgid님의 쓰레드란 무엇인가?](https://goodgid.github.io/What-is-Thread/)
- [Context Switching이란?](https://jeong-pro.tistory.com/93)
- [자바 컨커런시/멀티쓰레딩 튜토리얼_시리즈](https://parkcheolu.tistory.com/5?category=654619)
- [안드로이드 메인 스레드](https://codetravel.tistory.com/9)
- effective Java 3/E
