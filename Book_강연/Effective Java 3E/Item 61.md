## 박싱된 기본 타입보다는 기본 타입을 사용하라

- 다음은 기본 타입과 박싱된 기본 타입의 주된 차이점 3가지이다.
  * 기본 타입: int, double, float
  * 박싱된 타입: Integer, Double, Float
  
### 첫번째, 기본 타입은 값만 가지고 있지만 박싱된 기본 타입은 값에 더해 식별성이라는 속성도 갖는다.
- 즉 박싱된 타입은 값이 동일하더라도 다르다고 식별될 수 있다.
- 다음 예제는 Integer 값을 오름차순으로 정렬하는 비교자
  * 아래가 Collections.sort로 실행되면, 첫번째 비교 연산인 (i < j)을 실행할 때 i와 j는 각각 int로 변환되어 비교 연산을 하고 다음 연산으로 넘어가게 된다. 그런 다음 (i == j)를 실행하게 된다면, int로 변환되어 
  비교하는 것이 아니라, Integer의 주소 값 비교를 하게 되는 것이다. 따라서 식별성 검사.
  * 그러면 0을 반환하는 것이 아니라 1을 반환하게 된다.
```java
Comparator<Integer> naturalOrder =
    (i, j) -> (i < j) ? -1 : (i == j ? 0 : 1);
```

- 이를 해결하려면, Comparator.naturalOrder를 사용하거나 아래처럼 시작부터 int로 바꾸어서 비교하면 된다.
```java
Comparator<Integer> naturalOrder = (iBoxed, jBoxed) -> { 
    int i = iBoxed, j = jBoxed; // 오토박싱
    return i < j ? -1 : (i == j ? 0 : 1); 
};
```

- 추가적 참고: [[Java] Integer.valueOf(127) == Integer.valueOf(127) 는 참일까요?](https://meetup.toast.com/posts/185)

### 두번째, 박싱된 타입은 유효하지 않는 값 null을 가질 수 있다.

```java



```


### 세번째, 기본 타입이 박싱된 기본 타입보다 시간과 메모리 사용면에서 더 효율적이다.

