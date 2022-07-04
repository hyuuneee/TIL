### 문자열 처리 함수 (이어서...)

`repeat(문자열, 횟수)` : 문자열을 횟수만큼 반복

`replace(char1, str1, str2)` : 문자열의 특정 문자를 다른 문자로 변환

`Ltrim('     abc'), Rtrim('abc     '), Trim('  abc   ')` : 문자열의 왼쪽, 오른쪽 양쪽의 공백 제거



### 날짜 처리 함수

CURDATE() : 현재 년월일

CURTIME() : 현재 시분초 

NOW() : 년월일 시분초

SYSDATE() : 년월일 시분초

DATE() : 날짜와 시간에서 년월일 반환

TIME() : 날짜와 시간에서 시분초 반환

날짜데이터에서 특정 년,월,일,시,분,초,밀리초 반환

YEAR(NOW()), MONTH(NOW()), DAYOFMONTH(NOW()), HOUR(NOW()), MINUTE(NOW()), SECOND(NOW()), MICROSECOND(NOW())

ADDDATE : 날짜를 기준으로 차이를 더한 날짜를 반환

SUBDATE : 날짜를 기준으로 차이를 뺀 날짜를 반환

DATEDIFF(날짜1, 날짜2) : 날짜2에서 날짜1까지 몇일 남았는지 반환

TIMEDIFF(날짜1 OR 시간1, 날짜2 OR 시간2) : 시간이 얼마나 남았는지 반환

DAYOFWEEK(날짜) : 요일 반환 (월:2, 화:3, ...)

MONTHNAME(날짜) : 해당 월의 영어이름 반환

DAYOFYEAR(날짜) : 1년 중 몇일이 지났는지 반환

LASY_DAY(날짜) : 주어진 월의 마지막날을 반환

TIME_TO_SEC(시간) : 시간을 초 단위로 반환



### 변환 함수

* DATE_FORMAT(날짜시간, 포맷형식)

​		날짜를 원하는 형식으로 출력 가능하다.

|  %Y  |  년  |      4자리 연도       |
| :--: | :--: | :-------------------: |
|  %y  |  년  |      2자리 연도       |
|  %m  |  월  |       2자리 월        |
|  %M  |  월  | 월의 영어이름(풀네임) |
|  %b  |  월  |  월 영어이름(줄여서)  |
|  %d  |  일  |       2자리 일        |
|  %H  |  시  |      24시간 형식      |
|  %h  |  시  |      12시간 형식      |
|  %i  |  분  |       2자리 분        |
|  %s  |  초  |       2자리 초        |
|  %W  |  주  |       영어 요일       |
|  %a  |  주  |   영어 요일 줄여서    |



### 그룹함수

여러 행 또는 테이블 전체의 행에 대해 함수가 적용되어 하나의 결과값을 가져오는 함수이다.

Group By절을 이용하여 그룹화 할 수 있고, Having절을 이용하여 그룹 함수에 대해 조건비교를 할 수 있다. count(*)를 제외한 모든 그룹함수는 NULL값을 고려하지 않는다. 

count() : 검색된 행의 수 반환

Max(), Min() : 컬럼 중 최대값, 최소값 반환

Avg() : 평균값 반환

Sum() : 검색된 컬럼의 합 반환

where -> group by -> having -> order by 의 순서로 작성한다.

```
-- 담당업무별 사원수, 급여의 합, 급여의 평균
 select job, count(empno), sum(sal), avg(sal) from emp group by job; -- group by에 작성한 컬럼명을 select에 작성
 -- 담당업무별 사원수가 3명 이상인 경우 선택 
 select job, count(empno), max(sal), min(sal) from emp group by job having count(empno)>=3; -- group 함수를 가지고 조건비교
 -- 급여가 2500불 이상인 사원을 부서별 급여의 합계, 평균을 구하되 부서별 급여의 평균이 2900불 이상인 부서만 선택하라
 select deptno, sum(sal), avg(sal) from emp where sal>=2500 group by deptno having avg(sal)>=2900 order by deptno;
```



## 데이터 조작어 [데이터의 삽입, 수정, 삭제]

### INSERT

 테이블 안에 레코드를 삽입하는 역할을 한다.

**INSERT INTO** table_name(column1, column2...) **VALUES** (데이터1, '데이터2'.....)

테이블 이름 옆에 () 생략시에는 모든 칼럼을 VALUES()안에 입력한다.

primary key는 value값을 꼭 입력해야 한다. (null값 허용 안하기 때문)



### UPDATE

테이블 안의 레코드를 수정한다.

**UPDATE** table_name **SET** column1=값(고칠내용), column2=값... **WHERE** 조건

where절을 생략하면 모든 레코드를 수정하게 된다.

```
20부서 사원들의 급여 10% 인상
update emp set sal = sal*1.1 where depno =20;
```



### DELETE

사용하지 않는 레코드를 삭제한다.

**DELETE FROM** table_name **WHERE** 조건



## 테이블의 생성, 수정, 삭제

테이블은 데이터베이스의 기본적인 데이터 저장 단위이다. 

### CREATE : 테이블 생성

**CREATE TABLE** [schema] table_name

​	( column datatype

​	  column datatype

​              ......

   );

* 테이블 복사하기

**create table** table_name **as select * from** 복사할 테이블;

* 데이터 타입

테이블 생성할 때 각 컬럼에 지정할 수 있는 데이터 타입

정수형 : bit, bool, tinyint, smallint, mediumint, int, integer, bigint

고정소수점형(실수형) : decimal, bool

날짜형 : date(날짜), datetime(날짜와 시간), timestamp, time, year

문자형 : char(고정길이), varchar(가변길이), tinyblob, tinytext, blob, text, mediunblob, mediumtext, longblob, longtext, enum, set



### DROP : 테이블 삭제

**drop table** table_name;



### ALTER : 테이블 관리

* ADD : 테이블에 새로운 필드 추가

**alter table** emp **add** email varchar(50); 

null로 지정해야 한다

* MODIFY : 필드의 크기를 수정하거나 not null 컬럼으로 변경 가능

**alter table** emp **modify** depart varchar(20);

크기를 초과하고 있는 레코드가 이미 존재한다면 수정 불가

* CHANGE : 필드명을 변경

**alter table** emp **change **tel phone varchar(20);

* DROP : 필드 삭제

**alter table** emp **drop column** position;



----

### DB설계하기

모델 생성하여 DB 설계와 함께 테이블 생성까지 할 수 있다.

- Join 

외래키를 사용하여 여러개의 테이블을 사용할 수 있다.

