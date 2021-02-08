# SQL, DDL, DML, DCL

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung-Kwon*

<hr>

### SQL (Structured Query Language)

- <b>SQL 이란?</b>

  - 관계형 데이터베이스 관리 시스템 (RDBMS) 의 데이터를 관리하기 위해 설계된 특수 목적의 프로그램 언어이다.
  - 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정과 관리를 위해 고안되었다.
  - 데이터베이스로 부터 정보를 얻거나 갱신하기 위한 표준 대화식 프로그래밍 언어이다.
  - 많은 수의 데이터베이스 관련 프로그램들이 SQL을 표준으로 채택하고 있다.

<br/>

  <br/>

- <b>SQL의 문법 종류 3가지</b>

  - DDL (Data Definition Language) - 데이터 정의어
  - DML (Data Manipulation Language) - 데이터 조작어
  - DCL (Data Control Language) - 데이터 제어어

<br/>

<br/>

<br/>

### DDL (Data Definition Language)

- <b>DDL 이란?</b>
  - 데이터 정의 언어
  - 테이블이나 관계의 구조를 생성하는데 사용한다.
  - 데이터베이스와 <b>테이블을 생성, 수정, 삭제</b>하는 등 데이터 전체의 골격을 결정한다.
  - SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 정의하거나 변경 또는 삭제할 때 사용하는 언어이다.
  - 데이터베이스 관리자나 설계자가 사용한다.

<br/>

- <b>데이터 정의어 종류</b>
  - CREATE : 데이터베이스, 테이블 등을 생성하는 역할
  - ALTER : 테이블을 수정하는 역할
  - DROP : 데이터베이스, 테이블을 삭제하는 역할
  - TRUNCATE : 테이블을 초기화시키는 역할

<br/>

