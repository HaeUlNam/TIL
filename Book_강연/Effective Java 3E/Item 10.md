# 3장 모든 객체의 공통 메서드
- Object에서 final이 아닌 메서드는 모두 재정의(overrriding)를 염두에 두고 설계된 것이라 재정의 시 지켜야 하는 일반 규약이 명확히 정의되어 있다.
- 모든 클래스는 이 메서드들을 일반 규약에 맞게 재정의해야 한다. 메서드를 잘못 구현하면 대상 클래스가 이 규약을 준수한다고 가정하는 클래스(HashMap과 HashSet 등)를 오동작하게 만들 수 있다.

# equals 일반 규약을 지켜 재정의하라

## 재정의하지 않는 것이 최선인 경우
- 각 인스턴스가 본질적으로 고유하다
  * 값을 표현하는 게 아니라 동작하는 객체를 표현하는 클래스가 여기 해당.
  * ex) Thread
- 인스턴스의 '논리적 동치성'을 검사할 일이 없다
- 상위 클래스에서 재정의한 equals가 하위 클래스에도 딱 들어맞는다.
  * Set 구현체는 AbstractSet이 구현한 equals, List -> AbstractList로부터, Map 구현체들은 AbstractMap으로부터 상속받아 사용
  ```java
  //AbstractSet의 equals
  public boolean equals(Object o) {
      if (o == this)
          return true;

      if (!(o instanceof Set))
          return false;
      Collection<?> c = (Collection<?>) o;
      if (c.size() != size())
          return false;
      try {
          return containsAll(c);
      } catch (ClassCastException unused)   {
          return false;
      } catch (NullPointerException unused) {
          return false;
      }
  }
  ```
- 클래스가 private이거나 package-private이고 equals 메서드를 호출할 일이 없다.

## equals를 호출하지 못하도록 강제하는 경우
```java
@Override public boolean equals(Object o){
  throws new AssertionError(); //호출 금지
}
```

## equals를 재정의해야 할 때는 언제일까?
- 객체 식별성이 아니라 논리적 동치성을 확인해야 하는데, 상위 클래스의 equals가 논리적 동치성을 비교하도록 재정의되지 않았을 때다.
  * 보통 Integer와 String과 같은 값 클래스가 여기에 해당한다.
  * 이렇게 하면 Map의 키와 Set의 원소로 사용할 수 있다. 
  * 값 클래스라고 해도 값이 같은 인스턴스가 둘 이상 만들어지지 않음을 보장하는 인스턴스 통제 클래스라면 equals를 재정의하지 않아도 된다. ex) Enum의 경우 논리적 동치성 = 객체 식별성

## equals 메서드를 재정의할 때의 일반 규약
### 반사성: null이 아닌 모든 참조 값 x에 대해, x.equals(x)는 true이다.
### 대칭성: null이 아닌 모든 참조 값 x, y에 대해, x.equals(y)가 true면 y.equals(x)도 true다.
  * 아래의 예제는 대칭성을 지키지 못했다. CaseInsensitiveString/String 순서로는 비교가 되는데, String/CaseInsensitiveString 순서로는 비교가 불가능. (String 재정의가 안되니깐)
  ```java
  public final class CaseInsensitiveString {
    private final String s;

    public CaseInsensitiveString(String s){
      this.s = Objects.requireNonNull(s);
    }

    @Override public boolean equals(Object o){
      if (o instanceof CaseInsensitiveString)
        return s.equalsIgnoreCase(
            (CaseInsensitiveString)o).s);
      if (o instanceof String) //한 방향으로만 작동한다!
        return s.equalsIgnoreCase((String) o);
    }
  } 
  ```
  * 해결책은 재정의가 안되기에 애초에 String과 CaseInsensitiveString를 비교하지 않는 것이다
  ```java
  @Override public boolean equals(Object o){
    return o instanceof CaseInsensitiveString &&
       ((CaseInsensitiveString) o).s.equalsIgnoreCase(s);
  }
  ```
### 추이성: 1과 2가 같고, 2와 3이 같으면, 1과 3도 같아야 한다는 것

```java
public class Point { 
  private final int x; 
  private final int y;

  public Point(int x, int y) { 
    this.x = x;
    this.y = y; 
  }
  @Override public boolean equals(Object o) { 
    if (!(o instanceof Point))
      return false;
    Point p = (Point)o;
    return p.x == x && p.y == y;
}
... // 나머지 코드는 생략 }
```
```java
public class ColorPoint extends Point { 
  private final Color color;
  public ColorPoint(int x, int y, Color color) { 
    super(x, y);
    this.color = color; 
  }
... // 나머지 코드는 생략 }
```

- 위와 같이 두 클래스가 존재할 때 ColorPoint의 equals를 아래와 같이 짜면 어떨까?
```java
@Override public boolean equals(Object o) { 
  if (!(o instanceof ColorPoint))
    return false;
  return super.equals(o) && ((ColorPoint) o).color == color;
}
```
```java
Point p = new Point(1,2);
ColorPoint cp = new ColorPoint(1, 2, Color.RED);
```
- 위에 대해 p.equals(cp)는 true, cp.equals(p)는 false를 반환한다.
  * 따라서 대칭성을 만족하지 못한다. (Point는 Color를 무시하고 비교하기에 true가 나온다)
  * 이런 경우 대칭성을 만족시키기 위해 Point와 ColorPoint 비교 시 색을 무시하면 어떻게 되나?

```java
@Override public boolean equals(Object o) { 
  if (!(o instanceof ColorPoint))
    return false;
  if (!(o instanceof ColorPoint))
    return o.equals(this);
  return super.equals(o) && ((ColorPoint) o).color == color;
}
```
```java
ColorPoint p1 = new ColorPoint(1, 2, Color.RED); //A
Point p2 = new Point(1, 2); //B
ColorPoint p3 = new ColorPoint(1, 2, Color.BLUE); //C
```

- 대칭성은 만족시키지만 추이성을 만족시키지 못한다.
  * A == B, B == C, A != C이기 때문에 추이성을 만족하지 못한다.
  * 무한 재귀의 위험성: Point의 또 다른 하위 클래스로 SmellPoint를 만들고, 같은 방식으로 equals 구현 후 myColorPoint.equals(mySmellPoint)를 호출하면 StackOverflowError가 발생한다

- 해결책: 구체 클래스를 확장해 새로운 값을 추가하면서 equals 규약을 만족시킬 방법은 존재하지 않는다.



- 일관성
- null-아님



  
