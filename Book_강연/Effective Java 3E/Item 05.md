## 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라

- 아래 두 코드는 잘못 사용한 예이다.
  * 맞춤법 검사기는 사전에 의존하는데, 아래 두 방식 모두 단 하나만 사용한다고 가정한다는 점에서 그리 훌륭한 방법은 아닌 것 같다. 왜나햐면 사전이 테스트용 사전, 다른 사전 등이 필요할 수 있는데, 단 하나의 사전에 
  의존하고 있기 때문이다.

```java
//정적 유틸리티
public class SpellChecker {
  private static final Lexicon dictionary = ...; 
  
  private SpellChecker() {} // 객체 생성 방지
  
  public static boolean isValid(String word) { ... }
  public static List<String> suggestions(String typo) { ... } 
}
```

```java
//싱글톤으로 구현
public class SpellChecker {
  private static final Lexicon dictionary = ...; 
  
  private SpellChecker() {} // 객체 생성 방지
  
  public static SpellChecker INSTANCE = new SpellChecker(...);
  
  public boolean isValid(String word) { ... }
  public List<String> suggestions(String typo) { ... } 
}
```

- SpellChecker가 여러 사전을 사용할 수 있도록 하는 가장 간단한 방법은 dictionary의 final을 빼고, setter를 추가하는 것이다. 하지만 이 방법은 어색하고 오류를 내기 쉬우며 멀티스레드 환경에서는 쓸 수 없다.
따라서 사용하는 자원에 따라 동작이 달라지는 클래스에는 정적 유틸리티 클래스나 싱글턴 방식이 적합하지 않다.

### 의존 객체 주입
- 클래스(SpellChecker)가 여러 자원 인스턴스를 지원하며, 클라이언트가 원하는 자원을 사용하도록 하려면 의존 객체 주입 방식이 좋다.
  * 인스턴스를 생성할 떄 생성자에 필요한 자원을 넘겨주는 방식
  * Objects.requireNonNull은 dictionary가 null이면 NPE이고, 아니면 그대로 진행이다. 따라서 NPE가 뜨면 안되니깐 2번째 인자에 null일 경우, 어떤 객체를 넣어준다가 존재한다.
```java
public class SpellChecker {
 private final Lexicon dictionary;
 public SpellChecker(Lexicon dictionary) {
    this.dictionary = Objects.requireNonNull(dictionary); 
 }
 public boolean isValid(String word) { ... }
 public List<String> suggestions(String typo) { ... } 
}
```
- 의존 객체 주입 방식은 불변을 보장하여 여러 클라이언트가 의존 객체들을 안심하고 공유할 수 있다.
 * 이런 주입 방식은 Builder, 정적 팩터리 메서드도 응용 가능
- 변형은 팩터리 메서드 패턴
 * Java 8 Supplier<T> 인터페이스가 팩터리를 표현한 완벽한 예
 * Supplier<T>를 입력으로 받는 메서드는 일반적으로 한정적 와일드카드 타입을 사용해 팩터리의 타입 매개변수를 제한해야 한다. 이 방식을 사용해 클라이언트는 자신이 명시한 타입의 하위 타입이라면 무엇이든 생성할 수 있는 팩터리를 넘길 수 있다.
 ```java
 //클라이언트가 제공한 팩터리가 생성한 타일(Tile)들로 구성된 모자이크(Mosaic)를 만드는 메서드이다.
 Mosaic create(Supplier<? extends Tile> tileFactory) { ... }
 ```

### DI vs Factory method pattern
- TODO) 읽기 
- https://springframework.guru/gang-of-four-design-patterns/factory-method-design-pattern/
- https://springframework.guru/gang-of-four-design-patterns/abstract-factory-design-pattern/
- DI == Factory method는 아닌 듯..?


