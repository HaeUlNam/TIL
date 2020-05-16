## Blocking vs Non-Blocking
- Blocking: 호출된 함수가 자신의 작업을 모두 마칠 떄까지 호출한 함수에게 제어권을 넘겨주지 않고 대기하게 만드는 것
- Non-Blocking: 호출된 함수가 바로 리턴해서 호출한 함수에게 제어권을 넘겨주고, 호출한 함수가 다른 일을 할 수 있도록 기회를 줄 수 있는 것

## Synchronous/Asynchronous

- Synchronous: 호출되는 함수가 호출되는 함수의 작업 완료 후 리턴을 기다리거나 또흔 호출되는 함수로부터 바로 리턴 받더라도 작업 완료 여부를 
호출하는 함수 스스로 계속 확인하며 신경쓰면 Synchronous이다.

- Asynchronous: 호출되는 함수의 작업 완료를 신경쓰지 않는다. 호출되는 함수에게 callback을 전달해서, 호출되는 함수는 전달받은 callback을 실앻.

### Blocking-Synchronous && Non-Blocking-Asynchronous

![image](https://user-images.githubusercontent.com/26040955/82120583-33661880-97c2-11ea-8ed0-b161d8556e4a.png)


### NonBlocking-Sync
- 함수는 바로 리턴하고, 작업 완료 여부를 신경쓰는 것이다. 따라서 중간중간 물어보는 것이 더 효율적이기에 다음과 같이 할 수 있다.
![image](https://user-images.githubusercontent.com/26040955/82120706-0cf4ad00-97c3-11ea-85a1-60f8858d716b.png)

### Blocking- Async
- 함수를 바로 리턴하지 않고, callback으로 결과 전달.
- 꼭 써야 하는 경우 아니면 잘 쓰지 않는 방법


### 참고자료
- [Blocking-NonBlocking-Synchronous-Asynchronous](https://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)
