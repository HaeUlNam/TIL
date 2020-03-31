### Activity와 View의 관계

- Activity는 4대 Component 중 유일하게 화면에 관여하는 컴포넌트이고, 직접 화면을 그리는 것은 아니다.
- Activity 안에 View Class를 상속받은 TextView, Button 등의 화면 구성 요소들이 View LifeCycle에 따라 화면에 그려지게 된다.

### View가 그려지는 과정

- View는 포커스를 얻으면 Layout을 그리도록 요청한다. 이 때 부모 View부터 그려지게 되며, 하위 View들은 전위 순회 순서로 그려지게 된다.
- 아래는 각 View에서 그려지는 순서를 나타낸 것이다.
1) onMeasure: View의 크기를 알아낸다.
2) onLayout: View와 자식뷰들의 크기와 위치를 할당
3) onDraw: 뷰를 실제로 그리는 단계. Canvas를 이용해 뷰의 모양을 그리고, Paint를 이용해 뷰의 색을 그립니다.

### View Architecture

- View의 기본 구조는 뷰 객체 간의 계층으로 이루어져 있습니다. 소프트웨어 모델로 이야기하면 [DOM](https://jokergt.tistory.com/62)을 따르고 있고, 패턴(Pattern)으로 이야기하면 [Composite 패턴](https://github.com/HaeUlNam/TIL/blob/master/DesignPattern/CompositePattern.md)이 적용된 구조입니다.

![image](https://user-images.githubusercontent.com/26040955/77984585-ec74ae80-734c-11ea-8175-126c60836e2f.png)

- ViewGroup이 Composite 패턴에서 Composite이고, View가 Component입니다.
  - ViewGroup의 구체적 예시로 ConstraintLayout, RelativeLayout 등이 있습니다.
  - Button, TextView 등은 View Class를 상속받아 사용합니다.

- 출처
  * [현우의 개발노트](https://hyeonu1258.github.io/2018/03/26/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%20%EB%A9%B4%EC%A0%91/)
  * https://jungwoon.github.io/android/2019/10/02/How-to-draw-View/
  * 깡샘의 안드로이드 프로그래밍
  * https://gmlwjd9405.github.io/2018/08/10/composite-pattern.html
