### Singleton 패턴
- 단 한번의 객체 생성을 해서 해당 객체를 반복적으로 사용하는 것.
- 장점: 메모리를 줄일 수 있다. Caching된다.
- 단점: Singleton으로 만든 객체의 역할이 복잡하다면 해당 싱글턴 객체를 사용하는 다른 객체간의 결합도가 높아져서 객체지향 설계 원칙에 어긋나게 된다.
  * 여기저기서 다 참조해서 사용하다가 요구사항 변경 시에 개발자가 이를 다 변경하는데 resource가 많이 들기에 OCP에 위반되게 된다.(전역변수를 쓰지 말아야 하는 이유와 동일)
  * 따라서 잘 고민하고 사용해야 한다.
  

### Singleton 패턴 코드 작성법

- 프로그램 실행 시 객체 생성

```java
public class ExampleClass {
    //Instance
    private static ExampleClass instance = new ExampleClass();

    //private construct
    private ExampleClass() {}

    public static ExampleClass getInstance() {
        return instance;
    }
}
```

- lazy init

```java
public class ExampleClass {
    //Instance
    private static ExampleClass instance;

    //private construct
    private ExampleClass() {}

    public static ExampleClass getInstance() {
        if(instance == null) return instance = new ExampleClass();
        return instance;
    }
}
```

- Thread Safe + Lazy init: Thread safe하지만, 성능이 그렇게 좋지 않아서 권장하는 방법은 아니다.

```java
public class ExampleClass {
    //Instance
    private static ExampleClass instance;

    //private construct
    private ExampleClass() {}

    public  static synchronized ExampleClass getInstance() {
        if(instance == null) return instance = new ExampleClass();
        return instance;
    }
}
```

- Thread Safe + Lazy init + Double-checking Lock: 위보다 성능을 더 낮출 수 있었다.
  * 하지만 [Double-checking Lock](https://github.com/HaeUlNam/TIL/blob/master/DesignPattern/Singleton_DCL%EC%9D%84%20%EC%93%B0%EB%A9%B4%20%EC%95%88%EB%90%98%EB%8A%94%20%EC%9D%B4%EC%9C%A0.md)은 사용하면 안되는 방법 중에 하나이다. 그 이유는 링크를 타고 들어가면 된다.
  * 만약 사용할 거면 volatile 키워드를 사용해서 reodering을 하지 않도록 한다.
```java
public class ExampleClass {
    //Instance
    private static ExampleClass instance;

    //private construct
    private ExampleClass() {}

    public  static ExampleClass getInstance() {
        if(instance == null){ //null인 것만 동기화 block
          synchronized (ExampleClass.class) { //존재하는 모든 class 객체에 lock을 거는 것.
                if(instance == null)//대기 도중에 생성되면 안되기에 null check 한번 더!
                    instance = new ExampleClass();
            }
        }
        return instance;
    }
}
```

- Thread Safe + Lazy init + Holder를 이용
  * 클래스안에 Holder(클래스)를 두어 JVM의 class Loader와 class가 로드되는 시점을 이용한 방법
  * 중첩클래스인 Holder는 getInstance가 호출되기 전까지는 참조되지 않으며, 최초로 호출될 때 class loader에 의해 객체를 생성해서 return합니다.
  * Holder를 이용하는 건 DCL과 달리 Thread-safe하다. 왜냐하면 class loader 자체가 lock을 사용하기에 처음에 객체를 생성하는 행위가 원자적(atomic)하다고 할 수 있다.

```java
public class ExampleClass {
    //private construct
    private ExampleClass() {}
    
    private static class SingleTonHolder{
      private static final ExampleClass instance = new ExampleClass();
    }
    
    public static ExampleClass getInstance() {
        return SingleTonHolder.instance;
    }
}
```


### 참고자료
- [Java에서 싱글톤(Singleton) 패턴을 사용하는 이유와 주의할 점](https://elfinlas.github.io/2019/09/23/java-singleton/)
- [](https://jongyoungcha.tistory.com/entry/%EC%8B%B1%EA%B8%80%ED%84%B4-%ED%8C%A8%ED%84%B4%EC%9D%98-%EC%9E%A5%EC%A0%90%EA%B3%BC-%EB%8B%A8%EC%A0%90)
- [Multi Thread 환경에서의 올바른 Singleton](https://medium.com/@joongwon/multi-thread-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C%EC%9D%98-%EC%98%AC%EB%B0%94%EB%A5%B8-singleton-578d9511fd42)
- [Does the Java ClassLoader load inner classes?](https://stackoverflow.com/questions/24538509/does-the-java-classloader-load-inner-classes)
