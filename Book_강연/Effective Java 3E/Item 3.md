## private 생성자나 열거 타입으로 싱글턴임을 보증하라

### 싱글턴(Singleton)
- 싱글턴(Singleton)이란 인스턴스를 오직 하나만 생성할 수 있는 클래스를 말한다.
- 싱글턴으로 만들면 이를 사용하는 클라이언트를 테스트하기가 어려워질 수 있다.
  * 타입을 인터페이스로 정의한 다음 그 인터페이스를 구현해서 만든 싱글턴이 아니라면 싱글턴 인스턴스를 가짜(mock) 구현으로 대체할 수 없기 때문이다.

### 싱글턴 만드는 방식

1. public static final 변수에 class Loading Time동안 객체 생성/대입하도록 하여 단 하나의 인스턴스가 사용되도록 한다.
- 장점
  - 해당 클래스가 싱글턴임이 API에 명백히 드러난다. public static final이기 때문에..
  - 간결함
- 보통 단 한번 생성자가 호출되지만, 리플렉션(AccessibleObject.setAccessible)을 이용하여 private 생성자를 호출할 수 있다. 따라서 생성자 내부에 방어 로직을 작성해야 한다.
  * 방어 로직: 두 번 이상 생성자가 호출되면 exception
```java
public class Elvis {
   public static final Elvis INSTANCE = new Elvis();
   private Elvis() {
      /* 리플렉션 API에 대한 방어 로직 */
      if(INSTANCE != null){ 
          //throw exception
      } 
   }
   
   public void leaveTheBuilding() { ... } 
}
```

2. 정적 팩터리 방식으로 구현
```java
public class Elvis {
   private static final Elvis INSTANCE = new Elvis();
   private Elvis() {...}
   public static Elvis getInstance() { return INSTANCE; }
   
   public void leaveTheBuilding() { ... } 
}
```
- 장점
  - (마음이 바뀌면) API를 바꾸지 않고도 싱글턴이 아니게 변경할 수 있다는 점.
    - 예를 들어, 유일한 인스턴스를 반환하던 팩터리 메서드가 호출하는 스레드별로 다른 인스턴스를 넘겨주게 할 수 있다.
    - 이 경우 naming은 항상 새로운 Instance를 return하는 것이 아니기에 newInstance가 아니라 getInstance로 유지될 수 있다. (Item 1 static Factory 명명 규칙)
  - 정적 팩터리를 제너릭 싱글턴 팩터리로 만들 수 있다는 점
    - 이 부분의 대표적인 예는 Collections.reverseOrder 함수이다. 만약 reverseOrder가 아래와 같이 제너릭을 이용하여 타입 변환해주지 않는다면, 사용하는 모든 타입에 대한 함수가 필요하다.
      * SuppressWarning 같은 경우 타입이 안전하다고 생각할 때 사용해야 한다. (Item 27)
    ```java
    @SuppressWarnings("unchecked") 
    public static <T> Comparator<T> reverseOrder() { 
      return (Comparator<T>) ReverseComparator.REVERSE_ORDER;
    }
    ```
    - ReverseComparator에서 알게 된 점 
      - ReverseComparator를 보면 Comparator<Comparable<Object>>를 implement하고 있다. 이 뜻은 모든 Object와 비교할 수 있는(?)이라는 뜻.
      - 아래 compare을 재정의한 부분은 Collection.sort나 arrayList.sort등을 사용할 때 내부에서 사용된다.
    ![image](https://user-images.githubusercontent.com/26040955/90335788-43380780-e012-11ea-9ce2-3d5d3c982e77.png)

  - 정적 팩터리의 메서드 참조를 공급자(Supplier)로 사용할 수 있다는 점
    - Elvis::getInstance를 Supplier<Elvis>로 사용하는 식(Item 43, 44)

3. Enum 타입

```java
public enum Elvis{
  INSTANCE;
  
  public void leaveTheBuilding() { ... }
}
```

- public 필드 방식과 비슷하지만, 더 간결하고, 추가 노력없이 직렬화할 수 있다. 아주 복잡한 직렬화 상황이나 리플렉션 공격에서도 제2의 인스턴스가 생기는 일을 완벽히 막아준다.
  * 대부분에 상황에서는 원소가 하나뿐인 열거 타입이 싱글턴을 만드는 가장 좋은 방법
  * 만드려는 싱글턴이 Enum 외의 클래스를 상속해야 한다면 이 방법은 사용할 수 없다.
  * 직렬화/역직렬화 시 추가 노력이 필요없는 건 Enum의 요소들이 내부 구현 시 public static final로 구현되어 있기 때문이다.(참고 - [enum in Java](https://www.geeksforgeeks.org/enum-in-java/))
  
### 싱글턴 클래스 직렬화
- 위의 첫번째나 두번째 방식으로 만든 싱글턴 클래스를 직렬화하려면 단순히 Serializable을 구현한다고 선언하는 것만으로는 부족하다.
  - 이유: 직렬화된 인스턴스를 역직렬화할 때마다 새로운 인스턴스가 만들어진다.
  - 해결책: readResolve 메서드를 아래와 같이 재정의해서 원래 Instance를 return하고, 역직렬화하면서 새롭게 만들어진 객체는 gc에게 맡긴다. 이 때, Singleton INSTANCE 외에 나머지는 transient라고 선언해야 한다.
  (Item 89)
  ```java
  private Object readResolve() {
    // '진짜' Elvis를 반환하고, 가짜 Elvis는 가비지 컬렉터에 맡긴다.
    return INSTANCE; 
  }
  ```
  - 참고: [자바 직렬화: readResolve와 writeReplace](https://madplay.github.io/post/what-is-readresolve-method-and-writereplace-method)


### 참고자료
- [자바 직렬화, 그것이 알고싶다. 훑어보기편](https://woowabros.github.io/experience/2017/10/17/java-serialize.html)























