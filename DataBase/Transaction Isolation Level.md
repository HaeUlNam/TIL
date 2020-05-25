## Transaction Isolation Levels

- 아래와 같이 4단계로 이루어져 있다. serializable로 돌리면 데이터 무결성면에서 가장 좋지만 느리다. 따라서 성능을 향상시키기 위해서 위의 3단계가 필요하다.
  * Read uncommitted
  * Read committed
  * Repeatable read
  * Serializable
- 여러 개의 트랜잭션이 동시에 얼만큼 실행할 수 있는지를 개발자가 Isolation Level을 설정해주면 DBMS가 이에 맞추어 실행한다.


### Read uncommitted
- 아직 Transaction이 commit되지 않은 결과도 쿼리를 날리면 볼 수 있다.(Dirty Read)

### Read Committed
- commit된 결과만 읽을 수 있도록 하여 Dirty Read를 막아준다. 하지만 트랜잭션 도중 commit된 다른 트랜잭션의 결과를 반영하기에 
같은 트랜잭션 안에서 같은 쿼리가 다른 결과가 나올 수 있는 non-repeatable read가 가능

### Repeatable-Read
- 앞선 non-repeatable read를 막아준다. 이와 같이 같은 결과는 보장하지만 Insert와 같은 새로운 데이터가 들어오는 상황에서는 없던 데이터가 
트랜잭션 중에 일어날 수 있다는 것이다. 이것을 phantom read라고 한다.

### Serializable Read

- 모든 트랜잭션을 순차적으로 실행. 가장 안전하고 어떠한 비일관성 현상도 일어나지 않는다.

![image](https://user-images.githubusercontent.com/26040955/82823810-2ee8e080-9ee3-11ea-85e9-02bf746c4155.png)


### 상용 DBMS
- ORACLE: Read Committed 채택
- MySQL: Repeatable-Read 채택
- Serializable read를 선택하지 않는 이유는 성능을 조금이라도 높이기 위해서... 따라서 위에 언급한 각각의 문제 상황 phantom read, non-repeatable read
같은 경우 개발자가 신경써서 프로그램을 디자인해야 한다.

### 참고자료
- [DBGuide.net- 트랜잭션](http://www.dbguide.net/db.db?cmd=view&boardUid=148216&boardConfigUid=9&boardIdx=138&boardStep=1)
