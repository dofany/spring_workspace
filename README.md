# PlanE DB 환경구축 및 설정

## 목차
- [yum의 repository 설치](#yum의-repository-설치)
- [MySQL 서버 설치](#MySQL-서버-설치)
- [서버 재부팅 시 MySQL 서버 자동으로 시작하도록 설정](#서버-재부팅-시-MySQL-서버-자동으로-시작하도록-설정)
- [Mysql server 재시작](#Mysql-server-재시작)
- [MySQL root 계정 임시 비밀번호 찾기](#MySQL-root-계정-임시-비밀번호-찾기)
- [MySQL 접속](#MySQL-접속)
- [최초 비밀번호 설정(대소문자 특수문자 조합필요 ex)New1234!)](#최초-비밀번호-설정(대소문자-특수문자-조합필요-ex)New1234!))
- [사용자 생성](#사용자-생성)
- [모든 DB에 및 테이블에 관한 접근 권한을 부여](#모든-DB에-및-테이블에-관한-접근-권한을-부여)
- [설정한 권한 적용](#설정한-권한-적용)
- [방화벽 3306포트(mysql default포트) 개방](#방화벽-3306포트(mysql-default포트)-개방)
- [MySQL 방화벽 서비스 추가](#MySQL-방화벽-서비스-추가)
- [방화벽 서비스 재시작](#방화벽-서비스-재시작)

## DB
  - ### MySQL 8.ver 

## DB 환경세팅
<img width="1440" alt="MySQL repository 설치" src="https://user-images.githubusercontent.com/51348720/201600106-f50e0daf-4b53-422e-aff0-88d7c43b3fe2.png">
- ### yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm
  + #### yum의 repository 설치

- ### yum install -y mysql-server
  + #### MySQL 서버 설치

- ### systemctl enable mysqld
  + #### 서버 재부팅 시 MySQL 서버 자동으로 시작하도록 설정
  
- ### systemctl restart mysqld
  + #### mysql server 재시작

- ### grep "temporary password" /var/log/mysqld.log
  + #### MySQL root 계정 임시 비밀번호 찾기

- ### mysql -u 사용자계정명 -p
  + #### MySQL 접속

- ### alter user 'root'@'localhost' identified by '변경할 비밀번호'; 
  + #### 최초 비밀번호 설정(대소문자 특수문자 조합필요 ex)New1234!)

- ### create user dbadmin@'%' identified by '변경 비밀번호';
  + #### 사용자 생성

- ### GRANT ALL PRIVILEGES ON \*.\* TO '유저명'@'%';
  + #### 모든 DB에 및 테이블에 관한 접근 권한을 부여

- #### flush privileges;
  + #### 설정한 권한 적용

- ### firewall-cmd --zone=public --add-port=3306/tcp --permanent
  + #### 방화벽 3306포트(mysql default포트) 개방

- ### firewall-cmd --permanent --add-service=mysql
  + #### MySQL 서비스 추가

- ### firewall-cmd --reload
  + #### 방화벽 서비스 재시작

