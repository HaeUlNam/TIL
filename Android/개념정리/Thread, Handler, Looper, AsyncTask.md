### Android Main UI Thread

- 안드로이드 UI Thread는 기본적으로 싱글 스레드로 동작하여 이를 잘 고려하여 개발해야 한다.
- 메인 스레드는 안드로이드의 주요 컴포넌트(4대)를 실행하는 곳이자 UI를 그리거나 갱신하는 일을 담당.
- Class ActivityThread의 main함수가 4대 component의 entry point이다. 메인 스레드를 담당.
- UI 스레드는 매번 16ms마다 update되기에 16ms 안에 logic을 처리할 수 있도록 한다.

## Callback

- 역할: main thread를 blocking하지 않기 위해서는 callback을 사용해야 한다. callback을 사용하면 오랜 시간동안 걸리는 처리를 background thread에서 할 수 있다. 끝나게 되면 결과를 main thread에 전달.
- 단점1: callback을 너무 많이 쓰게 되면 읽기 어려운 코드가 되고, 왜 그렇게 동작하는지 설명하기 어렵다. 코드는 순차적으로 동작하는데 callback은 asynchronous하게 동작하기 때문이다.
- 단점2: 자바의 exception과 같은 언어의 특징을 살리지 못한다. 

### 4대 Component 생성 Flow
1) Activity Manager Service-> Zygote Process에게 ActivityThread 생성 요청
2) Zygote Process는 fork()를 하고 그 위에 ActivityThread를 올려서 main()으로 시작!
  * 기존의 component를 실행시키기 위한 준비된 process를 fork하여 성능을 증가시킨다.
  * 성능이 증가되는 이유는 COW(Copy On Write) 때문인데, 공통된 부분을 부모 프로세스와 자식 프로세스가 메모리 공간을 공유한다. 따라서 복사할 때
  참조만 하게 되어 성능이 증가하는 것.

### 싱글 스레드 모델의 규칙

1) 메인 스레드를 블럭하지 말 것
  - 만약 긴 스레드를 메인에서 담당하면 App의 반응성이 낮아지고, 시스템이 App을 ANR(Application Not Response) 상태로 변경할 수도 있습니다.
2) 안드로이드 UI 툴킷은 오직 메인 스레드에서 접근하도록 하기.

- 따라서 background 스레드와 메인 스레드 간의 통신 방법이 필요.
  * Looper와 Handler 사용
  * HanlderThread
  * AsyncTask: Thread나 Message Loop 등의 작동 원리를 크게 고러하지 않고도 사용이 가능.

### Looper와 Handler 동작 방식
- 메인 스레드는 내부적으로 Looper를 가지며 그 안에는 Message Queue가 존재.
- Message Queue는 메인 스레드가 다른 스레드 or 자기 자신으로부터 전달받은 Message를 순차적으로 처리하기 위한 Queue.
- Looper는 Message Queue에서 Message나 Runnable 객체를 Handler로 전달
- Handler는 Looper로부터 받은 메세지를 처리하거나 다른 스레드로부터 Message를 받고 Message Queue로 넣는 역할.
- 가장 중요한 것은 메세지를 전달해주는 Looper, 메서지를 선입선출하는 MessageQueue, 다른 스레드와 통신 또는 Message를 처리하는 Handler 3개는 같이 있어야
의미 있다. 이들은 모두 하나의 Thread에 종속된다.

<img width="546" alt="스크린샷 2020-05-02 오후 5 08 09" src="https://user-images.githubusercontent.com/26040955/80858880-8060cf80-8c97-11ea-98d3-154fe9339961.png">


### Looper와 Message Queue
- Looper 역할: 무한 루프를 돌면서 자신이 속한 스레드의 Message Queue에 들어온 Message나 Runnable 객체를 차례로 꺼내서 Handler에 전달
- 메인 스레드는 기본적으로 Looper가 있지만, 다른 스레드들은 Looper가 없기에 메세지를 받을 수 없다. 따라서 Looper를 prepare로 생성하고, loop()으로 반복적으로 Handler에 message 전달. quit()시 Loop 종료.

### Message와 Runnable

- Message: int와 object와 같이 스레드 간 통신할 내용을 담는다.
  * 일반적으로 새 Message 같은 경우 안드로이드 시스템에서 만들어 둔 Message Pool로부터 가져와서 사용한다.
- Runnable: run()메세드와 그 내부에서 실행될 코드를 담는다.
  * 자바의 Thread 생성 방식 두 가지: Thread 상속, Runnable Implement

### HandlerThread

- 기본으로 Looper를 가지고 있는 class. 다른 스레드에서 Looper를 따로 생성해야 하는 불편함이 없어진다.
- 자동으로 Looper 내에 MessageQueue도 생성되기에 Hanlder로부터 Message나 Runnable을 전달받을 수 있다.

### AsyncTask

- 스레드나 메세지 루프 등의 작동 원리를 몰라도 하나의 클래스로 UI와 background 스레드 작업을 쉽게 할 수 있도록 안드로이드에서 제공하는 클래스.
- 동작 방식
  1) onPreExecute(): background 스레드 동작하기 전에 처리해야 할 일(?)
  2) doInBackground(): 시간이 오래 걸리는 작업(통신.. 등등)
  3) onProgressUpdate(): 도중에 UI 작업이 필요할 경우, doInBackground()에서 publishProgress()를 호출해서 사용.
  4) onPostExecuted(): 후처리

- 단점
  * 하나의 객체이므로 재사용이 불가.. / 객체를 새롭게 생성하면 되지만 메모리 효율이 낮아진다.
  * 짧은 시간이 걸리는 것에는 AsyncTask가 편리하지만, 오래 걸리는 작업에서는 반응성이 낮아지기에 Thread를 사용.

<img width="631" alt="스크린샷 2020-05-02 오후 5 54 37" src="https://user-images.githubusercontent.com/26040955/80859741-fec07000-8c9d-11ea-8026-d76e5e846426.png">


### 참고

- [안드로이드 백그라운드 잘 다루기 Thread, Looper, Handler](https://academy.realm.io/kr/posts/android-thread-looper-handler/)
- [Java에서 Thread를 생성하는 방법](http://blog.naver.com/PostView.nhn?blogId=tkddlf4209&logNo=220487061964&categoryNo=0&parentCategoryNo=48&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)
- [Main Thread와 Handler 이해하기](https://junghun0.github.io/2019/09/07/android-thread-handler/)
- [안드로이드에서 AsyncTask를 활용한 스레드 동작](https://kim-hoya.tistory.com/44)
- [공식Android홈페이지-Multi-threading & callbacks primer](https://developer.android.com/courses/extras/multithreading)


