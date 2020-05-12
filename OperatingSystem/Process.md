### Process란?

- 실행 중에 있는 프로그램을 의미한다. 여러 개의 스레드를 가질 수 있다.
- PCB에 각 Process의 상태 정보를 저장하고 multiprocessing할 때 이를 꺼내서 사용한다.

### IPC(Inter Process Communication)

(1) message passing: 메세지가 커널을 거쳐서 보내진다.  
(2) shared memory: 둘 다 사용할 수 있는 공유 공간에서 메세지 주고 받기 진행. (커널 관여 x), 이 기능은 2개 이상의 프로세스가 같은 공간을 공유할 때
race condition이 일어나지 않도록 조심해야 한다.
![image](https://user-images.githubusercontent.com/26040955/80728969-8a24ee80-8b42-11ea-9aed-ac6371395b3d.png)

### 참고
- https://d2.naver.com/helloworld/47656
