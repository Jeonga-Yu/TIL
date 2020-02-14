# EC2 서버에 프로젝트를 배포해보자

## 8.1 EC2에 프로젝트 Clone 받기

EC2에 깃허브 설치 및 버전확인

    sudo yum install git
    
    git --version

디렉토리 생성 및 생성한 디렉토리로 이동

    mkdir ~/app && mkdir ~/app/step1
    
    cd ~/app/step1

프로젝트 클론해오기, 복사 확인

    git clone 복사한 주소
    
    cd 프로젝트명
    ll

테스트 검증

    ./gradlew test

성공!!! 😭😭😭

~~*사실은 테스트 에러터져서 수정하고 왔다*~~

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0775c2d2-e5da-4450-8470-5c7567ac5fa2/_2020-02-13__9.58.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0775c2d2-e5da-4450-8470-5c7567ac5fa2/_2020-02-13__9.58.05.png)

## 8.2 배포 스크립트 만들기

작성한 코드를 실제 서버에 반영하는 것을 배포라고 한다.

- git clone 혹은 git pull을 통해 새 버전의 프로젝트 받음
- Gradle 이나 Maven을 통해 프로젝트 테스트와 빌드
- EC2 서버에서 해당 프로젝트 실행 및 재실행

*배포할 때마다 개발자가 하나하나 명령어를 실행하는 것은 불편*

*→ 쉘 스크립트로 작성해 스크립트만 실행하면 앞의 과정이 차례로 진행되도록 해보자*

### 쉘스크립트 란?

.sh라는 파일 확장자를 가진 파일이다. 리눅스에서 기본적으로 사용할 수 있는 스크립트 파일의 한 종류이다

### 빔 이란?

리눅스 환경과 같이 GUI가 아닌 환경에서 사용할 수 있는 편집도구

리눅스에서는 빔 외에 이맥스, 나노 등의 도구도 지원하지만 빔이 가장 대중적인 도구이다. 

빔은 빔만의 사용법이 있다.

쉘에서는 타입 없이 선언하여 저장한다.

쉘에서는 $변수명으로 변수를 사용할 수 있다.

파일생성

    vim ~/app/step1/deploy.sh

    #!/bin/bash
    
    REPOSITORY=/home/ec2-user/app/step1
    PROJECT_NAME=springboot-webservice
    
    cd $REPOSITORY/$PROJECT_NAME/
    
    echo "> Git Pull"
    
    git pull
    
    echo "> 프로젝트 Build 시작"
    
    ./gradlew build
    
    echo "> step1 디렉토리로 이동"
    
    cd $REPOSITORY
    
    echo "> Build 파일 복사"
    
    cp $REPOSITORY/$PROJECT_NAME/build/libs/*.jar $REPOSITORY/
    
    echo "> 현재 구동중인 애플리케이션 pid 확인"
    
    CURRENT_PID=$(pgrep -f ${PROJECT_NAME}*.jar)
    
    echo "현재 구동중인 애플리케이션 pid : $CURRENT_PID"
    
    if [ -z "$CURRENT_PID" ]; then
            echo "> 현재 구동중인 애플리케이션 pid: $CURRENT_PID"
    
    else
            echo "> kill -15 $CURRENT_PID"
            kill -15 $CURRENT_PID
            sleep 5
    fi
    
    echo "> 새 애플리케이션 배포"
    
    JAR_NAME=$(ls -tr $REPOSITORY/ | grep *.jar | tail -n 1)
    
    echo "> JAR Name: $JAR_NAME"
    
    nohup java -jar $REPOSITORY/$JAR_NAME 2>&1 &

실행 권한 추가

    chmod +x ./deploy.sh

스크립트 실행

    ./deploy.sh

## 8.3 외부 Security 파일 등록하기

ClientRegistrationRepository를 생성하려면 clientId와 clientSecret가 필수이다.

로컬에서는 application-oath.properties가 있어 문제가 없었으나 공개 저장소에 clientId와 Secret은 올릴수 없으므로 서버에서 직접 이 설정을 가지고 있게 한다.

## 8.4 스프링 부트 프로젝트로 RDS 접근하기

### RDS 테이블 생성

    create table posts (
    	id bigint not null auto_increment,
    	created_date datetime,
    	modified_date datetime,
    	author varchar(255),
    	content TEXT not null,
    	title varchar(500) not null,
    	primary key (id)
    ) engine=InnoDB;
    
    create table user (
    	id bigint not null auto_increment,
    	created_date datetime,
    	modified_date datetime,
    	email varchar(255) not null,
    	name varchar(255) not null,
    	picture varchar(255),
    	role varchar(255) not null,
    	primary key (id)
    ) engine=InnoDB;
    
    CREATE TABLE SPRING_SESSION (
    	PRIMARY_ID CHAR(36) NOT NULL,
    	SESSION_ID CHAR(36) NOT NULL,
    	CREATION_TIME BIGINT NOT NULL,
    	LAST_ACCESS_TIME BIGINT NOT NULL,
    	MAX_INACTIVE_INTERVAL INT NOT NULL,
    	EXPIRY_TIME BIGINT NOT NULL,
    	PRINCIPAL_NAME VARCHAR(100),
    	CONSTRAINT SPRING_SESSION_PK PRIMARY KEY (PRIMARY_ID)
    ) ENGINE=InnoDB ROW_FORMAT=DYNAMIC;
    
    CREATE UNIQUE INDEX SPRING_SESSION_IX1 ON SPRING_SESSION (SESSION_ID);
    CREATE INDEX SPRING_SESSION_IX2 ON SPRING_SESSION (EXPIRY_TIME);
    CREATE INDEX SPRING_SESSION_IX3 ON SPRING_SESSION (PRINCIPAL_NAME);
    
    CREATE TABLE SPRING_SESSION_ATTRIBUTES (
    	SESSION_PRIMARY_ID CHAR(36) NOT NULL,
    	ATTRIBUTE_NAME VARCHAR(200) NOT NULL,
    	ATTRIBUTE_BYTES BLOB NOT NULL,
    	CONSTRAINT SPRING_SESSION_ATTRIBUTES_PK PRIMARY KEY (SESSION_PRIMARY_ID, ATTRIBUTE_NAME),
    	CONSTRAINT SPRING_SESSION_ATTRIBUTES_FK FOREIGN KEY (SESSION_PRIMARY_ID) REFERENCES SPRING_SESSION(PRIMARY_ID) ON DELETE CASCADE
    ) ENGINE=InnoDB ROW_FORMAT=DYNAMIC;
