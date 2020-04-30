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
