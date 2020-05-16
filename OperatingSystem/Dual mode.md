## User mode 와 Kernel mode란?
- User mode: 유저가 접근할 수 있는 영역을 제한적으로 두고, 프로그램의 자원에 함부로 침범하지 못하도록 한다.
- Kernel mode: 시스템 안의 모든 자원에 접근 가능

### User mode와 Kernel mode 예시

![image](https://user-images.githubusercontent.com/26040955/82113263-b3bf5600-978f-11ea-8720-3076c6ce965b.png)

1) User mode에서 실행되고 있는 Process가 system call 호출
2) mode bit = 0으로 바꾸고, Kernel mode로 전환해서 system call 처리
3) mode bit = 1로 바꾸고, User mode로 전환해서 나머지 Process 실행

- 최초 부팅 시 하드웨어는 커널 모드에서 시작. OS가 올라오는 순간부터 User mode 시작
- 필요성: 시스템을 보호하기 위해서 Dual mode를 사용하게 된다.
  * 다른 사용자의 입출력을 방해하는 경우가 생길 수 있다.
  * 다른 사용자의 메모리나 운영체제 영역 메모리에 접근할 수 있다.
  * CPU 보호

### System Call
- 커널 시스템의 유일한 진입점으로서 자원이 필요한 모든 프로그램은 System call을 사용해야 한다.
