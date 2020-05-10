### new 키워드 이용 - Heap에 생성

```java
String s1 = new String("Java");
String s2 = new String("Java");
```

### literal 이용 - String pool에 생성
- String pool은 Heap 메모리 내에 있는 특정 영역이라고 이해하면 된다.
- String pool은 이미 같은 내용의 문자열이 생성되었을 경우, 새롭게 생성하는 것이 아니라 재사용한다.

```java
String s3 = "Java";
String s4 = "Java";
```

![스크린샷 2020-05-10 오후 10 26 23](https://user-images.githubusercontent.com/26040955/81500457-49c92b80-930d-11ea-905d-11a771b5f338.png)


### == operator & equals() method
- ==은 String 비교 시 주소값이 동일한지 보는 것이고, equals()는 문자열 값이 동일한지 보는 것

![스크린샷 2020-05-10 오후 10 29 02](https://user-images.githubusercontent.com/26040955/81500516-a88ea500-930d-11ea-8abb-54e39b8caf5e.png)


### 참고자료

- 인프런 - 호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25
