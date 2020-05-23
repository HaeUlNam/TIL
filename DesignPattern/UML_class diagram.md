## UML(Unified Modeling language)

- UML은 요구 분석, 시스템 설계, 시스템 구현 등의 시스템 개발 과정에서 개발자 사이의 의사 소통이 원활하게 이루어지도록 표준화한 통합 모델링 언어다.
- 자주 쓰이는 UML로는 클래스 다이어그램, 시퀀스 다이어그램, 유스케이스 다이어그램 등이 있다.
  * 추후에 UML에 대해서는 잘 알아야 하겠다.

## class diagram
- 시간에 따라 변하지 않는 시스템의 정적인 면을 보여주는 대표적인 UML 구조 다이어그램

### 접근 제어자
- public: +
- private: -
- protected: #
- package(default): ~

### 연관 관계(association)

- 클래스들이 개념상 연결되어있음을 나타낸다.

- 예시 1
![스크린샷 2020-05-23 오후 9 07 08](https://user-images.githubusercontent.com/26040955/82730268-6156da00-9d39-11ea-95e9-7f92f5306955.png)

```java
public class Phone{

}

public class Person{
 private Phone[] phones;
 
 public Person{
  phones = new Phone[2];
 }
}
```

- 예시 2

![스크린샷 2020-05-23 오후 9 12 35](https://user-images.githubusercontent.com/26040955/82730388-20ab9080-9d3a-11ea-9c08-6e36a7d06e97.png)


```java
public class Phone{

}

public class Person{
 private Phone homePhones;
 private Phone officePhone;
 
 //객체 생성
}


```

- 다중성 표시
  * 1 : 엄밀하게 1
  * * 나 0..* : 0 또는 그 이상
  * 0..1 : 0 또는 1
  * 1, 2, 6: 1또는 2또는 6

- 단방향 연관 관계
  * 아래 예시는 '수강하다' 연관관계를 나타낸 것으로 Student-> Course형태로 되어 있다. 이는 학생은 자신이 수강하는 과목을 알지만 과목은 자신을 수강하는 학생들의 존재를 모른다는 사실을 의미.

![스크린샷 2020-05-23 오후 9 36 29](https://user-images.githubusercontent.com/26040955/82730810-7897c680-9d3d-11ea-9180-b360c958107d.png)

```java
public class Student{
 private String name;
 private ArrayList<Course> courses;
 
 public Student(){
  courses = new ArrayList<>();
 }
 
 public registerCourse(Course course){
  courses.add(course);
 }
 
 public dropCourse(Course course){
  if(courses.contains(course))
    courses.remove(course); //equal 메소드를 통해 remove (default는 주소값 비교)
 }
}
```

- 양방향 연관관계
  * 하지만 위 예제는 한 과목에 한 명의 학생만 수강해야 한다는 이상한 관계가 되기에 일반적으로 Course에 여러 수강생이 있기에 양방향 연관관계로 이를 수정해보겠다.
  * 참고로 양방향 연관관계는 서로의 존재를 안다는 의미이다.
  * 하지만... 양방향 연관관계는 구현하기 어렵기에 보통 다대다 관계를 일대다 단방향 관계로 변환해 구현한다.

![스크린샷 2020-05-23 오후 10 02 09](https://user-images.githubusercontent.com/26040955/82731339-0de88a00-9d41-11ea-9b67-a22907756eca.png)

 * 위의 Student 클래스는 그대로이고, Course에도 List 인터페이스로 다중 관계를 표현하면 된다.

- 연관관계
  * 이 상황에서 Student와 Course에서 성적정보는 어디가 두는 것이 알맞을까? 
  * Student나 Course 둘 중 어느 곳에도 둘 수 없다. 왜냐하면 Student와 Course 모두 존재해야 의미가 있기 때문이다.
  * "홍길동 학생이 소프트웨어 공학에서 A+을 받았다"처럼...
  * 따라서 성적정보는 클래스의 속성이 아닌 '수강하다'라는 연관 관계의 속성으로 다뤄야 한다. 이런 경우 연관 클래스를 사용. 연관 클래스는 아래처럼 점선을 사용해서 연결한다.
 
  ![스크린샷 2020-05-23 오후 10 18 29](https://user-images.githubusercontent.com/26040955/82731630-55701580-9d43-11ea-983f-addd56ea4997.png)

  * 그럼 위 상황에서 연관 클래스인 Transcript는 어떻게 구현해야할까?
  * Transcript 객체는 Student 객체와 Course 객체를 연관시키는 객체이므로 Student 객체와 Course 객체를 참조할 수 있는 속성을 포함해야 한다. 또한 성적과 과목 개설년도와 같은 데이터는 Student 클래스나 Course 클래스에 속하지 않으며 두 클래스의 연관 정보이므로 이들도 Transcript 클래스의 속성이어야 한다.
 
  ![스크린샷 2020-05-23 오후 10 26 07](https://user-images.githubusercontent.com/26040955/82731835-6705ed00-9d44-11ea-877c-ca58d5807da6.png)
  
- 재귀적 연관 관계
  * 현실에서 직원인 관리자 한 명이 여러 명의 사원들을 관리한다. 그런데 이를 아래와 같이 디자인하게 되면 '홍길서' -> '홍길동', '홍길동' -> '홍길남' 관계에서 
  '홍길동'은 관리자와 직원 둘 다 해당하는 모순이 생긴다.
  
  ![스크린샷 2020-05-23 오후 10 58 27](https://user-images.githubusercontent.com/26040955/82732558-ec8b9c00-9d48-11ea-9ec0-ae004b42baa1.png)

  
  * 따라서 이를 해결하려면 재귀적 연관 관계를 맺으면 된다. 하지만 여기에도 문제점이 있는데, 아래 그림에서는 '홍길남' -> '홍길서'도 가능하기 때문에 일종의 제약을 설정해주어야 한다.
  
  ![스크린샷 2020-05-23 오후 10 59 01](https://user-images.githubusercontent.com/26040955/82732577-00370280-9d49-11ea-9d5a-68f013e57294.png)

 * 계층적 제약을 통해 위의 문제를 해결할 수 있다.
 
 ![스크린샷 2020-05-23 오후 11 01 06](https://user-images.githubusercontent.com/26040955/82732629-4a1fe880-9d49-11ea-9962-7b61a62f12c0.png)

 
### 일반화 관계(generalization)

- 일반화 관계는 상속 관계이다. 따라서 'is a kind of'의 관계가 성립해야 올바른 상속이라고 할 수 있다.
  * 세탁기는 is a kind of 가전 제품
  * TV is a kind of 가전 제품
  * 식기세척기 is a kind of 가전 제품
  <br>
  ![스크린샷 2020-05-23 오후 11 04 59](https://user-images.githubusercontent.com/26040955/82732694-d500e300-9d49-11ea-9975-474db5c76f10.png)

- 클래스에서 추상 메서드는 이탤릭체로 써서 구분하거나 스테레오 타입으로 표시한다.
  ![image](https://user-images.githubusercontent.com/26040955/82732750-28733100-9d4a-11ea-9a64-8514658cb853.png)

### 집합 관계(composition, aggregation)

- 집합 관계는 UML 연관 관계의 특별 경우로 전체와 부분의 관계를 명확하게 명시하고자 할 때 사용한다.
  * 집약 관계: 한 객체가 다른 객체를 포함하는 것을 나타낸다. '전체', '부분'과의 관계며 '전체'를 가리키는 클래스 방향에 빈 마름모로 표시한다. 전체 객체의 라이프타임과 부분 객체의 라이프타임은 독립적이다. 즉, 전체 객체가 메모리에서 사리진다 해도 부분 객체는 사라지지 않는다.
  * 합성 관계: 전체를 가리키는 클래스 방향에 채워진 마름모로 표시되며 부분 객체가 전체 객체에 속하는 관계다. 따라서 전체 객체가 사라지면 부분 객체도 사라지는 경우를 의미한다. 만약 공유할 수 있는 객체를 사용할 경우에는 합성 관계가 아닌 집약 관계를 사용한다.
  
  ![image](https://user-images.githubusercontent.com/26040955/82732990-b4d22380-9d4b-11ea-815b-70c1157a160b.png)

```java
//
public class Computer {
 private MainBoard mb;
 private CPU c;
 // 생성자
 public Computer(MainBoard mb, CPU c) {
 this.mb = mb;
 this.c = c;
 }
}

public class Computer {
 private MainBoard mb;
 private CPU c;
 // 생성자
 public Computer(MainBoard mb, CPU c) {
 this.mb = new MainBoard();
 this.c = new CPU();
 }
}


출처: https://gmlwjd9405.github.io/2018/07/04/class-diagram.html
```

- 예시1) 동아리와 학생 관계
  * 학생은 한 동아리에만 가입할 수 있다.
  * 한 동아리에는 여러 명의 학생들이 있다.
  * 동아리가 없어지면 동아리에서 활동했던 학생들의 정보도 없어진다.
  <br>
  ![스크린샷 2020-05-23 오후 11 35 05](https://user-images.githubusercontent.com/26040955/82733323-0a0f3480-9d4e-11ea-8794-f72e66e25383.png)  

### 의존 관계(dependency)

- 연관 관계와 같이 한 클래스가 다른 클래스에서 제공하는 기능을 사용할 때를 나타낸다. 차이점은 두 클래스의 관계가 한 메서드를 실행하는 동안과 같은, 매우 짧은 시간만 유지된다는 점이다. 점선 화살표를 사용해 표시한다. 

- 아래의 예시는 자동차와 주유기의 관계인데, 자동차가 항상 특정 주유기로 주유하는 것이 아니라 매번 다른 주유기를 사용하기에 아래와 같이 표현.

![스크린샷 2020-05-23 오후 11 42 38](https://user-images.githubusercontent.com/26040955/82733480-16e05800-9d4f-11ea-9a5e-08855081b2bd.png)

```java
public class Car{

  public void fillGas(GasPump p){
   p.getGas(amount);
  
  }

}
```

### 인터페이스와 실체화 관계(realization)

- 인터페이스는 책임이다. 객체가 외부에 제공하는 서비스나 기능은 객체가 수행하는 책임으로 본다.
- 일반화 관계는 is a kind of 관계지만 실체화 관계는 can do this 관계이다.

![스크린샷 2020-05-23 오후 11 47 29](https://user-images.githubusercontent.com/26040955/82733594-c4ec0200-9d4f-11ea-929e-d93a52c70a78.png)

### 참고자료
- JAVA 객체지향디자인패턴
- [List - ArrayList 사용하는 방법](https://developer-syubrofo.tistory.com/2)
- [[UML] 클래스 다이어그램 작성법](https://gmlwjd9405.github.io/2018/07/04/class-diagram.html)
