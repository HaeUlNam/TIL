### Formal-parameter && Actual-parameter

- Actual-parameter: 실제 전달 값을 가진 변수
- Formal-parameter: 선언된 function의 parameter 변수

### Call-by-value vs Call-by-reference
- Call-by-value: actual-parameter를 대응하는 함수의 변수로 복사하며, 복사된 값은 함수내에서 지역적으로 사용되는 local value라는 특징을 가지고 있습니다. 
caller는 인자값을 복사 방식으로 넘겨주었으므로 callee내에서 어떤 작업을 하더라도 caller는 영향을 받지 않습니다.

![스크린샷 2020-05-03 오후 10 56 49](https://user-images.githubusercontent.com/26040955/80916069-61466880-8d91-11ea-8cc8-b807c68feb97.png)


- Call-by-reference: 사용될 변수의 묵시적인 레퍼런스를 함수로 전달하며, 그것이 변수의 값은 아니다라고 되어있습니다. call-by-reference로 swap함수에
뭔가를 전달한다면 x와 y가 가지고 있는 값(10, 20)이 아닌 x,y 변수 자체에 대한 레퍼런스를 전달해야 합니다.

![스크린샷 2020-05-03 오후 11 09 36](https://user-images.githubusercontent.com/26040955/80916367-2a715200-8d93-11ea-8f70-1818e8963403.png)

- 예시
  * 아래의 경우 (1)은 call-by-value, (2)은 call-by-reference, (3)은 call-by-value이다.
  * (3)의 경우 c가 reference를 넘겨준 것이 아니라 자신이 저장하고 있는 값을 넘겨준 것이기에 call-by-value이다.

```c

void modify(int p, int* q, int* r){
  p = 27; //(1)
  *q = 27; //(2)
  *r = 27; //(3)
}

int main(int argc, char** argv) {
    int a = 1;
    int b = 1;
    int x = 1;
    int* c = &x;
    modify(a, &b, c);   // a is passed by value, b is passed by reference by creating a pointer,
                        // c is a pointer passed by value
    return 0;
}
```

### Java가 call-by-value인 이유

1) 자바에서는 c, c++의 &과 같이 객체의 주소를 가져오는 방법이 없다.
2) 아래의 예제를 보면, 속성을 바꾸는 것 말고 새로운 객체로 변경할 때는 바뀌지 않는다. 이것은 Java에서 object는 reference '값'을 가지고 있고 
함수 인자로 이 '값'을 전달하기 때문이다.
  - 첫번째 예제는 assignNewPerson함수에 Person p 변수는 "Bob"을 가진 reference '값'으로 변경되게 된다.
  - 두번째 예제는 changePersonName함수에 Person p 변수는 이전에 전달된 reference '값'을 가지고 있고, 해당 속성을 변경하기 때문이다.
  - 추가적으로 각 함수에 Formal-parameter들은 stack에 저장된다.

![스크린샷 2020-05-03 오후 11 44 15](https://user-images.githubusercontent.com/26040955/80917135-019f8b80-8d98-11ea-846c-b4f09ae4adfe.png)



### 참고
- [Java 인자 전달 방식: Call-by-{Value | Reference}?](http://mussebio.blogspot.com/2012/05/java-call-by-valuereference.html)
- [Java Heap Space vs Stack – Memory Allocation in Java](https://www.journaldev.com/4098/java-heap-space-vs-stack-memory)
- [자바 메모리 모델](https://parkcheolu.tistory.com/14?category=654619)