- <b>사용 예시</b>

  <small>정확한 의미의 스키마와 데이터베이스는 다르지만 MySQL 에서는 같은 것으로 본다.</small>

  - <b>스키마 / 데이터베이스 정의</b>

    - 스키마 생성 / 데이터베이스 생성

      ``` SQL
      CREATE SCHEMA 스키마명;
      CREATE DATABASE 데이터베이스명;
      ```

    <br/>

    - 스키마 삭제 / 데이터베이스 삭제

      ``` SQL
      DROP SCHEMA 스키마명;
      DROP DATABASE 데이터베이스명;
      ```

    <br/>

    <br/>

  - <b>테이블 정의</b>

    - 테이블 생성

      ``` SQL
      CREATE TABLE 테이블명(
      	컬럼명1 데이터타입 [DEFAULT 형식],
      	컬럼명2 데이터타입 [DEFAULT 형식]
      );
      ```

      <br/>

    - 제약 조건

      - PRIMARY KEY (기본키)

        - 기본키 설정
        - PRIMARY KEY = UNIQUE KEY & NOT NULL

        <br/>

      - UNIQUE KEY (고유키)

        - NULL 가능
        - 중복된 값 불가

        <BR/>

      - NOT NULL

        - NULL 값 금지

        <BR/>

      - CHECK

        - 입력할 수 있는 값의 범위 등을 제한
        - TRUE 또는 FALSE로 평가할 수 있는 논리식 지정
        - MySQL 에서 적용할 수 있지만 데이터의 무결성을 강요하지 않음 -> 적용 안됨

        <BR/>

      - FOREIGN KEY (외래키)

        - 테이블 간의 관계를 정의하기 위해 다른 테이블의 기본키를 외래키로 지정
        - 외래키 지정 시 참조 무결성 제약 옵션 선택 가능

        <BR/>

        ``` SQL
        CREATE TABLE 테이블명(
        	컬럼명1 데이터타입 [DEFAULT 형식],
            컬럼명2 데이터타입 [DEFAULT 형식],
            UNIQUE INDEX 컬렴명_UNIQUE(컬럼명 ASC),
            CONSTRAINT 테이블명_PK PRIMARY KEY(컬럼명),
            CONSTRAINT 테이블명_FK FOREIGN KEY(컬럼명) REFERENCES 상대테이블명(기본키)
            CONSTRAINT CHK_테이블명 CHECK (논리식)
        );
        ```

        ``` SQL
        CREATE TABLE TEST(
        	NO INT NOT NULL,
            NO2 INT,
            NO3 INT,
            UNIQUE INDEX NO2_UNIUQE(NO2 ASC),
            CONSTRAINT TEST_PK PRIMARY KEY(NO),
            CONSTRAINT TEST_FK FOREIGN KEY(NO3) REFERENCES STUDENT(NUM),
            CONSTRAINT CHK_TEST CHECK(NO>=1)
        );
        ```

    <BR/>

    <BR/>

  - <b>테이블 수정</b>

    - 컬럼 추가

      ``` SQL
      ALTER TABLE 테이블명
      	ADD 컬럼명 데이터타입;
      ```

      <BR/>

    - 컬럼 삭제

      ``` SQL
      ALTER TABLE 테이블명
      	DROP 컬럼명;
      ```

      <BR/>

    - 컬럼 수정

      ``` SQL
      ALTER TABLE 테이블명
      	MODIFY 컬럼명 데이터타입;
      ```

      <BR/>

    - 컬럼명 수정

      ``` SQL
      ALTER TABLE 테이블명
      	CHANGE 기존컬럼명 새컬럼명 데이터타입;
      ```

      <BR/>

    - 제약조건 추가

      ``` SQL
      ALTER TABLE 테이블명
      	ADD CONSTRAINT 제약조건명 제약조건 (컬럼명);
      ```

      <BR/>

    - 제약조건 삭제

      ``` SQL
      ALTER TABLE 테이블명
      	DROP 제약조건명;
      ```

    <BR/>

    <BR/>

  - <b>테이블 초기화</b>

    - 테이블의 모든 행을 지움

      ``` SQL
      TRUNCATE TABLE 테이블명;
      ```

      - 테이블은 유지

      <br/>

  - <b>테이블 삭제</b>

    - 테이블 자체를 삭제함

      ``` SQL
      DROP TABLE 테이블명;
      ```

      - TRUNCATE는 테이블은 유지하고 데이터들만 삭제하기 때문에 둘이 차이가 있음

<br/>

<br/>

<br/>

#### DML (Data Manipulation Language)

- <b>DML이란?</b> 

  - 데이터 조작 언어
  - 테이블에 <b>데이터를 검색, 삽입, 수정, 삭제</b>하는 데 사용
    - 정의된 DB에 입력된 레코드 조회, 수정, 삭제 등
  - 데이터베이스 사용자가 응용 프로그램이나 질의어를 통해 저장된 데이터를 실질적으로 처리하는데 사용하는 언어
  - 데이터베이스 사용자와 데이터베이스 관리 시스템 간의 인터페이스 제공

  <br/>

- <b>데이터 조작 언어 종류</b>

  - SELECT : 데이터 조회
  - INSERT : 데이터 삽입
  - UPDATE : 데이터 수정
  - DELETE : 데이터 삭제

<br/>

<br/>

<br/>

### DCL (Data Control Language)

- <b>DCL이란?</b>

  - 데이터 제어 언어
  - 데이터의 <b>사용 권한</b>을 관리하는 데 사용한다.
  - 데이터베이스에 접근, 객체에 권한을 주는 등
  - 데이터의 보안, 무결성, 회복, 병행 수행 제어 등을 정의하는 데 사용한다.

<br/>

- <b>데이터 제어어 종류</b>

  - GRANT : 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 부여
  - REVOKE : 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 박탈, 회수
  - COMMIT : 트랜잭션의 작업이 정상적으로 완료되었음을 관리자에게 알려줌
  - ROLLBACK : 트랜잭션의 작업이 비정상적으로 종료되었을 때 원래 상태로 복구
  
  <br/>
  
