### CREATE TABLE
    CREATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( [COLUMN1] VARCHAR(50), [COLUMN2] VARCHAR(5) )

### 테이블 칼럼 수정
    ALTER TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ALTER COLUMN [COLUMNNAME] NVARCHAR(MAX)

### ROW_NUMBER()
    SELECT [NO] = ROW_NUMBER() OVER(ORDER BY (SELECT NULL))

### Truncate Table
테이블의 모든 행을 제거한다. 기능상으로 WHERE 절이 없는 DELETE 문과 동일하지만 더 빠르고 시스템 및 트랜잭션 로그 리소스를 덜 사용한다.

    TRUNCATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }

### SELECT 결과를 새 테이블에 INSERT 하기
      SELECT * INTO { database_name.schema_name.table_name | schema_name.table_name | table_name }
      FROM { database_name.schema_name.table_name | schema_name.table_name | table_name }

### SELECT 결과를 기존 테이블에 INSERT 하기
    INSERT INTO { database_name.schema_name.table_name | schema_name.table_name | table_name }
    SELECT {* | Columns } FROM { database_name.schema_name.table_name | schema_name.table_name | table_name }
    WHERE 1=1

### DBCC SHRINKDATABASE
지정한 데이터베이스에 있는 데이터 및 로그 파일의 크기를 축소한다.

    DBCC SHRINKDATABASE (TCO_SYSTEMCOMPLETION, 0);

### oepnrowset으로 엑셀 읽어오기
> OEPNROWSET에서는 표현식을 사용할 수 없다.
    SELECT * INTO #TEMP_TABLE FROM OPENROWSET (
    'MICROSOFT.ACE.OLEDB.12.0', 'EXCEL 12.0;DATABASE=e:\dir\file.xlsx;hdr=yes;imex=1;','SELECT * FROM [DB$]'
    )

### Convert 날짜형 변환
    [TEST_DATE] = CONVERT(NVARCHAR(10), [DATE_COLUMN], 101)
    > 11/15/19
    
### Schema CREATE
    CREATE SCHEMA [schema_name]
    
### Schema ALTER
    ALTER SCHEMA [바꿀 스키마 명] transfer [기존 스키마명].[table_name]
    
### SET ANSI_WARNINGS {ON | OFF}
ON으로 설정할 경우 SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP, COUNT 등의 집계 함수에 NULL 값이 있으면 경고 메시지가 생성된다.
OFF로 설정한 경우에는 경고가 발생하지 않는다..

### Numeric
    Numeric(전체길이, 소수점이하길이)
