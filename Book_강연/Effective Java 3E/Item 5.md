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
  
  public boolean isValid(String word) { ... }
  public List<String> suggestions(String typo) { ... } 
}
```