- <b>사용 예시</b>

  - <b>GRANT</b>

    - 사용자에게 권한을 부여하는 명령어
  
    - 권한 허용
  
      ``` SQL
      GRANT 명령어 ON 데이터베이스명.테이블 TO 'DKDLEL'@'localhost';
      ```
  
      - '아이디' 사용자에게 데이터베이스명.테이블에서 명령어를 사용할 수 있는 권한을 부여
  
      <br/>
  
      ``` SQL
      GRANT ALL ON TEST.* TO 'test'@'localost';
      ```
  
      - test 사용자에게 TEST 데이터베이스에 있는 모든 테이블의 모든 명령어를 사용할 수 있는 권한을 부여한다.
  
        <small>모든 권한 : SELECT, INSERT, UPDATE, DELETE, CREATE, DROP,REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLE, LOCK TABLES, CREATE VIEW, CREATE ROUTINE, ALTER ROUTINE, EXECUTE, EVENT TRIGGER</small>
  
      <br/>
  
      ``` SQL
      GRANT INSERT ON TEST.* TO 'test'@'localhost';
      ```
  
      - test 사용자에게 TEST 데이터베이스에 있는 INSERT 명령어를 사용할 수 있는 권한을 부여
  
    <br/>
  
    <br/>
  
  - <b>REVOKE</b>
  
    - 사용자에게 권한을 회수하는 명령어
  
      ```SQL
      REVOKE 명령어 ON 데이터베이스명.테이블 FROM '아이디'@'localhost' 
      ```
  
      - '아이디' 사용자에게 데이터베이스명.테이블에서 명령어를 사용할 수 있는 권한을 회수
  
      <br/>
  
      ``` sql
      REVOKE ALL ON TEST.* FROM 'test'@'localhost'; 
      REVOKE INSERT ON TEST.* FROM 'test'@'localhost'; 
      ```
  
    <br/>
  
    <br/>
  
  - <b>COMMIT</b>
  
    - 작업한 결과를 물리적 디스크로 저장하고, 작업이 정상적으로 완료됨을 관리자에게 알려주는 명령어
  
      ``` SQL
      COMMIT; 
      ```
  
    <br/>
  
    <br/>
  
  - <b>ROLLBACK</b>
  
    - 작업했던 내용을 원래의 상태로 복구하는 명령어
  
    - INSERT, UPDATE, DELETE 와 같은 트랜잭션의 작업을 취소
  
    - COMMIT 명령어를 사용하기 이전의 상태만 ROLLBACK 가능
  
      ```sql
      ROLLBACK;
      ```

<br/>

<br/>

<br/>

### DELETE, TRUNCATE, DROP 의 차이

| 명령어   | 특징                                                         |
| -------- | ------------------------------------------------------------ |
| DELETE   | 데이터는 지워지지만 테이블 용량은 줄어들지 않는다. 원하는 데이터만 지울 수 있다. 잘못 삭제 한 경우, 삭제한 것을 되돌릴 수 있다. |
| TRUNCATE | 삭제 후, 용량이 줄어들고 인덱스 등도 모두 삭제된다. 테이블이 삭제 되지는 않으나 데이터만 삭제한다. 선택해서 지울 수 없다. 삭제 후 절대 되돌릴 수 없다. |
| DROP     | 테이블 전체를 삭제한다. 공간, 객체를 삭제한다. 삭제 후 절대 되돌릴 수 없다. |

<br/>

<br/>

## 예상질문❔

Q1) DDL이란 무엇인가?

A1) 데이터베이스와 테이블의 관계의 구조, 즉 데이터의 전체의 골격을 결정하는 데이터 정의 언어이다.

<br/>

Q2) DML이란 무엇인가?

A2) 데이터를 테이블에 삽입, 수정, 삭제, 검색하는 데 사용하는 데이터 조작 언어이다.

<br/>

Q3) DCL이란 무엇인가?

A3) 데이터의 사용 권한을 관리하는데 사용하는 데이터 제어 언어이다.

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/KJY/%5BDATABASE%5D%20SQL%2C%20DDL%2C%20DML%2C%20DCL.md
