## Template Method 패턴

- 전체적으로 동일하면서 부분적으로 다른 구문으로 구성된 메서드의 코드 중복을 최소화할 때 유용


### Template Method 다이어그램
- AbstractClass: 템플릿 메서드를 정의하는 클래스. 하위 클래스에 공통 알고리즘을 정의하고 하위 클래스에서 구현될 기능을 primitive메서드 또는 hook
메서드로 정의하는 클래스.
- ConcreteClass: 물려받은 primitive나 hook 메서드를 오버라이드해서 구현
![스크린샷 2020-05-26 오전 12 10 20](https://user-images.githubusercontent.com/26040955/82824977-4c1eae80-9ee5-11ea-97ec-e9cea9dad845.png)

### 예시

- 엘레베이터 제어 시스템에서 모터를 구동시키는 기능을 생각해보자. 예를 들어 현대 모터를 이용하는 제어 시스템이라면 HyundaiMotor클래스에 move메서드를 
정의할 수 있다.
![스크린샷 2020-05-26 오전 12 17 32](https://user-images.githubusercontent.com/26040955/82825489-4d9ca680-9ee6-11ea-8277-3c39ae3c1261.png)
- 만약 이 상태에서 현대 모터가 아닌 다른 모터를 사용해야 한다고 하면 어떻게 하면 좋을까?
  * 동작방식은 동일하기에...중복되는 코드가 발생하는데, 이를 제거하기 위해 상속을 사용
  
![스크린샷 2020-05-26 오전 12 22 06](https://user-images.githubusercontent.com/26040955/82825863-f21ee880-9ee6-11ea-95bb-0d676f672aa3.png)


- 위에서 코드 중복을 더 피하려면 하나의 함수에서 중복되는 부분을 Template method로 두고, 따로 구현해야 하는 것을 구현 method로 두어서 호출하는 방식으로 
사용하면 코드의 중복을 더 많이 줄일 수 있다.
