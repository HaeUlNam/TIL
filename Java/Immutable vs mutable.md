### Wrapper Object - Immutable

```java
public class helloworld {

    public static void main(String[] arg) {
        Integer aa = 0;

        changeValue(aa);
        System.out.println(aa); //result is 0 이다. Integer가 Immutable 속성을 가지기 때문이다.
    }

    private static void changeValue(Integer bb){
        bb += 10;
    }
}
```
- 첨에 아래 코드에서 출력값이 10일 것이라고 생각했지만, 실제로는 10이었다. 왜 그랬을까?
- Wrapper Object들이 Immutable(불변)하기 때문이다. Wrapper object들은 생성자에 의해 생성되는 순간에만 초기화되고, 그 이후에는 불가능하다.
실제로 Wrapper Class 중에 하나인 Integer의 값을 나타내는 변수는 아래와 같이 정의되어 있다고 한다.
```java
private final int value;
```

- 따라서 changeValue 함수의 Actual-Parameter는 처음에 main함수의 aa가 가리키는 객체 주소값을 가지고 있다가 + 연산이 하게 되면, 새로운 객체를 할당해서
변경된 값을 할당하게 된다. 따라서 bb 지역변수에는 새로운 객체의 주소값이 들어가 있는 것이다.

### Custom Integer - mutable
- 그럼 custom Integer를 만들어서 final을 안 붙이면 변할 수 있을까? 당연하다.. 아래의 결과는 10!

```java
public class FakeInteger {
    private int value = 0;

    FakeInteger(int value){
        this.value = value;
    }
    void sum(int sumValue){
        this.value += sumValue;
    }

    int getValue(){
        return this.value;
    }
}

public class helloworld {

    public static void main(String[] arg) {
        FakeInteger aa = new FakeInteger(0);

        changeValue(aa);
        System.out.println(aa.getValue()); //result is 10 이다. FakeInteger의 value는 final이 아니니깐!
    }

    private static void changeValue(FakeInteger aa){
        aa.sum(10);
    }
}

```

### Custom Integer - Immutable

- 위의 custom Integer의 멤버변수인 value에 final 키워드를 붙이면 어떻게 될까? 죄다 빨간 줄이다. final 키워드를 붙이면 1번 초기화 이후에
값을 변경할 수 없다. 그럼 Integer를 동일하게 구현할 수 없는가? 없다. 그 이유는 아래 2가지 때문이다.
1) Autoboxing과 Unboxing 같은 경우 compiler에서 자동으로 변환해주는 것이기에 이를 구현해서 compiler할 방법이 없다.
2) Java는 연산자 overloading를 지원하지 않기에 불가능하다. 

### String(Immutable) vs StringBuffer(mutable)

- 결론부터 이야기하면 StringBuffer를 사용하는 것이 String을 사용하는 것보다 메모리 상 더 좋다.
- String은 Immutable하기에 +연산을 하면 지속적으로 객체를 생성하고, StringBuffer는 mutable 하기에 기존 객체에 +연산하게 되기 때문이다.
- 참고로 String은 wrapper class가 아니다. char의 Wrapper Class는 Character이다.
    * 참고: [Can we call String as a wrapper class?](https://stackoverflow.com/questions/6594380/can-we-call-string-as-a-wrapper-class)

```java

String s1 = "South Korea ";
s1 += "Seoul"; //"South Korea Seoul"을 가진 새로운 객체 생성

StringBuffer s2 = new StringBuffer("South Korea");
s2 += "Seoul"; //기존에 객체에 덧붙이기

```

### StringBuffer(mutable) vs StringBuilder(mutable)

- 둘 다 동일하게 mutable하다. 하지만 StringBuilder는 StringBuffer보다 속도가 빠릅니다. 그 이유는 synchronization 지원 여부 때문이다.
- StringBuffer는 Synchronous하지만, StringBuilder는 Non-synchronous하다.
- 단일 스레드에서는 StringBuilder > StringBuffer, 멀티 스레드에서는 StringBuffer > StringBuilder


### 참고자료
- [자바 메모리 관리 - 스택 & 힙](https://yaboong.github.io/java/2018/05/26/java-memory-management/)
- [Is autoboxing possible for the classes I create?](https://stackoverflow.com/questions/17619724/is-autoboxing-possible-for-the-classes-i-create)
