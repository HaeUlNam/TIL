## 객체지향 5대 원칙 - SOLID

### SRP(Single Responsibility Principle/ 단일 책임 원칙)
- 모든 클래스는 하나의 책임만 가지며, 클래스는 그 책임을 완전히 캡슐화해야 함을 일컫는 원칙
- 예시
  * 특정 데이터를 분석하고 서버에 전송하는 모듈이 있다고 가정할 때, 이 모듈은 두 가지 이유로 수정될 수 있다.
  * 첫번째, 데이터를 분석하는 알고리즘
  * 두번째, 서버에 전송하는 형식
  * 단일 책임 원칙에 따르면 이 모듈은 두 가지 책임을 가지고 있는 것이기에 해당 모듈을 둘로 나누어야 한다. 다른 시기에 다른 이유로 변경되어야 하는 두 가지를 묶는 것은 나쁜 설계일 수 있다.

### OCP(Open-Close Principle/ 개방 폐쇄의 원칙)
- 확장에 열려있고, 변경에는 닫혀있어야 한다는 원칙. 변경이 발생할 때, 기존 구성 요소는 수정이 일어나지 말아야 하며, 쉽게 확장해서 재사용할 수 있어야 한다는 뜻입니다.
- OCP는 객체지향 프로그래밍의 핵심 원칙이라고 할 수 있습니다. 이 원칙을 무시하고 프로그래밍한다면 OOP의 가장 큰 장점인 유연성, 재사용성, 유지 보수성 등을 결코 얻을 수 없을 것입니다.

- 예시1: 성적표나 출석부에 학생의 성적이나 출석 기록을 출력하는 기능

