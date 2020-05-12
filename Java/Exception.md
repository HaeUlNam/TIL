### Exception vs Error
- Excetion : 일어난 예외 상황을 다룰 수 있다.
  * checked: compile time에 일어난다.(syntax)
  * unchecked: run time에 일어난다.(NullpointException)

- Error: 심각해서 다시 시작해야 한다.
  * severe exception: 너무 심각해서 복구하기 어려움.(OOM - OutOfMemory)
  
### Exception Handling

- try, catch block: 직접 exception 처리

<img width="416" alt="스크린샷 2020-05-11 오후 9 09 59" src="https://user-images.githubusercontent.com/26040955/81560148-c91d3480-93cb-11ea-9bf7-e0d04f4213aa.png">

- throws: 자신을 호출한 함수에게 예외를 던진다.

<img width="576" alt="스크린샷 2020-05-11 오후 9 11 13" src="https://user-images.githubusercontent.com/26040955/81560235-f4a01f00-93cb-11ea-9d36-5c64ea6a19ee.png">


### Throw
- 개발자가 직접 필요에 의해 Exception을 발생시키기에 아래와 같이 객체를 생성해서 throw해야 한다.
- 그러면 try catch블럭으로 예외를 처리.
- 오직 한 객체만 사용할 수 있다.

<img width="590" alt="스크린샷 2020-05-11 오후 9 22 41" src="https://user-images.githubusercontent.com/26040955/81561070-8f4d2d80-93cd-11ea-926e-c447b5da5d03.png">


### Try Catch and Finally

- try 블럭에서 예외 발생하지 않으면: try 블럭 -> finally -> 나머지 코드
- try 블럭에서 예외 발생하면: try 블럭 -> catch -> finally -> 나머지 코드
- 보통 Finally는 이처럼 어떠한 경우에도 거치게 되기에, DB connection이나 stream close하는 것과 같이 resource를 release하는 구현에 사용.

![스크린샷 2020-05-12 오후 3 50 04](https://user-images.githubusercontent.com/26040955/81647604-40a0a180-9468-11ea-8cd4-92b7900466d7.png)

- 만약 아래와 같이 try block에 system.exit(0);을 한다면 프로세스를 종료시키기에 finally block을 거치지 않고 프로그램이 바로 종료됩니다.

![스크린샷 2020-05-12 오후 4 06 49](https://user-images.githubusercontent.com/26040955/81649001-97a77600-946a-11ea-88ad-8afaa7aac611.png)

- 하지만 return을 한다면 finally block을 거치고 함수를 종료하게 됩니다.

![스크린샷 2020-05-12 오후 4 06 59](https://user-images.githubusercontent.com/26040955/81649016-9e35ed80-946a-11ea-8570-c671c019775e.png)


### 참고자료
- 호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25
