## final 키워드
- final은 해당 entity가 오로지 한 번 할당될 수 있음을 뜻한다. 따라서 Immutable/Read-only를 지시하는 지시어입니다.
- final 변수: 오직 한번만 초기화 가능
  * 선언 또는 생성자에서 초기화 가능.
- final 메소드: 상속되었을 때 재정의가 불가.
- final 클래스: 상속 불가

### final은 언제 사용할까?
- final 클래스: 하나의 개념에 대해 오직 하나의 인스턴스만 바라보도록 디자인하고 싶을 때 클래스에 final을 붙여서 상속이 불가능하도록 한다.
  * 이에 대한 예제는 제가 다시 쓰면... 그 의미를 해칠 것 같아 아래 캡쳐로 대체하겠습니다.
  
  <img width="969" alt="스크린샷 2020-05-15 오전 11 45 36" src="https://user-images.githubusercontent.com/26040955/82005913-9ad87700-96a1-11ea-8be1-56b48f3c01fa.png">
  * 출처: [자바의 final은 언제 사용할까?](https://blog.lulab.net/programming-java/java-final-when-should-i-use-it/)

- final 메소드: 상속되었을 때 재정의되어 사용되기를 원하지 않을 때

### final에 static을 붙이는 경우
- 모든 클래스에서 똑같은 값으로 사용해야 하기 위해, 하나의 공간에 같은 값을 쭉 할당해두고 모든 클래스에서 사용하도록 한다.


## finally 키워드
- [Exception](https://github.com/HaeUlNam/TIL/blob/master/Java/Exception.md) 참고

## finalize 키워드
- finalize는 c++에서 소멸자라고 보면 되는데, Java는 일반적으로 메모리 관리를 JVM에서 다 해주기 때문에 개발자가 명시적으로 소멸자를 정의하거나 호출할 필요가 없다.
- 이에 대해 effetive java에서는 "종료자는 사용하면 안된다. 예측이 불가능하고 대체로 위험하며 일반적으로 필요하지 않다."라고 한다.
  * JVM에서 GC가 돌아가는 원리에 대해 공부하면 위에 대해 더 명확히 알 수 있다.
  * 간단하게 말하면 C++은 unmanaged 언어이기에 메모리 관리해를 해줘야 하고, Java는 managed 언어이기에 메모리 관리를 JVM에서 하는데로 따라가야 한다.
- 참고로 finalize는 Java9에서 deprecated 되었고, cleaner이 대체되었다.

### 참고자료
- [자바의 final은 언제 사용할까?](https://blog.lulab.net/programming-java/java-final-when-should-i-use-it/)
- [왜 자바에서 final 멤버 변수는 관례적으로 static을 붙일까?](https://djkeh.github.io/articles/Why-should-final-member-variables-be-conventionally-static-in-Java-kor/)
- [자바 소멸자 finalize](https://madplay.github.io/post/java-finalize)
