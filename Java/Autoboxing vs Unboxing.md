### Primitive Data & Wrapper Class
- Primitive : boolean, char, byte, short ...
  * stack 메모리 영역에 존재
- Wrapper: Integer, Character, Byte, Short...
  * Heap 메모리 영역에 존재하고, 이를 포인팅하는 래퍼런스 변수만 스택 메모리에 존재.

### Autoboxing, Unboxing
- 아래처럼 Primitive와 Wrapper를 자동으로 변환해주는 것.
- 장점: 개발자는 이를 통해 이해가 빠른 코드 작성이 가능해진다.

![스크린샷 2020-05-10 오후 8 53 38](https://user-images.githubusercontent.com/26040955/81498500-53986200-9300-11ea-8083-0b5124415c0d.png)


### Autoboxing
- compiler가 primitive data -> Wrapper object로 변환

![스크린샷 2020-05-10 오후 8 55 27](https://user-images.githubusercontent.com/26040955/81498562-95c1a380-9300-11ea-8353-e733ba06fd67.png)

```java

int a = 2017;
Integer b = a; //Autoboxing;
Integer b = new Integer(a); //Autoboxing을 지원해주기 전에는 이런 식으로 변환

```

### Unboxing
- compiler가 Wrapper object -> primitive data로 변환

![스크린샷 2020-05-10 오후 8 58 04](https://user-images.githubusercontent.com/26040955/81498621-f355f000-9300-11ea-8f57-fed8c501b45f.png)


```java

Integer a = new Integer(2017);

int b = a.intValue(); //Unboxing 지원 이전
int b = a; //Unboxing(Compiler가 위 작업을 내부적으로 진행)

```
