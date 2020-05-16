## Locality of reference

- 지역성: 프로그램이 실행하다보면 메모리에 Access할 텐데, 프로그램이 모든 공간을 Access하는 것이 아니라 일부만 Access하더라..

### Temporal locality(시간 지역성)
- 최근에 Access한 데이터를 다시 Access할 가능성이 높다.

### Spatial locality(공간 지역성)
- 최근에 Access한 데이터 주변을 참조할 가능성이 높다.
- 그래서 Cache의 데이터를 접근할 때, 1 Block(64Byte)단위로 Access한다. 그 Block 안에 자신이 원하는 데이터가 있다면 접근할 수 있다.

### 캐쉬 Hit&& Miss
- Hit Time << Miss Penalty : Cache에 있는 데이터를 가져오는 Hit 시간보다 Miss해서 하위 Level로부터 데이터를 가져와서 전달하는 시간이 더 걸리기 때문에 
지역성이 높을 수록 메모리 캐시를 통한 성능 향상을 기대해볼 수 있다.
