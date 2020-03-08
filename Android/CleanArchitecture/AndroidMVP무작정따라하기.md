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
