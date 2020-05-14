### Object Level Lock
- Object Level lock은 instance 수준의 lock. 즉, 같은 instance가 재진입하는 것을 막는 용도.
- 하나의 class에 count 변수를 ++하는 것 같은 경우. object lock으로 원자성을 보장할 수 있다.
- non-static, non-static code block을 thread-safe하게 가능.
```java
//첫번째 방법
synchronized(this){
  ...
}

//두번째 방법
private final Object lock = new Object();
synchronized(lock){
  ...
}

//세번째 방법
public synchronized void demoMethod(){}

```
### Class Level Lock
- class로 생성한 모든 객체가 관여되는 lock. 즉, class에서 오직 하나의 객체만 해당 블럭을 진입할 수 있다.
- static method 같은 경우 class level lock으로 해야 된다. 그렇기에 singleton에서 class level lock을 사용하는 것.

```java
//첫번째 방법
private static final Object lock = new Object();

synchronized(lock){
  ..

}

//두번째 방법
synchronized(class명.class){
  ...
}

//세번째 방법
public synchronized static void demoMethod(){
 
}

```

### .class로 Class Level Locking이 가능한 이유
- Class의 object들은 class의 정보를 Class.class로부터 가져오게 되는데, Class.class를 lock하게 되면 class의 모든 객체는 대기할 수 밖에 없는 것.

### 참고자료
- https://howtodoinjava.com/java/multi-threading/object-vs-class-level-locking/
