### index
#### index란?
* 검색을 빠른 속도로 하기 위해서 사용된다.
* SQL 명령문의 처리 속도를 향상시키기 위해서 컬럼에 대해서 생성하는 오라클 객체

#### index 사용하는 경우
* 테이블에 행의 수가 많을때
* where문에 해당 컬럼이 많이 사용되는 경우
* 적은 양의 컬럼을 가져올때
* join에 많이 사용되는 컬럼
* null을 포함하는 컬럼이 많은 경우

#### 사용하지 말아야되는 경우
* 테이블에 행의 수가 작을때
* where문에 해당 컬럼이 작게 사용되는 경우
* 테이블에 DML 작업이 많은 경우
* 많은 양의 데이터를 가져오는 경우

#### index 생성 방법
```SQL
--index 생성법
create index index명 on table명(index걸어줄 table에 colum명);
ex)create index idx_emp_ename on emp(ename);
```

#### index 제거
```SQL
--index 제거
drop index index명
ex)drop index idx_emp_ename;
```

#### index 재생성
```SQL
--index 재생성
alter index index명 rebuild;
ex)alter index idx_emp_ename rebuild;
```

#### index 종류
* Unique Index(고유 인덱스) - 유일한 값을 갖는 컬럼에 대해서 생성하는 인덱스
* NonUnique Index(비고유 인덱스) - 중복된 데이터를 갖는 컬럼에 대해서 생성하는 인덱스
* Single Index(단일 인덱스)
* Composite Index(결합 인덱스)

출처 : http://hyun0412.tistory.com/entry/oracle-index-%EC%A0%95%EB%A6%AC
