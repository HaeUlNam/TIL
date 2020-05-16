## DeadLock
- 공유 자원에 접근하기 위해 Semaphore S와 Q가 필요로 한다고 가정하자. 아래와 같이 두 개의 Process가 S와 Q를 하나씩 들고 있을 때, 다른 하나에 대해 요청을 하게 되면 얻지
못하는 상황이 발생해서 서로 기다리기만 하는데 이 상황을 'DeadLock'이라고 한다.

![스크린샷 2020-05-16 오후 3 16 29](https://user-images.githubusercontent.com/26040955/82112469-3b08cb80-9788-11ea-8293-9631b43bab5a.png)


### DeadLock 성립 조건 4가지
- 상호 배제: 한 순간에 오직 하나의 Proceess만 자원을 사용할 수 있다.
- Hold and wait: 하나 이상의 자원을 가진 Process가 다른 자원을 획득하기 위해 기다린다.
- No preemtion: 점유된 자원을 빼앗을 수 없다.
- circular wait: 원형 구조로 자원을 획득하기 위해 기다린다.

### DeadLock 예시
- Process-> Resource: request
- Resource-> Process: holding

![스크린샷 2020-05-16 오후 3 21 30](https://user-images.githubusercontent.com/26040955/82112567-edd92980-9788-11ea-9e98-9f82a0017d83.png)



### DeadLock 해결책
- Deadlock prevention: Deadlock의 4가지 조건을 만족하지 못하도록 막는다.
- Deadlock avoidance: 요청에 대한 사전 정보가 있다면, 자원 할당 그래프를 통해 safe한 것만 자원을 할당시켜준다.
- Deadlock detection: Deadlock을 허락하는 대신 detection해서 자원을 다른 곳에 주거나, process를 종료시키는 방법으로 deadlock이 풀릴 때까지 진행.
