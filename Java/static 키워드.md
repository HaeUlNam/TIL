### static이 의미하는 것은?

- JVM에 의해 class가 로딩되는 처음 순간에 메모리에 탑재된다.
- static은 객체가 아닌 '클래스'에 귀속되는 것들을 명시하기 위한 키워드이다. 따라서, static변수에 접근하기 위해서는 class이름.변수이름으로 접근한다.

```java
public class MyClass { 
  static int myStaticVariable = 100; 
  int myVariable = 200; 
}

//출처: https://imasoftwareengineer.tistory.com/73 [삐멜 소프트웨어 엔지니어]
```
- 위와 같이 코드를 작성하면 메모리 공간에는 아래와 같이 할당된다.

![image](https://user-images.githubusercontent.com/26040955/81503355-23f85280-931e-11ea-957e-9fe3ffb59042.png)

- 위처럼 static 변수는 하나의 공간만 사용하고 여러 변수에서 참조가 가능하기에 마치 공유변수처럼 사용하게 된다.

### static method 안에 일반 변수를 참조할 수 없는 이유

```java
public class MyClass { 
  static int myStaticVariable = 100; 
  int myVariable = 200; 
  public void myMethod() { 
    myStaticVariable++; 
    myVariable++; 
    System.out.println(myStaticVariable); 
    System.out.println(myVariable); 
  } 
  public static void myStaticMethod(){ 
    myStaticVariable = 3; 
    myVariable = 4; // non-static field 'myVariable' cannot be referenced from static context 
  }
}
//출처: https://imasoftwareengineer.tistory.com/73 [삐멜 소프트웨어 엔지니어]
```

- 위와 같이 코드가 있을 때, myVariable = 4부분에서 error를 뱉을 것이다. 그 이유는 myVariable이라는 변수 자체가 MyClass라는 객체가 만들어지고 
Heap에 저장될 때 같이 저장되는 변수인것이다. 따라서, 메모리에 로딩되는 순간 MetaSpace에 넣어지는 static 변수, 메소드 안에는 static만 접근이 가능해야 한다.


### main 메소드가 static인 이유?

- main 메소드는 entry point로서 객체를 생성하지 않더라도 JVM에서 시작할 수 있어야 하기에, static으로 선언되어 프로그램 실행시 metaspace에 적재된다.


### static 단점

- 객체 지향적이지 않다: 캡슐화(정보 은닉) 등을 무시하고 여러 곳에서 참조가 가능하다.
- static은 GC의 관리 대상이 아니기에 메모리 관점에서 비효율이 있다.
- 여러 곳에서 변경 가능하기에 변경에 대한 예측이 어렵다..(유지 보수 측면?)


### Metaspace는 어디 있는가?

- 아래 그림은 Java 8 HotSpot JVM 구조이다.
- Metaspace는 Native Memory 영역임을 알 수 있다.
  * Native Memory: OS 관리 대상
  * 기존의 Perm은 JVM에 의해 크기가 강제되고 있었는데, Metaspace로 변경되고는 OS에서 자동으로 크기를 조절한다.
  * 기존의 Perm보다 Metaspace의 영역을 더 크게 사용할 수 있기에, Perm 영역 크기로 인해 java.lang.OutOfMemoryError는 더 보기 힘들어진다.

![스크린샷 2020-05-11 오전 12 56 33](https://user-images.githubusercontent.com/26040955/81504060-442a1080-9322-11ea-83d9-097ea9f56e57.png)

- 아래 그림은 기존의 Perm 영역인데 Perm의 static Object들은 기존에 GC 대상이었다.

![스크린샷 2020-05-11 오전 1 00 19](https://user-images.githubusercontent.com/26040955/81504182-cadeed80-9322-11ea-9719-a141db292175.png)

### 그럼 Perm -> Metaspace의 이점은?

- 개발자들은 더이상 제한된 Perm의 용량을 의식하지 않고 코딩할 수 있게 되었다. OS에서 Metaspace의 용량을 자동으로 조절해주기 때문이다.

### 참고 자료

- [9. 자바 static 변수 static 메서드](https://imasoftwareengineer.tistory.com/73)
- [Why are static variables considered evil?](https://stackoverflow.com/questions/7026507/why-are-static-variables-considered-evil)
- [JDK 8에서 Perm 영역은 왜 삭제됐을까](https://johngrib.github.io/wiki/java8-why-permgen-removed/)
