### Singleton에서 Double Cheching Lock을 쓰면 안되는 이유
- 결론부터 이야기하면 JVM의 최적화 기법인 reodering 때문에 그렇다. DCL을 쓰고 싶으면 instance 변수에 volatile 키워드를 붙이면 될 거 같다...

- 아래 참고자료를 보고 알게 되었는데, JVM은 최적화 기법을 통해 다음과 같이 reoder를 할 수 있다. (생성자에서 exception이 발생하지 않는다는 보장이 있다면..)
  * 저렇게 바꿔주는 것이 왜 효율적인가?
  * 그 이유는 메모리를 할당하면 해당 주소를 어딘가 저장해두었다가 instance 변수에 대입해야 하는데, 이를 연속적으로 하게 되면 바로 대입할 수 있기에 최적화가 가능하다.

![스크린샷 2020-05-15 오전 12 14 44](https://user-images.githubusercontent.com/26040955/81952162-1524df00-9641-11ea-89a4-7ebd647314fa.png)

- 따라서 위와 같이 reordering이 일어나면 Thread A와 Thread B에 대해 다음과 같은 상황이 가능하다.
  * Thread A가 instance 변수에 메모리를 대입하자마자 Thread B가 getInstance함수를 시작해서 null 체크를 하면 instance 변수가 이미 할당되어서 null 아니라고 될 것이다. 
  * 그렇게 되면 Thread B는 바로 객체를 사용하게 되는데, 이 때 Thread A에서 생성자가 호출되기 전이기에 제대로 초기화되지 않은 객체를 사용하게 되는 위험성이 존재한다. 
![image](https://user-images.githubusercontent.com/26040955/81952766-d7748600-9641-11ea-9ecd-233a7df994dd.png)

### 참고자료

- [Double-Checked Locking Pattern을 쓰지 말아야 하는 이유2](https://blog.naver.com/jjoommnn/130036640859)
