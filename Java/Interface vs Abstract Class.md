### Abstract Class
- super class가 어느 정도 구현이 되어 있는 관점에서 subclass를 디자인할 경우 Abstract Class로 디자인
- super class에는 멤버변수/메소드/Abstract 메소드가 존재 가능

### Interface
- 실질적인 구현은 아무것도 없고, subclass에서 정해진 규약을 구현하도록 한다.
- 이러한 규약들이 중요한 이유는 어떤 기능을 subclass들이 가지게 될지 예측할 수 있기 때문이다.

### Marker Interface
- 어떠한 멤버변수나 메소드나 존재하지 않는 비어있는 Interface를 의미합니다.
- 사용하는 이유: compiler나 JVM에 어떤 특별한 행동을 나타내기 위해서입니다.
- 예시: Serializable, Clonnable
  * Serializable을 구현한 클래스 경우, compiler가 나중에 stream을 통해 객체 직렬화를 사용해서 통신될 수 있는 일종의 표시를 하게 된다. 실행 시에는 JVM이 객체 직렬화를 하게 된다.
  * JVM이 Clonnable을 구현한 객체만 clone 기능을 support하게 된다.

### 참고자료
- [Java관련 - 면접 질문](https://www.notion.so/Java-73d227883d4c4c388884a9421aab9730#5ca46cb215cc48ac818fbbe9daece99f)
- 호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25
