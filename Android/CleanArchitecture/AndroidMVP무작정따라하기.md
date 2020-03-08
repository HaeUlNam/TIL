## 출처: [권태환님의 Android MVP 무작정 따라하기](https://thdev.tech/androiddev/2016/10/12/Android-MVP-Intro/)
아래 남긴 내용들은 모두 위 출처를 공부하고 요약한 것입니다.

## Intro

### MVP 설명
- Android에서 Test code를 작성하기 위한 구조 중 하나로 MVP를 선택.
- Model, View, Presenter 간의 상호 의존성을 떨어트리기 위한 용도임과 동시에 Test code 작성을 위한 최적의 구조 중 하나이다.
<img width="600" alt="제목 없는 그림" src="https://user-images.githubusercontent.com/26040955/76162096-5f8b6a80-617d-11ea-985d-f1a38b1ce7b5.png">

- Model: Data 관련된 처리 담당
- View: 사용자의 실질적인 이벤트가 발생하고, 이를 처리 담당자인 Presenter에 전달
- Presenter: View에서 전달받은 이벤트를 처리하고, 이를 다시 View에 전달

### MVP 흐름
<img width="600" alt="제목 없는 그림" src="https://user-images.githubusercontent.com/26040955/76162137-ec362880-617d-11ea-9d2a-f90366318931.png">

- 위의 흐름대로 흘러가는데, Presenter는 이벤트의 형태에 따라 캐시 데이터를 가져오거나/Model에 요청

## MVC 구조 이해하기

### MVC 설명
<img width="600" alt="제목 없는 그림" src="https://user-images.githubusercontent.com/26040955/76162308-daee1b80-617f-11ea-804e-0c2dbfcfbe25.png">

- Model: Data를 가진다.
- View: 사용자에게 보일 화면을 표현
- Control: 사용자로부터 입력을 받고, 이를 모델에 의해 View 정의를 하게 된다.

<img width="600" alt="제목 없는 그림" src="https://user-images.githubusercontent.com/26040955/76162475-8186ec00-6181-11ea-8e60-d44ab5aa18d8.png">

하지만 안드로이드에서는 View와 Control이 Activity/Fragment와 같은 View에 모두 포함되어 있어서.. 아래 그림과 같이 나타난다.
ex) ClickListener에서 model로 요청할 때, Activity 안에서 View와 Control을 모두 수행

<img width="600" alt="제목 없는 그림" src="https://user-images.githubusercontent.com/26040955/76162526-f35f3580-6181-11ea-986b-5c710da5b288.png">

### 장점
- 개발 기간이 짧을 수 있음: Activity 안에 모든 Logic이 들어가면 되기에..
- 코드만 읽을 수 있다면 누구나 쉽게 파악 가능

-> MVC도 함수 분리 또는 Class 분리를 적절하게 잘 한다면 복잡도가 낮아질 수 있다.

### 단점
- 하나의 Class에 많은 양의 코드를 발견할 수 있다.
- 스파게티 코드 가능성: 분리가 잘 안되기에
- 유지 보수의 어려움
- View와 Model의 결합도가 높다: 대부분의 코드에서 View가 Model을 호출하여 사용하게 된다.
(TODO/ MVP에서는 안 그런가? MVP 코드 작성할 때 유심히 봐야겠다.)

4번째 단점이 명확히 이해가지 않았는데, [안드로이드 Architecture 패턴 Part 1: 모델 뷰 컨트롤러](https://medium.com/nspoons/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-architecture-%ED%8C%A8%ED%84%B4-part-1-%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC-model-view-controller-881c6fda24d9)
여기에서 맨 아래에 '누가 UI로직을 다룰 것인가?'부분을 읽어보면 좋을 것 같다.
