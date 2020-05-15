### 접근제한자(Access Modifier)
- 자바에서 접근제한자는 public, protected, default, private 등의 4가지로 이루어져 있다. 접근제한자는 OOP 중에 캡슐화의 정보 은닉을 위해 사용하게 된다.

### 접근제한자 종류
- public: 모든 허용
- protected: 같은 패키지(폴더)에 있는 class들과 상속 관계의 객체들만 허용
  * 즉 다른 패키지에 있더라도 protected 멤버변수가 있는 클래스를 상속받으면 사용 가능하다.
  * 동일 패키지라면 public처럼 자유롭게 접근 가능
- default: 같은 패키지에 있는 객체들만 허용
  * 동일 패키지라면 public처럼 자유롭게 접근 가능. 다른 패키지라면 절대 접근 불가
- private: 현재 class 내에서만 허용
  * 해당 class에서만 가능
  
### 종류별 접근제한자
- class: public, default
- 멤버변수, 메소드, 생성자: public, protected, default, private

### 참고자료
- [자바(Java)〃접근 제한자 private/ protected/ public / default](https://hunit.tistory.com/162)
