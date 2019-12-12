## Index

책에서 원하는 내용을 빨리 찾으려면 인덱스를 이용

Database 에서도 사용자가 원하는 내용을 빨리 찾으려면 색인이라는 정보를 미리 만들어서 원하는 데이터를 빨리 찾을 수 있게한다.

Data base의 고급 퍼포먼스 성능 튜닝과 관련된 작업으로 데이터베이스내의 테이블에서 원하는 정보를 좀 더 빨리 찾아줄 수 있게 데이터의 위치 정보를 보아놓은 데이터베이스 내의 객체(Object)이다.

Data Base의 전반적인 성능의 핵심, 반드시 알아야 할 기술이다.

보통 WHERE 절에 비교대상으로 사용되는 칼럼에 Index가 사용된다.

> 포인트 쿼리 Point Query

조회되는 데이터가 한 두개

    SELECT * FROM MEMBER WHERE ID = 'TEST' --조회 값이 하나

> 범위 쿼리 Range Query

조회되는 데이터가 다수

    SELECT * FROM MEMBER WHERE REGDATE = '2019/12/12' -- 조회 값이 다수

> 커버드 쿼리 Covered Query

조회의 대상과 조회의 결과가 컬럼이 일치하는 상태

    SELECT * FROM MEMBER WHERE ID = 'TEST' AND PW = '1234' -- 커버드 쿼리 OR 포인트 쿼리
    
    SELECT ID FROM MEMBE WHERE ID ='TEST' AND PW = '1234' -- 커버드 쿼리

---

## 클러스터 인덱스 Clustered Index

해당 key 값을 기반으로 테이블이나 뷰의 데이터 행을 정렬하고 저장

해당 키를 기준으로 물리적으로  정렬됨

MS-SQL 에서 PK로 지정된 컬럼에 대해 Clustered Index로 자동 생성한다.

영어사전과 같은 책 - 페이지를 알기 때문에 바로 그 페이지를 펴는것

필요한 경우

우리들 데이터 테이블에서는 PK가 없으므로 Clustered 형 index를 별도로 생성하기에는 힘들어보인다.

테이블당 최대 1개

클러스터형 인덱스 만들기

Transact-SQL 사용

    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO

[참고](https://docs.microsoft.com/ko-kr/sql/relational-databases/indexes/create-clustered-indexes?view=sql-server-2016#Restrictions](https://docs.microsoft.com/ko-kr/sql/relational-databases/indexes/create-clustered-indexes?view=sql-server-2016#Restrictions)) (SQL Server Management Studio 사용법 등)

---

## 비클러스터 인덱스 Non-Clustered Index

비 클러스터형 인덱스 키 값이 있고 각 키 값 항목에는 해당 키 값이 포함된 데이터 행에 대한 포인터가 있다.

인덱스 페이지를 따로 만든다. 용량을 더 차지한다. 기존테이블 + 넌클러스트 인덱스테이블

B-Tree Index ?

그냥 찾아보기가 있는 일반 책 - 목차에서 찾고자하는 내용의 페이지를 찾고 그 페이지로 이동하는것과 같음

쿼리의 조건자 및 조인 조건에서 자주 사용되는 열에 비클러스터형 인덱스를 만든다.

테이블당 249개

비클러스터형 인덱스 만들기

Transact-SQL 사용

    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named IX_ProductVendor_VendorID and delete it if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
                WHERE name = N'IX_ProductVendor_VendorID')   
        DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;   
    GO  
    -- Create a nonclustered index called IX_ProductVendor_VendorID   
    -- on the Purchasing.ProductVendor table using the BusinessEntityID column.   
    CREATE NONCLUSTERED INDEX IX_ProductVendor_VendorID   
        ON Purchasing.ProductVendor (BusinessEntityID);   
    GO

[참고](https://docs.microsoft.com/ko-kr/sql/relational-databases/indexes/create-nonclustered-indexes?view=sql-server-2016#TsqlProcedure) (SQL Server Management Studio 사용법 등)