# INDEX 이어서

> PK나 UNIQUE제약 조건을 정의할 경우 UNIQUE INDEX가 자동으로 생성됨



## INDEX의 종류

### 고유 인덱스(UNIQUE INDEX)

- 유일한 값을 가지는 컬럼에 대해서 생성하는 인덱스로 고유 인덱스를 지정하려면 UNIQUE 옵션을 지정해야 함.



### 비고유 인덱스(NON UNIQUE INDEX)

- 중복되는 데이터가 들어가야 하는 경우



### 단일 인덱스(SINGLE INDEX)

- 한 개의 컬럼으로 구성한 인덱스를 의미.



### 결합 인덱스(COMPOSITE INDEX)

- 두 개 이상의 컬럼으로 인덱스를 구성하는 것.

  - ex) 부서 번호와 부서명으로 결합

  

### 함수 기반 인덱스(FUNCTION BASED INDEX)

- '컬럼'*N과 같이 컬럼에 어떠한 산술식을 수행했을 때를 의미
  - SAL 컬럼에 INDEX가 걸려있을 때 SAL*5는 INDEX를 타지 못 함.
  - -> 이럴 때 함수 기반 인덱스를 생성
- 잘못 생성하게 되면 성능에 나쁜 영향을 가하게 됨.

- 기존 인덱스를 활용 할 수 없음.



## INDEX 생성 방법

```mysql
# 고유 인덱스 생성
CREATE UNIQUE INDEX `인덱스 이름`
ON `테이블 이름`('테이블 컬럼')
```



```mysql
# 단일 인덱스 생성
CREATE INDEX `인덱스 이름`
ON `테이블 이름`('테이블 컬럼')
```



```mysql
# 결합 인덱스 생성
CREATE INDEX `인덱스 이름`
ON `테이블 이름`('테이블 컬럼1','테이블 컬럼2')
#WHERE 컬럼1 = 'A'
#AND 컬럼2 = 'B'와 같은 구문이 많이 사용 될 때
```



```mysql
# 함수 기반 인덱스 생성
CREATE INDEX `인덱스 이름`
ON `테이블 이름`('테이블 컬럼1'+150)
```



```mysql
# 인덱스 생성시 정렬
# 정렬 방법을 지정하여 인덱스를 만들 때
CREATE INDEX `인덱스 이름`
ON `테이블 이름`('테이블 컬럼' ASC|DESC)
# ASC이 기본값
```