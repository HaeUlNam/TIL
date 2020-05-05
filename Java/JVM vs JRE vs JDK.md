### JVM vs JRE vs JDK

- JVM(Java Virtual Machine): Javac로 컴파일된 byte 코드를 실행하는 실행자의 역할
- JRE(Java Runtime Environment)
  * JRE는 3가지(Class Loader, Bytecode Verifier, JVM)로 이루어져 있는데, 자바 프로그램을 실행될 수 있는 환경을 의미.
  * Class Loader: 컴파일된 Class 파일을 메모리에 Loading 시켜줌.
  * ByteCode Verifier: 로딩된 Class 파일의 정보가 플랫폼에서 실행되는데 문제가 있는지 없는지 확인.
  * JVM: 최종적으로 플랫폼에서 실행.

<img width="265" alt="스크린샷 2020-05-05 오후 1 48 40" src="https://user-images.githubusercontent.com/26040955/81035711-22222f80-8ed7-11ea-9852-8aeb525b3d7c.png">

- JDK(Java Development Kit)
  * JRE가 컴파일된 바이트코드(class파일)을 실행하는 환경을 제공하는 반면, 프로그램 개발을 위해 그 이상의 것을 제공한다. 개발에 필요한 툴셋을 제공.
  * Javac: class파일을 생성하는 compiler
  * Debugger
  * JDK에는 jar명령어가 있어 이를 만들거나 실행할 수 있다. ex) java -jar foo.jar
  * jar는 라이브러리 등을 배포하기 위한 포맷으로서 class파일이나 class가 사용하는 리소스(텍스트, 그림) 및 메타데이터들을 하나로 모아두었다
  
### 참고
- 호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25