![스크린샷 2020-05-13 오전 11 43 52](https://user-images.githubusercontent.com/26040955/81765532-063e0f80-950f-11ea-8aff-0ecaf8116fbe.png)

- 위 상태로 설계되어있을 때 학생의 대여 기록을 출력하는 기능을 추가하게 되면, 대여 기록 SomeClient class를 수정하게 되는 일이 벌어지기에 OCP를 위반하게 된다. 따라서 아래와 같이 SomeClient와 성적표, 도서관 대여 명부, 출석부 사이에 Interface를 두어 SomeClient와 Interface가 관계를 맺게 하면 확장에 열려있고, 변경에 닫힌 OCP를 만족하게 된다.

![스크린샷 2020-05-13 오후 12 09 25](https://user-images.githubusercontent.com/26040955/81767118-97fb4c00-9512-11ea-8b3d-aaaccfe5340e.png)

- 예시2: 단위 테스트를 진행할 때
  * 테스트 대상이 되는 기능이 네트워크를 통해 웹 서비스를 사용한다고 하자. 이런 경우 DB나 웹 서버를 설치해야 테스트할 수 있다. 이러한 것은 빠른 시간의 테스트, 실제 서비스 테스트의 위험도를 수반하기에 가짜 객체를 만들어 테스트의 효율성을 높일 필요가 있다.
  * [DroidKnight2019_AndroidTDD](https://github.com/HaeUlNam/TIL/blob/master/Android/TDD/DroidKnight2019_AndroidTDD/DroidKnight2019_AndroidTDD.md) 강의는 이러한 예시에 적합한 강의인듯하다. 한번 들어보고, 정확히 어떻게 가짜 객체를 만들어서 테스트 했는지 보자.
 

### LSP(Liskov Substitution Principle)
- 서브 타입은 언제나 기반 타입으로 교체할 수 있어야 한다는 원칙. 이 말은 부모 클래스와 자식 클래스 사이의 행위가 일관성이 있어야 한다는 의미이다.
- 따라서 LSP를 만족하려면 부모 클래스의 인스턴스를 자식 클래스의 인스턴스로 대신할 수 있어야 한다.
- extend나 implements 모두 궁극적으로는 다형성을 통한 확장성 획득을 목표로 합니다. 다형성과 확작성을 극대화하려면 하위 클래스를 사용하는 것보다 상위의 클래스를 사용하는 것이 더 좋습니다. 

- 다형성으로 인한 확장 효과를 얻기 위해서는 서브 클래스가 기반 클래스와 클라이언트 간의 규약을 어겨서는 안됩니다. 결국 이 구조는 다형성을 통한 확장의 원리인 OCP를 제공하게 됩니다. 따라서 LSP는 OCP를 구성하는 구조가 됩니다. 즉 LSP는 규약을 준수하는 상속구조를 제공합니다. LSP를 바탕으로 OCP는 확장하는 부분에 다형성을 제공해 변화에 열려있는 프로그램을 만들 수 있도록 합니다.


- 예시: Collection Framework
  * 아래 코드가 List만 사용할 것이라면 상관없지만, 다른 HashSet과 같은 collection으로 교체하려고 하면 수정을 많이해야한다.
 ```java
void f(){  
    LinkedList list = new LinkedList();
    // …
    modify(list);
}

void modify(LinkedList list){  
    list.add(…);
    doSomethingWith(list);
}
```

   * 아래처럼 Collection을 통해 LSP와 OCP를 모두 만족시킬 수 있다. 우선 Collection이 LSP를 만족하지 않았다면, 모든 collection framework에 대해 
범용 작업(모든 collection은 add연산이 가능)을 수행할 수 없었을 것이다. 이를 통해 modify는 변화에 닫혀있으면서, 컬렉션의 변경과 확장에 열려있는 OCP가 됩니다.

```java
void f(){  
     Collection collection = new HashSet();
     //…
     modify(list);
}

Void modify(Collection collection){  
     collection.add(…);
     doSomethingWith(collection);
}
```


### ISP(Interface Segregation Principle/ 인터페이스 분리 원칙)
- 어떠한 클래스가 자신이 이용하지 않는 메서드에 의존하지 않아야 한다는 원칙이다. 큰 덩어리의 인터페이스들을 구체적이고 작은 단위들로 분리함으로써 클래스들이 꼭 필요한 메서드들만 이용할 수 있게 한다. ISP를 통해 시스템의 내부 의존성을 약화해 리팩토링, 수정, 재배포를 쉽게 할 수 있다.

- 예시1: 독수리과 펭귄을 클래스로 표현하는 예제
  * 아래와 같이 독수리를 만들었을 때, 펭귄 class를 만든다고 하면 아래의 Bird를 그대로 상속받게 되면 fly()를 사용하지 않기에 ISP 위반이다.
```java
public abstract class Bird{
  abstract void fly();
  abstract void cry();
}

public class Eagle extends Bird{
 @Override
 public void fly() {....}

 @Override
 public void cry() {....}
}
```
   * 아래와 같이 fly()와 cry()를 쪼개서 fly()를 가지는 interface를 만들어서 ISP가 지켜지도록 한다.
 
```java
public abstract class Bird{
  abstract void cry();
}

public abstract class FlyableBird extends Bird implements Flyable {...}

public class Eagle extends FlyableBird{
 @Override
 public void fly() {....}

 @Override
 public void cry() {....}
}

public class Penguin extends Bird{
 @Override
 public void cry() {....}
}
```

### DIP(Dependency Inversion Principle/ 의존성 역전의 원칙)

- 구조적 디자인에서 발생하던 하위 레벨 모듈의 변경이 상위 레벨 모듈의 변경을 요구하는 위계관계를 끊는 의미의 역전. 실제 사용 관계는 바뀌지 않으며, 추상을 매개로 메세지를 주고 받음으로써 관계를 최대한 느슨하게 만드는 원칙. 
1) 상위 모듈은 하위 모듈에 의존해서는 안 된다. 상위 모듈과 하위 모듈 모두 추상화에 의존해야 한다.
2) 추상화는 세부 사항에 의존해서는 안 된다. 세부 사항이 추상화에 의존해야 한다.
- 이 원칙은 '상위와 하위 객체 모두가 동일한 추상화에 의존해야 한다.'는 객체 지향적 설계의 대원칙을 제공한다.

- 예시: 예전 핸드폰들은 각 제조사별로 충전기가 달라서 하나의 충전기가 기기에 강한 의존성을 가지고 있었다. 하지만 이제 아래와 같이 c-type형태로 통일되면서 안드로이드 기기는 C-type이라는 인터페이스에 의존하고, 충전기들도 c-type이라는 인터페이스 의존하게 되어 약한 의존성을 가지게 되었다.(이는 해당 기기의 전용 충전기가 아니더라도 충전이 가능해지기에 약한 의존성이라고 말할 수 있는 것. 충전기 단자를 c-type이라는 인터페이스로 추상화시켰다고 말할 수도 있겠다)
![스크린샷 2020-05-14 오전 12 16 17](https://user-images.githubusercontent.com/26040955/81831282-22c26200-9578-11ea-888e-2bed3b64e4b4.png)


### 참고자료
- [Android서적] 아키텍처를 알아야 앱 개발이 보인다
- [객체지향 개발 5대 원리: SOLID](http://www.nextree.co.kr/p6960/)
- Java 객체지향 디자인 패턴
