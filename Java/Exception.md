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

### 참고자료
- 호주 현직 자바 개발자가 묻고 답하는 영어 기술면접 25
