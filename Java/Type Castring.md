### Type Casting(형변환)
- 각 type의 크기가 다르기에 이를 변경할 때 형변환이라는 것이 필요한데, 보통 묵시적 형변환과 명시적 형변환으로 나뉘게 된다.

### 묵시적 형변환
- 직접 선언을 하지 않더라도 자연스럽게 형변환이 되는 것
- 보통 아래와 같이 크기가 작은 것이 큰 type에 대입될 때 묵시적 형변환이 가능하다.

```java
short t2 = 20; //2byte
int bb = t2; //4byte
```

### 명시적 형변환
- 직접 선언을 통해 변환할 type을 정해주는 것

```java
//굳이 명시적으로 선언하지 않더라도 대입 가능
short t2 = 20;
int bb = (int)t2;

//명시적으로 선언하지 않으면 에러 발생. 더 큰 type을 작은 type에 대입하려고 하다보니..
int bb = 10;
short t2 = bb;
```

### 자바의 기본 연산 데이터 타입

- 정수 + 정수 = int
- 정수 + 실수 = double
- 정수 or 실수 + "문자" = string
- 따라서 위처럼 연산 후에 더 작은 타입이나 원하는 타입으로 대입하려고 할 때는 명시적 형변환이 필요할듯 싶다.

- 아래와 같이 코드를 작성하면 java에서 다음과 같은 오류가 발생한다.
```java
short t1 = 10;
short t2 = 20;
short t3 = t1 + t2;
```
<img width="268" alt="스크린샷 2020-05-15 오전 11 28 19" src="https://user-images.githubusercontent.com/26040955/82004991-30bed280-969f-11ea-896b-ce5dc0e3052a.png">

- 따라서 위 코드를 아래처럼 변경해서 사용해야 한다.

```java
short t1 = 10;
short t2 = 20;
short t3 = (short)(t1 + t2);
```


### 참고자료
- [[Java] 묵시적, 명시적 형 변환](https://haebi.kr/entry/Java-%EB%AC%B5%EC%8B%9C%EC%A0%81-%EB%AA%85%EC%8B%9C%EC%A0%81-%ED%98%95-%EB%B3%80%ED%99%98)
