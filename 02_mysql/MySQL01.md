## MySQL 

MySQL은 세계에서 가장 많이 쓰이는 오픈 소스의 관계형 데이터베이스 관리 시스템(**RDBMS**)이다. 

MySQL 하위에 root(계정)가 있고 root의 하위에 db들이 존재한다. db의 하위에는 테이블들이 있다.  테이블은 데이터, 레코드(행), 필드(컬럼)으로 이루어져 있다.

 

* MySQL 설치 후 cmd에서 사용하기

  `mysql -u root -p` : mysql에 연결

  `show databases / tables` : database 또는 table 목록 확인

  `create database (이름)` : database 생성

  `use (데이터베이스명)` : 데이터베이스 선택

  `source (파일명)` :  외부에 있는 파일의 쿼리문 실행

  `select * from 테이블명` : 테이블 전체 데이터 보기

* 제어판 - 서비스에서 MySQL 실행과 중지가 가능하다.



## SQL문

관계형 데이터베이스에서 사용하는 표준 질의언어이다. 모든 DBMS에서 사용 가능하며, 대소문자를 구분하지 않는다는 특징이 있다.



### 1) 데이터조작언어 DML(Data Manipulation Language)

`INSERT(입력)`, `DELETE(삭제)`, `UPDATE(수정)`, `SELECT(검색)`

* SELECT문 및 연산자

  SELECT문은 데이터베이스로부터 저장되어 있는 데이터를 검색하는데 사용한다.

  ```
  SELECT {*, column [alias], ..} FROM table_name [WHERE condition]
  [ORDER BY {column, expression} [ASC | DESC]];
  ```

  `*`: 테이블의 모든 column 출력

  `alias`: 해당 column에 대해 다른 이름 부여

  `WHERE` : 레코드에 대한 조건식

  `ORDER BY` : 레코드를 오름차순 또는 내림차순으로 정렬 (디폴트는 오름차순)

* SQL 연산자

  * 산술 연산자 : +, - , *, /

  * 비교 연산자 : =, !=, <>, ^=, >, <, >=, <=

  * 논리 연산자 : and, &&, or, ||, not

  * SQL 연산자 : BETWEEN a AND b, In (list), Like, IS NULL, NOT BETWEEN a AND b, NOT IN (list), NOT LIKE, IS NOT NULL

    * BETWEEN 연산자 : 범위를 지정할 때 사용

    * IN (list) 연산자 : list의 값 중 어느 하나와 일치하는 데이터를 출력

    ```
    사원번호가 7369, 7654, 7788인 사원을 선택하라.
    select * from emp where empno in(7369,7654,7788);
    사원번호가 ~인 사원을 제외하고 선택하라.
    select * from emp where empno not in(7369,7654,7788);
    ```

    * LIKE 연산자 : 문자열내에 특정 데이터가 포함된 정보를 선택할 때

    ```
    % : 여러문자, _ : 한문자
    사원명이 A로 시작하는 사원을 선택하라
    select * from emp where ename like 'A%';
    사원명에 A를 포함하는 사원을 선택하라.
    select * from emp where ename like '%A%';
    이름의 두번째 글자가 A인 사원을 선택하라.
    select * from emp where ename like '_A%';
    이름에 D가 포함된 사원을 제외한 나머지 사원을 선택하라.
    select * from emp where ename not like '%D%';
    ```

    * IS NULL : NULL값을 가진 데이터 출력

    ```
    null은 모든 연산에서 제외되기 때문에 null 전용 연산자인 is null을 사용한다.
    null을 다른 값으로 변경하여 작업하기 가능
    select comm, ifnull(comm,0)+100 comm2 from emp;
    mgr가 null이 아닌 사원을 선택하라.
    select * from emp where mgr is not null;
    ```

* 내장 함수 1 : 숫자 함수

` ABS(-10);` : 절대값
` CEIL(54.1), FLOOR(19.9);` : 올림, 버림
` MOD(10,3), 10 % 3;` : 나머지
` floor(RAND()*6)+5;` : 5~10사이의 난수 
` POW(5,3), SQRT(16);` : 거듭제곱, 루트
` ROUND(253.2654,2), ROUND(253.845,-2);` : 반올림 (양표음반)
`FORMAT(25364.532,2);` : 원하는 소수자릿수까지 작성 + 세자리마다 , 삽입

* 내장 함수 2 : 문자열 처리 함수

`ascii('A');` : 아스키코드값으로 변환
`char(66);` : 아스키코드를 문자로 반환
`bit_length('abc'), char_length('abc'), length('abc');` : bit크기, 문자수, 바이트 크기  // 1바이트 = 8bit, mysql에서 한글은 3바이트
`concat(2022, 6, 27), concat_ws('-',2022,3,10);` : 문자열 연결, 구분자와 함께 문자열 연결
`elt(2, 'A', 'B', 'C', 'D') ` : 위치번째의 문자를 반환                                        `field('b','x','y','b','z')` : 찾을 문자열의 위치를 찾는다, 없으면 0 `find_in_set('text','text,sample,apple') ` : 찾을 문자열을 문자열 리스트에서 찾아서 위치 반환 
`instr('abcd','c') ` : 기준 문자열에서 부분 문자열을 찾아서 위치 반환                                                    `locate('x', 'xyz') ;` : 문자열에서 문자의 위치 반환 
`insert(ename, 2, 2, '**') ` : 기준 문자열의 위치부터 길이만큼을 삽입할 문자열로 변경
`ename, reverse(ename) ` : 문자열 거꾸로 
`left(ename, 2), right(ename, 2) ` : 왼쪽 2글자, 오른쪽 2글자 반환
`lcase(ename), ucase('abcd') ` : 소문자, 대문자로 변환
`lpad(ename, char_length(ename)+1, '*'), rpad(ename, 10, '*') ` : 입력한 문자열의 길이내에 왼쪽, 오른쪽에 문자열을 끼어 넣음
`substring('abcdef', 3, 2);` : 시작위치부터 길이만큼 문자를 반환
`substring_index('www.nate.com','.',2)` : 두번째 . 까지 반환   `substring_index('www.naver.com','.',-2)` : 뒤에서 두번째 . 까지 반환`substring_index('www.naver.com','n',-1);` : 뒤에서 첫번째 n까지 반환