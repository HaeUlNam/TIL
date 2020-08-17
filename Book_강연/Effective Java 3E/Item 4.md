## 인스턴스화를 막으려거든 private 생성자를 사용하라

- 정적 메서드와 정적 필드만을 담은 클래스가 필요한 경우가 있다. 물론 이러한 것을 객체지향적 사고를 하지 않고 남용하면 안되지만, 유틸리티 클래스 등에는 유용하게 쓰인다.
- 예를 들어, java.lang.Math/java.util.Arrays/java.util.Collections
  * final 클래스와 관련한 메서드들을 모아놓을 때도 사용한다. final 클래스를 상속해서 하위 클래스에 메서드를 넣는 것은 불가능하기 때문이다(why?)
- 정적 멤버만 담은 유틸리티 클래스는 인스턴스로 만들어 쓰려고 설계한 것이 아니다. 따라서 유틸리티 클래스의 생성자를 private하게 두는 것이 가장 적절하다.
  * 실제로 공개된 API들에서도 이처럼 의도치 않게 인스턴스화할 수 있게 된 클래스가 종종 목격된다.
```java
public class UtilityClass{
  //기본 생성자가 만들어지는 것을 막는다(인스턴스화 방지용)
  private UtilityClass(){
    //일어나서는 안되는 경우 AssertionError Throw
    throw new AssertionError();
  }
}
```
- 생성자가 존재하는데 호출할 수 없도록 하는 것은 직관적이지 않다. 따라서 위처럼 적절한 주석을 달아두는 것이 좋을 것 같다.
- 이렇게 하면 상속을 방지하는 효과도 있다.
  * 모든 생성자는 명시적이든 묵시적이든 상위 클래스의 생성자를 호출하게 되는데, 이를 private으로 선언했으니 하위 클래스가 상위 클래스의 생성자에 접근할 길이 막혀버린다.

### 참고자료
- [What is an AssertionError? In which case should I throw it from my own code?](https://stackoverflow.com/questions/24863185/what-is-an-assertionerror-in-which-case-should-i-throw-it-from-my-own-code/24863229)
