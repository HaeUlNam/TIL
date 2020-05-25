## Transcation이란?

- DBMS는 보통 많은 user나 프로세스가 동시에 접근하게 되는데, Transaction이 여기에서 생겨나는 동기화 문제를 해결해준다.
- 하나의 단위로만 작업이 일어나도록 트랜잭션이 보장.
  * 계좌 이체


## ACID 
- ACID는 Transaction의 속성으로서 Atomic, Consistent, Isolated, Durable이 있다.

### Atomic
- Atomic: 전체 Transaction은 쪼갤 수 없다.
- 예시1) A에서 B로 50달러의 돈을 보내는 상황
![스크린샷 2020-05-25 오후 8 33 29](https://user-images.githubusercontent.com/26040955/82809405-ffc47600-9ec6-11ea-8191-7c01534e856f.png)
  * 만약 위 상황에서 step 3와 step 6 사이에 fail이 발생한다면, 돈은 없어지는게 된다.
  * 따라서 위와 같이 원자성이 지켜지지 않는 상황을 막아야 하기에 중간에 오류가 나면 rollback 등을 통해 원래대로 되돌린다.

### Consistent
- DB의 제약은 보존되어야 한다.


### Isolated


### Durable

