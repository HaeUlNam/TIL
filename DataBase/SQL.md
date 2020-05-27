### Select문

- attribute list: 쿼리를 날려서 얻어오려고 하는 속성 리스트
- table list: 쿼리를 날리려는 테이블
- condition: 쿼리의 조건
<img width="237" alt="스크린샷 2020-05-07 오후 7 27 26" src="https://user-images.githubusercontent.com/26040955/81284214-ca332680-9098-11ea-9efc-8767ef18f1fc.png">

### ORDER BY

- 지정한 속성을 정렬하는 기능이다.
- ASC: 오름차순(Default)
- DESC: 내림차순
- ex) order by workdate desc, age

### 상위 n개를 뽑는 법
- LIMIT n을 하면 된다.
- 참고: https://luciferd.tistory.com/entry/MYSQL-limit-%EB%AA%85%EB%A0%B9%EC%96%B4

### 중복제거 && NULL 예외처리

```sql
SELECT COUNT(DISTINCT(NAME)) #DISTINCT로 NAME의 중복제거
FROM ANIMAL_INS
WHERE NOT NAME is NULL       #NAME 중에 NULL인 것은 뺀다.
```

- 참고: http://blog.naver.com/PostView.nhn?blogId=50after&logNo=220939090572&parentCategoryNo=6&categoryNo=&viewDate=&isShowPopularPosts=true&from=search

### 최대,최소

```sql
SELECT MIN(DATETIME) # 최댓값일 경우 MAX
FROM ANIMAL_INS 
```
- 참고: https://extbrain.tistory.com/55

### GROUP BY 시간

```sql
SELECT HOUR(DATETIME), COUNT(*)
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) >= 9 AND HOUR(DATETIME) <= 19 # 9시부터 19시까지의 제한조건
GROUP BY HOUR(DATETIME) # 시간단위로 grouping, 1 day 기준으로 하려면 DAY(DATETIME)으로 해야함.
```

- 참고: https://stackoverflow.com/questions/14845981/datetime-group-by-date-and-hour/14846088

### CASE문 

```sql
CASE WHEN 조건
THEN 참일때
ELSE 아닐때
END AS column 상위에 적는 것
```


### 참고
- [[oracle] 상위 n개 데이터만 뽑고 싶은 경우](http://blog.naver.com/PostView.nhn?blogId=nomadgee&logNo=220854618303)
