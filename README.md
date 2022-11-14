# PlanE DB 환경구축 및 설정

## 목차
- [yum의 repository 설치](#yum의-repository-설치)
- [MySQL 서버 설치](#MySQL-서버-설치)
- [MySQL 서버 자동으로 시작하도록 설정](#MySQL-서버-자동으로-시작하도록-설정)
- [Mysql server 재시작](#Mysql-server-재시작)
- [MySQL root 계정 임시 비밀번호 찾기](#MySQL-root-계정-임시-비밀번호-찾기)
- [MySQL 접속](#MySQL-접속)
- [최초 비밀번호 설정](#최초-비밀번호-설정)
- [사용자 생성](#사용자-생성)
- [모든 DB 및 테이블에 관한 접근 권한을 부여](#모든-DB-및-테이블에-관한-접근-권한을-부여)
- [설정한 권한 적용](#설정한-권한-적용)
- [방화벽 3306포트(mysql default포트) 개방](#방화벽-3306포트(mysql-default포트)-개방)
- [오라클 클라우드의 수신규칙 추가](#오라클-클라우드의-수신규칙-추가)
- [모든 프로토콜의 규칙 추가](#모든-프로토콜의-규칙-추가)
- [방화벽을 해제한 포트번호 추가](#방화벽을-해제한-포트번호-추가)
- [MySQL 방화벽 서비스 추가](#MySQL-방화벽-서비스-추가)
- [방화벽 서비스 재시작](#방화벽-서비스-재시작)
- [DBeaver 툴에서 MySQL 사용](#DBeaver-툴에서-MySQL-사용)
- [Test Connection](#Test-Connection)
- [연결에 실패할 경우](#연결에-실패할-경우)

## DB
  - ### MySQL 8.ver 

## DB 환경세팅
- ### yum의 repository 설치

<img width="1440" alt="MySQL repository 설치" src="https://user-images.githubusercontent.com/51348720/201600106-f50e0daf-4b53-422e-aff0-88d7c43b3fe2.png">

  + #### "yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm" 명령어를 사용

- ### MySQL 서버 설치

<img width="1440" alt="MySQL 서버 설치" src="https://user-images.githubusercontent.com/51348720/201600766-463daf0a-2c1e-4adb-9c12-d666c63c0564.png">

  + #### "yum install -y mysql-server" 명령어를 사용하여 MySQL 서버 설치

- ### MySQL 서버 자동으로 시작하도록 설정

<img width="1420" alt="서버 재기동 시 MySQL 자동 실행 " src="https://user-images.githubusercontent.com/51348720/201601151-3295eea9-1556-4139-959a-a95f6c4d7fcf.png">

  + #### "systemctl enable mysqld" 명령어를 사용하여 서버를 재부팅 할 시에 MySQL 서버 재시작하도록 설정
  
- ### MySQL server 재시작

<img width="1420" alt="설정 후 MySQL 서버 재시작" src="https://user-images.githubusercontent.com/51348720/201601457-c70f4092-1e89-403f-8c28-8907bfa63706.png">
  
  + #### 설정 완료 후 "systemctl restart mysqld" 명령어를 사용하여 mysql 서버 재시작
  
- ### MySQL root 계정 임시 비밀번호 찾기

<img width="1420" alt="MySQL Root 계정 임시 비밀번호 찾기" src="https://user-images.githubusercontent.com/51348720/201601865-fe9fff88-54b6-414f-881f-c2034ecc3832.png">

  + #### 초기 root계정으로 접속하기 위해선 "grep "temporary password" /var/log/mysqld.log" 명령어를 사용 한 뒤 복사하여 접속 

- ### MySQL 접속

<img width="1420" alt="MySQL Root 접속" src="https://user-images.githubusercontent.com/51348720/201602235-15d3c50c-ce10-4028-86b9-ebf11868a4f1.png">

  + #### 사용자 생성 및 root계정의 비밀번호 변경을 위하여 우선적으로 "mysql -u root -p" 명령어를 사용하여 mysql 접속

- ### 최초 비밀번호 설정

<img width="1420" alt="Root 계정 비밀번호 변경(대문자 한자리 필수)" src="https://user-images.githubusercontent.com/51348720/201602630-e3d80e96-2a7e-42e0-8501-ccd192f5c9e8.png">

  + #### alter user 'root'@'localhost' identified by '변경할 비밀번호';
  + #### ex) New1234!
  + 대소문자 및 특수문자 조합이 필수로 들어가야함

- ### 사용자 생성

<img width="1420" alt="사용자 생성" src="https://user-images.githubusercontent.com/51348720/201602859-ace819ea-19ad-41ee-abc8-e62ece893700.png">

  + #### create user dbadmin@'%' identified by '변경 비밀번호';
  + #### 마찬가지로 대소문자 및 특수문자 조합 필수

- ### 모든 DB 및 테이블에 관한 접근 권한을 부여

<img width="1420" alt="생성한 사용자에게 권한 부여" src="https://user-images.githubusercontent.com/51348720/201603057-becbfc0b-2823-492d-ba4a-1262deea2a05.png">

  + #### "GRANT ALL PRIVILEGES ON \*.\* TO '유저명'@'%';" 명령어 사용
  + #### 우선적으로 모든 권한을 부여했으나 다른 사용자 생성 시 별도의 권한부여 가능

- ### 설정한 권한 적용
  + #### flush privileges;

- ### 방화벽 3306포트(mysql default포트) 개방

<img width="1420" alt="3306 방화벽 개방" src="https://user-images.githubusercontent.com/51348720/201603505-04512c1a-cf20-456b-bfbf-ecbe3f3a5673.png">

  + #### firewall-cmd --zone=public --add-port=3306/tcp --permanent

- ### 오라클 클라우드의 수신규칙 추가
  
  <img width="1420" alt="수신규칙 추가" src="https://user-images.githubusercontent.com/51348720/201603706-76b34a0c-14ff-4fbd-9c58-71c7d11b594c.png">
  
  + #### 오라클 클라우드의 인스턴스 메뉴 클릭
  + #### 해당 인스턴스의 "인스턴스 세부정보" 소메뉴의 "가상 클라우드 네트워크" 클릭
  + #### "루트 구획 내 서브넷"의 생성되어있는 서브넷 이름 클릭
  + #### "보안목록"의 생성되어있는 보안목록 이름 클릭
  + #### "수신 규칙 추가" 클릭

- ### 모든 프로토콜의 규칙 추가

  <img width="916" alt="수신규칙 추가2" src="https://user-images.githubusercontent.com/51348720/201604611-db3da3f4-693e-46f8-b689-bdf5ba02fd12.png">
 
- ### 방화벽을 해제한 포트번호 추가
  
  <img width="916" alt="수신규칙 추가3" src="https://user-images.githubusercontent.com/51348720/201604985-2dab37ef-01a6-4159-b2a5-8807ccdcbc84.png">

  + #### 설정 및 방화벽을 해제한 해당 DB의 포트번호의 규칙 추가

- ### MySQL 서비스 추가

<img width="1420" alt="MySQL 방화벽 서비스 추가" src="https://user-images.githubusercontent.com/51348720/201605149-edee9c09-1a97-4c43-a8ee-db962edb2fda.png">

  + #### "firewall-cmd --permanent --add-service=mysql" 명령어 사용
  + #### MySQL의 방화벽 서비스 추가

- ### 방화벽 서비스 재시작

<img width="1420" alt="방화벽 설정 후 재시작" src="https://user-images.githubusercontent.com/51348720/201605535-08f58fc7-ef5d-47f8-8542-a2bd568242b9.png">

  + #### "firewall-cmd --reload" 명령어 사용하여 방화벽 서비스

- ### DBeaver 툴에서 MySQL 사용

<img width="917" alt="Dbeaver connect 설정" src="https://user-images.githubusercontent.com/51348720/201606268-e406f493-1192-4a3f-a577-d37d2817dc7a.png">
  
  + #### 메뉴바에서 데이터베이스 클릭 후 "새 데이터베이스 연결" 클릭
  + #### MySQL 선택 후 다음
  + #### 호스트 및 포트 입력 후 해당 DB의 사용자 명과 비밀번호 입력

- ### Test Connection

<img width="695" alt="connection 테스트" src="https://user-images.githubusercontent.com/51348720/201606918-ee9d9a1a-f4f1-4670-a243-0f30a99e5548.png">

  + #### 왼쪽 하단 부분의 "Test Connection ... " 버튼 클릭
  + #### Connected 팝업이 뜰 시 확인 후 연결

- ### 연결에 실패할 경우

<img width="695" alt="publickey 설정(MySQL 8버전 이후부터)" src="https://user-images.githubusercontent.com/51348720/201607283-9264049e-abb2-4714-87e0-c307fb17fd02.png">

  + #### 연결에 실패할 경우에는 "Driver Properties" 탭 클릭 후 DB Driver 설정
  + #### "allowPublicKeyRetrieval" 선택 후 "True"로 변경
  + #### 재연결 시도
