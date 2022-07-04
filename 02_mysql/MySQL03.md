## 서브쿼리 

* 단일 행 서브쿼리 : 오직 한개의 행(값)을 반환 한다. 

​										단일 행 연산자(=,>,>=,<=,<>,!=)만 사용할 수 있다.

EX 1) ford와 같은 부서의 사원중 평균 급여보다 작게 받는 사원은?

select * from emp where deptno=(select deptno from emp where ename='ford') and sal < (select avg(sal) from emp);

EX 2) 담당 업무별 급여의 합계와 급여의 평균을 구하되 전체 사원의 평균보다 많이 받는 담당업무를 선택하라.

select job, sum(sal) 급여합계, avg(sal) 급여평균 from emp group by job having avg(sal)>(select avg(sal) from emp);



* 다중 행 서브쿼리 : 하나 이상의 행을 반환하는 서브쿼리이다. 

​										복수 행 연산자(IN, NOT IN, ANY, ALL, EXISTS)를 사용 할 수 있다.

in : or의 개념 / any : 서브쿼리의 결과값 중 어느 하나의 값이라도 만족하면 결과값 반환 / all : 결과값 중 모든 결과값이 만족되어야 함 / exists : 서브쿼리의 데이터가 존재하는가의 여부를 따져 존재하는 값들만 결과로 반환

EX 1) 업무가 'SALESMAN'인 사원의 최소급여보다 많으면서 부서번호가 20번이 아닌 사원의 이름과 급여, 부서코드를 출력하라.

SELECT ename, sal, deptno FROM emp WHERE deptno !=20 AND sal > ANY(SELECT sal FROM emp WHERE job='SALESMAN');

EX 2) 업무가 'SALESMAN'인 사원의 최대급여보다 많으면서 부서번호가 20번이 아닌 사원의 이름과 급여를 출력하라.

SELECT ename, sal FROM emp WHERE deptno != 20 AND sal > ALL(SELECT sal FROM emp WHERE job='SALESMAN');

EX 3) 사원을 관리할 수 있는 사원의 정보를 선택하라.

SELECT empno, ename, sal FROM emp e WHERE EXISTS(SELECT empno FROM emp WHERE e.empno = mgr);



* 다중 열 서브쿼리 : 서브쿼리의 결과값이 두개 이상의 컬럼을 반환한다.

EX 1) 사원테이블에서 급여와 보너스가 부서 30에 있는 사원의 급여, 보너스와 일치하는 사원의  이름, 부서번호, 급여, 보너스를 출력하라.

select empno, ename, sal, deptno, comm from emp
where (sal, deptno) in(select sal, deptno from emp where deptno=30 and comm is not null);



* FROM절 서브쿼리 : 하나의 테이블에서 자료의 양이 많을 경우 필요한 행과 열만 선택하여 FROM절에 기술한다. 서브쿼리로 새로운 테이블로 생성한 것과 비슷하다.



## 제약조건 

제약조건이란 테이블에 부적절한 자료가 입력되는 것을 방지하기 위해서 여러 가지 규칙을 적용한 것이다. 즉, 데이터의 무결성 유지를 위하여 사용자가 지정할 수 있는 성질이다. 제약조건에는 not null, primary key, foreign key, unique, check, default가 있다.

제약조건 확인하는 법 : SELECT * FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS  WHERE TABLE_NAME='----------';

* not null : 컬럼을 필수 필드화 시킬 때 사용한다

**create table** table_name( 컬럼명 데이터타입 **not null**);

* unique : 데이터의 유일성 보장한다. 중복데이터 허용 안한다. 자동으로 index 생성된다.

**alter table** table_name **add constraint** 제약조건이름 **unique**(컬럼명);

* check : 컬럼의 값을 특정 범위로 제한 할 수 있다. 조건식에서 IN연산자 사용 가능하다.

**alter table** table_name **add constraint** 제약조건이름 **check** (조건);

* default : 데이터 입력시에 입력을 하지 않아도 지정된 값이 입력될 수 있다. 기본값 지정.

**create table** table_name(컬럼명 데이터타입 **default** 기본값);

* primary key : 중복 데이터 허용 안한다.

**alter table** table_name **add primary key** (기본키로 지정할 컬럼);

* foreign key : 외래키, 기본키를 참조하는 컬럼 또는 컬럼들의 집합이다. 외래키를 가지는 컬럼의 데이터형은 외래키가 참조하는 기본키의 컬럼과 데이터형이 일치해야 한다. 외래키에 의해 참조되고 있는 기본키는 삭제할 수 없다. 

on delete/update cascade : 다른 테이블의 기존 행에 있는 외래 키에서 참조하는 키가 포함된 행을 삭제/수정하려고 하면 해당 외래키가 포함되어 있는 모든 행도 삭제/수정되도록 지정한다.

no action : 참조되는 있는 데이터의 삭제, 수정이 불가능하다 (기본값)

**alter table** table_name **add constraint** 제약조건이름 **foreign key** (참조하는컬럼) **references** 참조되는테이블(컬럼명) **on delete cascade**;

* 제약조건 삭제

**alter table** table_name **drop constraint** 제약조건이름;

* 외래키 삭제

**alter table** table_name **drop foreign key** 제약조건이름;

