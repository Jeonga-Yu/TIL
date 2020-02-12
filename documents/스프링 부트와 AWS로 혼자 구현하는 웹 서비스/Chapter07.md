# AWS에 데이터베이스 환경을 만들어보자 - AWS RDS

웹 서비스의 백엔드를 다룬다고 했을 때 애플리케이션 코드를 작성하는 것 만큼 중요한 것이 데이터베이스를 다루는 일이다. 규모있는 회사에서는 데이터베이스를 전문적으로 처리하는 DBA 직군 담당자가 있지만 백엔드 개발자가 데이터베이스를 몰라도 된다를 의미하지는 않는다. 스타트업이나 개발 인원수가 적은 서비스에서는 개발자가 데이터베이스를 다뤄야만한다.

## RDS(Relational Database Service)

모니터링, 알람, 백업, HA구성 등 처음 구축할 때 며칠이 걸릴 수 있는 작업을 모두 지원하는 관리형 서비스인 RDS를 AWS에서 제공한다. 운영 작업을 자동화하여 개발자가 개발에 집중할 수 있게 지원해주는 서비스다.

## 7.1 RDS인스턴스 생성

### MariaDB 선택이유

- 가격
- Amazone Aurora(오로라) 교체 용이성
- MySQL의 창시자인 몬티 와이드니어가 만든 프로젝트
- MySQL기반으로 만들어졌기 때문에 전반적인 사용법이 유사하다
- 동일 하드웨어 사양으로 MySQL보다 향상된 성능

## 7.2 RDS 운영환경에 맞는 파라미터 설정하기

- 타임존
- Character Set

    utf8mb4는 이모지를 저장할 수 있다

- Max Connection

## 7.3 내 PC에서 RDS접속해보기

### 데이터베이스 선택

    use mydbinstance;

### 현재 character_set, collation 설정 확인

    show variables like 'c%';

### 파라미터 그룹을 변경이 안된 필드 변경처리

    ALTER DATABASE mydbinstance
    CHARACTER SET = 'utf8mb4'
    COLLATE = 'utf8mb4_general_ci';

### 타임존 확인

    select @@time_zone, now();

### 한글이 잘 들어가는지 간단한 테스트

    create table test (
        id bigint(20) not null auto_increment,
        content varchar(255) default null,
        primary key(id)
        
    ) ENGINE=InnoDB;
    
    insert into test(content) values('테스트');
    
    select * from test;

## 7.4 EC2에서 RDS접근 확인

### mysql 설치(명령어 라인만 쓰기 위한 설치)

    sudo yum install mysql

### RDS 접속

    mysql -u 계정 -p -h Host주소
