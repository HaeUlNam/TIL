### 요구사항 변경에 대처하는 설계 원리

- 높은 응집도와 낮은 결합도를 유지할 수 있도록 설계해야 요구사항을 변경할 때 더 유연하게 대처 가능
- 응집도: 특정 목적을 위해 밀접하게 연관되어 있고, 지나치게 많은 역할을 하지 않으면 응집도가 높다고 한다.
  * 응집도가 낮으면, 이해하기 힘들고 / 재사용하기 어렵고 / 유지 보수하기 어렵고 / 다른 클래스의 변화에 민감하다.
- 결합도: 소프트웨어의 한 요소가 다른 것과 얼마나 밀접하게 연관되어 있는지, 얼마나 의존적인지 나타내는 것.
  * 결합도가 높으면, 연관된 다른 클래스가 변경되면 같이 변경해야 하고 / 재사용하기 어렵다.

### Is kind of && Has a 관계

- Is kind of 관계는 포유류 <- 고양이과 <- 호랑이처럼 명확하게 종속 관계를 보일 때이다.
- 이 관계에서는 상속을 사용한다.

![image](https://user-images.githubusercontent.com/26040955/81520320-ebd52c00-937e-11ea-910e-e6000f2e1e3f.png)

- Has a 관계는 포함 관계로서 전체와 부분을 나타내는 관계이다. UML로는 aggregation or composition 관계이다.
- 아래 예시처럼 자동차가 바퀴를 가지고 있는 건 Has a 관계()이다.

![image](https://user-images.githubusercontent.com/26040955/81520419-2fc83100-937f-11ea-997f-e088a11d3b8b.png)

### OOP(Object Oriented Programming)

- 추상화: 어떤 영역에서 필요로 하는 속성이나 행동을 추출하는 작업
  * 아래 사진을 보면 벤츠와 아우디 둘의 공통되는 특징이 자동차라는 것이라서 이를 자동차라는 하나의 개념으로 표현할 수 있다.
  * 이렇게 구체적인 개념이 아니라 추상적 개념에 의존하기 때문에 더 유연한 설계가 가능하다.
![image](https://user-images.githubusercontent.com/26040955/81517078-b1ff2800-9374-11ea-9f36-987a592f3a28.png)

  * 구체적 개념에 의존하는 경우
  ```java
  switch(자동차 종류)
    case '아우디':
    case '벤츠':
    ...
  ```
  
  * 추상적 개념에 의존하는 경우
    * Car라는 추상적 개념으로 나머지 자동차 종류들을 관리할 수 있어 코드가 훨씬 깔끔해진다.

- 캡슐화: 정보 은닉을 통해 높은 응집도와 낮은 결합도를 가지게 해준다.
  * 정보 은닉: 접근 제한자(private, protected..)를 통해 필요 없는 정보는 외부에서 접근하지 못하도록 하는 것
  * 정보 은닉을 함으로서 외부에서는 내부의 내용을 알지 못해도 사용할 수 있기에, 인터페이스가 간결해지고 객체 간의 결합도가 낮아진다.
  * 아래와 같이 private으로 내부 멤버변수를 지정하고, 외부에서는 push와 같은 함수로 접근할 수 있도록 해두면 itemArray와 같은 내부 변수가 
  데이터 타입등이 변경되더라도 외부에서는 변경 없이 지속적으로 사용가능하다.
  
```java
public class ArrayStack {
  // 은닉되어 있다.(private)
  private int top;
  private int[] itemArray;
  private int stackSize;
  ...
}

public class StackClient {
  public static void main(String[] args) {
    ArrayListStack st = new ArrayListStack(10);
    st.push(20);
    System.out.println(st.peek());
  }

//출처: https://gmlwjd9405.github.io/2018/07/05/oop-features.html
```

- 일반화(상속): 두 클래스 사이에 is kind of 관계가 성립할 때 사용하는 것이다.
 * 만약 is kind of 관계가 성립하지 않는데, 상속받게 되면 불필요한 것들도 물려받게 되어 문제이다.

- 다형성: 서로 다른 클래스의 객체가 같은 함수들에 대해 서로 다르게 동작하는 것.
 * interface나 부모 클래스를 통해서 자식 클래스를 주입받았을 때, 각 자식 클래스마다 다르게 구현되었다면 다르게 동작하는 것.


### 출처
- [OOP(객체지향 프로그래밍)의 특징](https://gmlwjd9405.github.io/2018/07/05/oop-features.html)
- [결합도(Coupling), 응집도(Cohesion)](https://lazineer.tistory.com/93)
- [[Java] 07. Is Kind Of 관계, Has A 관계](https://dog-foot-story.tistory.com/34)
- [[UML] Class Diagram 클래스 다이어그램](https://onecellboy.tistory.com/343)
- [[C++] 상속 세번째, 상속의 조건 (is-a 와 has-a 그리고 포함)](https://pacs.tistory.com/entry/C-%EC%83%81%EC%86%8D-%EC%84%B8%EB%B2%88%EC%A7%B8-%EC%83%81%EC%86%8D%EC%9D%98-%EC%A1%B0%EA%B1%B4-is-a-%EC%99%80-has-a-%EA%B4%80%EA%B3%84)
