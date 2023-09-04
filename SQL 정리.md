# SQL 정리

## DDL(정의어)

### 테이블의 구조나 관계를 생성하는 CREATE, ALTER, DROP, TRUNCATE

> 1. CREATE : 테이블 혹은 데이터베이스를 생성
>    - CREATE TABLE [테이블명];
>    - CREATE INDEX 인덱스명 ON 테이블명(컬럼명);
> 2. ALTER : 데이터베이스의 객체를 변경
>    - column 추가
>      - ALTER TABLE [테이블명] ADD [추가할 column] [데이터타입];
>    - 컬럼 타입 수정
>      - ALTER TABLE [테이블명] MODIFY [변경할 column명] [변경할 타입];
>    - 컬럼명 수정
>      - ALTER TABLE [테이블명] RENAME COLUMN [기존 column명 TO [변경할 > column명];
>    - 컬럼 삭제
>      - ALTER TABLE [테이블명] DROP [삭제할 column명];
> 3. DROP : 테이블이나 데이터베이스 삭제
>    - DROP TABLE [테이블명] (CASCADE | RESTRICT);
>      - CASCADE : 참조하는 테이블까지 다 제거
>      - RESTRICT : 삭제하려는 테이블을 다른 테이블이 참조 중이면 제거하지 않음
> 4. TRUNCATE : 테이블 내의 데이터를 삭제
>    - TRUNCATE TABLE [테이블명];

## DML(조작어)

### 테이블의 데이터 검색, 등록, 수정, 삭제하는 SELECT, INSERT, > > UPDATE, DELETE

> 1. SELECT : 검색
>    - SELECT \_ FROM [테이블명];
> 2. INSERT : 등록
>    - INSERT INTO [테이블명] (컬럼명) VALUES(추가할 정보);
> 3. UPDATE : 수정
>    - UPDATE [테이블명] SET [변경할 컬럼]=[변경할 내용]; + (조건절)
> 4. DELETE : 삭제
>    - DELETE FROM [테이블명]; + (조건절)

## DCL(제어어)

### 데이터베이스의 사용권한을 관리하는 GRANT, REVOKE, COMMIT, >?> > ROLLBACK

> 1. GRANT : 권한 부여
>    - GRANT [권한 종류] ON [대상] TO [계정명] IDENTIFIED BY [암호] [WITH GRANT OPTION];
>    - FLUSH PRIVILEGES;
>    - 모든 권한을 가진 계정
>      - GRANT ALL ON _._ TO bonni@localhost IDENTIFIED BY "AAAA";
>    - 특정 데이터베이스에 조회권한을 가진 계정 생성
>      - GRANT SELECT ON test.\_ TO bonni@localhost IDENTIFIED BY "AAAA";
> 2. REVOKE : 권한 해제
>    - REVOKE insert, update, crate ON [DB명.테이블명] TO [계정명];
>    - 전체 권한 해제
>      - REVOKE ALL ON [DB명.테이블명] TO [계정명];
>      - REVOKE 권한 ON [테이블명] FROM [계정명] (CASCADE CONSTRAINTS);
>      - CASCADE CONSTRAINTS : 옵션으로 부여된 사용자들의 권한까지 취소
> 3. COMMIT : 작업 완료
>    - COMMIT;
> 4. ROLLBACK : 작업 내용 복구
>    - ROLLBACK;
>    - COMMIT 하기 이전의 상태만 ROLLBACK 가능. COMMIT 후에는 불가능

### DROP, DELETE, TRUNCATE 차이점

> - DELETE → 데이터만 지우고 테이블 용량이 줄어들지 않음. 삭제 후 되돌릴 수 있음
> - TRUNCATE → 테이블 용량 줄어들고 인덱스 등 모두 삭제됨. 테이블은 삭제하지 않고 데이터만 삭제하며 삭제 후에 되돌릴 수 없음
> - DROP → 테이블 전체를 삭제하며 삭제 후 되돌릴 수 없음
