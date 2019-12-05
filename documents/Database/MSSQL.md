# 테이블 칼럼 수정
ALTER TABLE [TABLENAME] ALTER COLUMN [COLUMNNAME] NVARCHAR(MAX)

# Truncate Table
테이블의 모든 행을 제거한다. 기능상으로 WHERE 절이 없는 DELETE 문과 동일하지만 더 빠르고 시스템 및 트랜잭션 로그 리소스를 덜 사용한다.
  TRUNCATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }

# SELECT 결과를 새 테이블에 INSERT 하기
  SELECT * INTO { database_name.schema_name.table_name | schema_name.table_name | table_name } FROM { database_name.schema_name.table_name | schema_name.table_name | table_name }

# SELECT 결과를 기존 테이블에 INSERT 하기
  INSERT INTO { database_name.schema_name.table_name | schema_name.table_name | table_name }
  SELECT {* | Columns } FROM { database_name.schema_name.table_name | schema_name.table_name | table_name } WHERE 1=1

# DBCC SHRINKDATABASE
지정한 데이터베이스에 있는 데이터 및 로그 파일의 크기를 축소한다.

    DBCC SHRINKDATABASE (TCO_SYSTEMCOMPLETION, 0);

# Issue
- OEPNROWSET에서는 표현식을 사용할 수 없다.