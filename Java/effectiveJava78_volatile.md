### volatile을 사용하기 적절한 때

- volatile는 가시성은 제공하지만 경합 조건일 때 보장하지 못하는 단점이 있다. 따라서 오직 한 쓰레드만 이 변수에 읽기/쓰기 작업을 하고,
다른 쓰레드들은 읽기 작업만 하는 상황이라면 volatile 선언이 잘 쓰일 수 있다.

- volatile 키워드는 JVM의 성능 향상을 위한 코드 재정리 기술도 막을 수 있기에 가시성 보장이 반드시 필요한 경우에만 사용되어야 한다.

### Effective Java Item 78

```java
public class helloworld {
    private static boolean stopRequested;

    public static void main(String[] arg) throws InterruptedException{
        Thread backgroundThread = new Thread (() -> {
            int i = 0;
            while(!stopRequested)
                i++;
        });
        backgroundThread.start();

        TimeUnit.SECONDS.sleep(1);
        stopRequested = true;
    }
}
```
위 프로그램은 실행 시 끝나지 않는데... OpenJDK JVM 끌어올리기 기법(hoisting)이라는 최적화에 의해 아래와 같이 바뀌기 때문이다. 

```java

//기존 코드
while(!stopRequested)
  i++;

//최적화 코드
if(!stopRequested)
  while(true)
    i++;
```

- hoisting은 loop 변수를 끌어올리는 기법인데, 위에서도 stopRequested의 값이 불변한다고 생각해서 저렇게 최적화한 것 같다.
- 따라서 위 프로그램이 끝나게 하려면, stopRequested에 volatile 키워드를 붙이거나 while문 안에서 stopRequested를 true로 변경시켜줘야 한다.
그렇게 되면 volatile 키워드는 main memory로부터 읽고 쓴다는 것이기에 바뀔 여지가 있고.. 후자는 말 안해도...
