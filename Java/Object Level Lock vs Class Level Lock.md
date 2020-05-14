
### Class Level Locking이 가능한 이유
- Class의 object들은 class의 정보를 Class.class로부터 가져오게 되는데, Class.class를 lock하게 되면 class의 모든 객체는 대기할 수 밖에 없는 것.

### 참고자료
- https://howtodoinjava.com/java/multi-threading/object-vs-class-level-locking/
