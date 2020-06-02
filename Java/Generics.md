## Generic이란?
- 다양한 타입의 객체들을 다루는 메서드나 클래스에 컴파일 시에 타입 체크를 해주는 기능
- 아래처럼 의도하지 않은 타입이 들어오는 걸 막아서, 객체의 타입 안정성을 높이고 형변환의 번거로움이 줄어들게 된다.
```java
ArrayList<String> stringList = new ArrayList<>();
stringList.add(1); //컴파일 시 에러
stringList.add(222.2); //컴파일 시 에러
stringList.add("zzz");
```

### Generic 사용법

- 일반적인 사용법
  * T라고 붙이는 건 관례. 사실 저렇게 하지 않아도 동작은 함.

```java
public class Box<T>{
  List<T> arrayList;
}

public class Main{

  public static void main(String[] args){
    Box<Apple> box1 = new Box<Apple>();
    Box<Fruit> box1 = new Box<Apple>(); 
    //만약 Apple이 Fruit을 상속받았다고 해도 이와 같이 대입할 수 없다.
    //제너릭은 명확히 타입이 일치해야 한다.
  }

}
```

- 제한된 제너릭
  * 아래와 같은 방식은 Fruit를 상속받는 타입만 들어올 수 있다.
```java
public class Box<T extends Fruit>{
  List<T> arrayList;
}
```

### 제너릭 메소드
```java

//return 타입: T
//매개변수: List<T>
public <T> T foo(List<T> list){
}

//범위 제한 제너릭 메소드
public <T extends Fruit> T foo(List<T> list){
}
```

- 제너릭 클래스의 타입 매개변수와 제너릭 매서드의 타입 매개변수는 서로 다른 것이다.
  * 아래와 같이 코드를 작성했을 때 에러가 나지 않는 이유는 제너릭 메소드를 적용했기에 Integer가 대입될 수 있는 것이다.
  * 만약 foo메소드 앞에 <T>를 지운다면 컴파일 에러가 아래와 같이 발생한다.
```java

public class TestGenerics <T> {
    T data;

    TestGenerics(T data){
        this.data = data;
    }

    public <T> void foo(T t1){
        System.out.println(t1.getClass());
        System.out.println(data.getClass());
    }
}

public class helloworld{

    public static void main(String[] args){

        TestGenerics<String> t = new TestGenerics<String>("This is String class");
        t.foo(1);
    }
}

```

### 와일드 카드

- 어떤 타입이든 가능하다는 뜻
```java
//아래와 같이 매개변수를 선언하면 List<String>과 같은 List는 매개변수로 들어가지 못한다.
//정확히 List<Object>만 들어올 수 있음.
public void getList(List<Object> list){
  
}

//하지만 아래와 같이 와일드카드를 적용하면 가능
public void getList(List<? extends Object> list){
  
}
```


### 참고자료
- [우아한Tech - [10분 테코톡] 💫두강의 Generics](https://www.youtube.com/watch?v=n28M8iryFPw)
