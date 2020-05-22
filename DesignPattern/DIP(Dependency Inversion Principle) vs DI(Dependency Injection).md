## DIP(Dependency Inversion Principle)
- 의존 관계를 맺을 때 변화하기 쉬운 것 또는 자주 변화하는 것보다는 변화하기 어려운 것. 거의 변화가 없는 것에 의존하라는 원칙
- 의존성 역전: 상위 계층이 하위 계층에 의존하는 전통적인 의존관계를 반전
  * 이를 통해 상위 계층이 하위 계층의 구현으로부터 독립되게 할 수 있다.
  * 구조적 디자인에서 하위 모듈의 변경이 상위 모듈의 변경을 요구하는 위계관계를 끊는 의미의 역전.

- DIP를 만족하려면 아래와 같이 추상적인 것인 인터페이스나 추상 클래스와 의존 관계를 맺도록 설계해야 한다.
- 이를 통해 변화에 유연한 시스템이 된다.

### DIP 예시

<img width="597" alt="스크린샷 2020-05-22 오후 4 09 51" src="https://user-images.githubusercontent.com/26040955/82641053-ad752200-9c46-11ea-948d-2ece3869465e.png">

- 위처럼 DIP를 만족하면 의존성 주입(Dependency Injection)이라는 기술로 변화를 쉽게 수용할 수 있는 코드를 작성할 수 있다.

### DI(Dependency InJection)
- 의존성 주입은 필요한 객체를 직접 생성하는 것이 아닌 외부로부터 필요한 객체를 받아서 사용하는 것.
- 이를 통해, 객체 간의 결합도를 줄이고 코드의 재활용성을 높여준다.
- 아래 예시 설명
  * Kid class 안에 연관 관계로 Toy Interface와 관계를 맺고 있다.
  * Kid class 안에 setToy 함수로 외부로부터 객체를 주입한다.
  * 따라서 Kid가 로봇에서 레고로 장난감을 바꾼다고 해도 기존의 코드 변경 없이 변경 가능하다.

```java
public class Kid{
  private Toy toy; //연관 관계(Kid -> toy)
  public void setToy(Toy toy){ //의존성 주입
    this.toy = toy;
  }
  
  public void play(){
    System.out.println(toy.toString());
  }
}
```

```java
public class Robot implements Toy{
  public String toString(){
    return "Robot";
  }
}
```

```java
public class Main{
  public static void main(String[] args){
    Toy t = new Robot(); //new Lego()로 변경
    Kid k = new Kid();
    k.set(t);
    k.play();
  }
}

```

### DI 추가 예제 

- 아래와 같이 Programmer 안에 Coffee가 있어서 내부에서 생성하면 매번 바뀔 때마다 직접 바꾸어줘야 한다.
- 따라서 생성자나 setter함수로 객체를 주입하도록 해서 의존성을 낮추면 기존의 코드를 바꾸지 않아도 되는 OCP를 만족하게 된다.

```java
class Coffee {...}

class Cappuccino extends Coffee {...}
class Americano extends Coffee {...}

class Programmer {
    private Coffee coffee;

    public Programmer() {
    	  this.coffee = new Cappuccino();// 직접 수정 필요
    }
    
    ...
}
```



### 참고자료
- [[DI] Dependency Injection이란 무엇일까?](https://velog.io/@wlsdud2194/what-is-di)
- [[UML] 클래스 다이어그램 작성법](https://gmlwjd9405.github.io/2018/07/04/class-diagram.html)
- [Dependency Inversion Principle](https://medium.com/@lightsoo/dependency-inversion-principle-52a7bb6dd6be)
- [[DI] Dependency Injection이란 무엇일까?](https://velog.io/@wlsdud2194/what-is-di)
