SELECT 
--------------------------
SELECT는 오라클에서 저장된 데이터를 조회할 때 사용하는 명령어입니다.

오라클에서 SELECT ~ FROM의 실행 순서 분석
------------------------------------
- FROM 테이블명 : 가장 먼저 테이블이 존재하는지를 식별하고 접근합니다. DBMS는 테이블을 식별해야만 데이터를 가져올 수 있습니다.
- SELECT 컬럼명 : 테이블이 식별된 이후에야 어떤 데이터를 가져올 지 결정합니다.
  
SQL문의 대소문자 구분
------------------------------
- DBMS에 따라 다르지만 SQL문을 대소문자 구분 없이 입력해도 수행이 되지만, 내부적으로 대소문자가 다르면 다른 SQL문으로 인식될 가능성이 있습니다.
- 그렇기 때문에 SQL 문장을 작성할 때 대소문자 구분을 반드시 하는 습관을 들여야 합니다.
- 보통은 그래서 키워드 부분은 대문자, 컬럼명이나 조건 등은 소문자로 통일합니다.

표현식(Expression)
--------------------------
- 표현식(Expression)이란 SQL의 SELECT 문에서 컬럼명 이외에 계산된 값, 함수, 문자열 등을 출력할 때 사용됩니다.
- 표현식에는 숫자, 문자열, 연산식, 함수 등이 포함될 수 있습니다.
- 만약 문자 표현식을 사용하고 싶다면 ''를 이용해 작은 따옴표로 감싸야 하지만, 숫자 연산 및 함수 호출 등은 작은 따옴표 없이도 사용 가능합니다.
- 표현식을 사용하면 모든 행에서 동일한 값을 출력할 수 있고, 연산이나 함수 등을 사용해서 출력될 값을 동적으로 변경할 수도 있습니다.

```sql
SELECT empno * 1.1 AS "New SALARY" FROM emp; // 숫자 연산을 포함한 표현식입니다.
SELECT '안녕' FROM emp; // 문자를 작은 따옴표로 감싼 문자 표현식입니다.
```
  
```sql
SELECT * FROM users WHERE user_id = 1; // 키워드는 대문자, 컬럼명/테이블명은 소문자로 작성하는 관례를 반드시 지킵시다.
DESC dept; // DESC 테이블명 -> 테이블에 어떤 컬럼이 있는지를 조회합니다.
SELECT empno FROM emp; // SELECT 컬럼명 FROM 테이블명 -> 테이블에서 특정 컬럼만 조회합니다.
SELECT empno, ename FROM emp; // SELECT 컬럼명1, 컬럼명 2 FROM 테이블명 -> 테이블에서 여러 개의 컬럼을 선택해서 조회합니다.
SELECT * FROM emp; // SELECT * FROM 테이블명 -> 테이블에서 모든 컬럼을 조회합니다.
SELECT name, 'good morning~~!' "Good Morning"
FROM professor; // -> 
```

