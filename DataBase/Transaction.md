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
- Transaction 수행 중에는 inconsistant하지만, Transaction 전후로 DB의 제약은 보존되어야 한다.
- 명시적인 무결성 제약
  * 예를 들어, A-> B인 계좌 이체 상황에서 A + B의 합은 항상 동일해야 하는 제약.

### Isolated

- Transaction을 수행 시 다른 트랜잭션의 연산 작업이 중간에 끼어들지 못하도록 하는 것.
- 순차적으로 돌리면 Isolation이 보장된다.
- 하지만 성능 상의 이점 때문에 Isolation level에 따라 이를 중간에 허용하기도 한다.

- 예시) 두 개의 트랜잭션
 * T1과 T2가 순서를 가지며 중간에 끼어들지 못하도록 해야 한다.
![스크린샷 2020-05-25 오후 11 00 30](https://user-images.githubusercontent.com/26040955/82819570-8aaf6b80-9edb-11ea-8a95-478b0f53e0be.png)


### Durable

- 트랜잭션이 성공적으로 끝나면, 해당 변화는 영구적으로 DB에 반영되어 시스템이 실패하는 상황이 오더라도 복구될 수 있게 한다.

### SQL 명령어
- BEGIN TRANSACTION: 트랜잭션 시작
- COMMIT: 트랜잭션 성공
- ROLLBACK: begin 전으로 돌리기


