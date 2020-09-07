## 불필요한 객체 생성을 피해라

- 똑같은 기능의 객체를 매번 생성하기보다는 객체 하나를 재사용하는 편이 나을 때가 많다. 재사용은 빠르고 세련된다. 특히 불변 객체는 언제든 재사용할 수 있다. (재사용 시 불변인지 확인할 것 Item 17)
- 다음과 같이 생성자 대신 정적 팩터리 메서드를 제공하는 불변 클래스에서는 정적 팩터리 메서드를 사용해 불필요한 객체 생성을 피할 수 있다.
```java
Boolean(String)
Boolean.valueOf(String) //권장
```

- Boolean.valueOf는 어떤 역할을 하나 궁금해서 찾아보니 String이 true이고, null이 아니면 true를 반환한다.
  * equalsIgnoreCase: https://library1008.tistory.com/37
```java
public static Boolean valueOf(String s) {
    return parseBoolean(s) ? TRUE : FALSE;
}

public static boolean parseBoolean(String s) {
    return ((s != null) && s.equalsIgnoreCase("true"));
}
```

### 정규표현식 같은 비싼 객체는 특히 캐싱하여 재사용

- 다음 예제는 주어진 문자열이 유효한 로마 숫자인지를 확인하는 메서드이다.
  * TODO) 정규표현식 문법
```java
static boolean isRomanNumeral(String s) { 
    return s.matches("^(?=.)M*(C[MD]|D?C{0,3})"
            + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
}
```

- String.matches는 정규표현식으로 문자열 형태를 확인하는 가장 쉬운 방법이지만, 성능이 중요한 상황에서 반복해 사용하기엔 적합하기 않다.
  * 위와 같이 사용하면 한번 쓰고 버려져서 GC에 대상이 된다.
  * Pattern 인스턴스는 입력받은 정규표현식에 해당하는 유한 상태 머신(Finite State Machine)을 만들기 때문에 인스턴스 생성 비용이 높다.
  * 참고: [FSM](https://www.joinc.co.kr/w/man/12/statemachine)
  
- 해결책: 재사용
  * 속도 향상: 책에서는 길이 8 문자열에 대해 실험했을 때, 1.1(μs) -> 0.17(μs)이다. 6.5배 상승
  * 코드 가독성: 정규표현식 Pattern에 이름을 지어주어 코드가 더 명확해졌다
```java
public class RomanNumerals {
    private static final Pattern ROMAN = Pattern.compile(
            "^(?=.)M*(C[MD]|D?C{0,3})"
            + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
    static boolean isRomanNumeral(String s) {
        return ROMAN.matcher(s).matches(); 
    }
}
```

### Lazy Initialization
- 위의 ROMAN 필드가 쓰이지 않을 경우, 지연 초기화(Lazy Initialization)로 불필요한 초기화를 없앨 수는 있지만, 권하지는 않는다. 지연 초기화는 코드를 복잡하게 만드는데, 성능을 크게 개선되지 않을 때가 많기 때문이다.
  * TODO) Item 67
  
### 재사용 예시 - Adapter
- 어댑터는 실제 작업은 뒷단 객체에 위임하고, 자신은 제 2의 인터페이스 역할을 해주는 객체. 어댑터는 뒷단 객체만 관리하면 된다. 즉, 뒷단 객체 외에는 관리할 상대가 없으므로 뒷단 객체 하나당 어댑터 하나씩만 만들어지면 충분하다. 

### 재사용 예시 - Map의 keySet 메서드
- keySet 메서드는 아래처럼 Map 객체 안에 key들을 전부 담은 Set을 반환한다.
```java
Map<String, String> a = new HashMap<>();
a.put("1","a");
a.put("2","b");
a.put("3","c");
a.put("4","d");
a.put("5","e");
a.put("6","f");
Set<String> set = a.keySet();

set.forEach(System.out::println);
//출력: 1 2 3 4 5 6
```
- 그런데 이 때 매번 다른 Set 인스턴스를 반환한다고 생각할 수 있겠지만, 사실은 매번 같은 인스턴스를 반환한다. 즉, 하나가 바뀌면 다 바뀐다는 뜻.
  * 그러니 조심해서 사용해야 한다.
  * 아래는 HashMap의 keySet인데, 처음에만 새로 생성하고 나머지는 캐싱해서 사용한다.
```java
public Set<K> keySet() {
    Set<K> ks = keySet;
    if (ks == null) {
        ks = new KeySet();
        keySet = ks;
    }
    return ks;
}
```

### 불필요한 객체 생성 - Auto Boxing

- 오토박싱은 기본 타입과 박싱된 기본 타입(Wrapper Class)을 섞어 쓸 때 자동으로 상호 변환해주는 기술이다.
- 사실 어떠한 것을 사용해도 상관없다고 생각할 수 있겠지만, 성능에서는 그렇지 않다.
  * [Item 61 - 박싱된 기본 타입보다는 기본 타입을 사용하라](https://github.com/HaeUlNam/TIL/blob/master/Book_%EA%B0%95%EC%97%B0/Effective%20Java%203E/Item%2061.md)

```java
private static long sum() { 
    Long sum = 0L;
    for (long i = 0; i <= Integer.MAX_VALUE; i++) 
        sum += i;
        
    return sum; 
}
```
- sum변수를 long이 아닌 Long으로 선언해서 불필요한 Long 인스턴스가 231개나 만들어진 것이다. (대략, long 타입인 i가 Long 타입인 sum에 더해질 때마다)
  * TODO) 진짜 231개인가..?
- 단순 Long을 long으로 바꾸면 6.3초 -> 0.59초가 된다. 따라서 박싱된 기본 타입보다는 기본 타입을 사용하고, 의도치 않은 오토박싱이 숨어들지 않도록 주의하자.
- 하지만 여기서 오해하면 안되는 것이 프로그램 명확성, 간결성, 기능을 위해 객체를 추가로 생성하는 것은 좋은 일이다. (요즘엔 JVM 최적화도 잘 되어 있기에..)

### 자신만의 객체 풀을 만드는 것은 지양하자.
- 아주 무거운 객체(DB Connection)가 아니면 단순히 객체 생성을 피하고자 자신만의 객체 풀을 만들지는 말자.
  * 일반적으로 자체 객체 풀은 코드를 헷갈리게 만들고 메모리 사용량을 늘리고 성능을 떨어뜨린다.
  * 요즘 JVM의 GC는 잘 최적화되어 있어 가벼운 객체용의 경우 직접 만든 객체 풀보다 훨씬 빠르다.










