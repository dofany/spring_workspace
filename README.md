# PlanE WEB 환경구축 및 설정

## 목차

- [httpd 설치](#httpd-설치)
- [방화벽 개방](#방화벽-개방)
- [오라클 클라우드의 수신규칙 추가](#오라클-클라우드의-수신규칙-추가)
- [모든 프로토콜의 규칙 추가](#모든-프로토콜의-규칙-추가)
- [방화벽을 해제한 포트번호 추가](#방화벽을-해제한-포트번호-추가)
- [http 방화벽 서비스 추가](#http-방화벽-서비스-추가)
- [https 방화벽 서비스 추가](#https-방화벽-서비스-추가)
- [방화벽 서비스 재시작](#방화벽-서비스-재시작)
- [아파치 시스템 기동 및 상태 체크](#아파치-시스템-기동-및-상태-체크)
- [IP를 입력 후 페이지 확인](#IP를-입력-후-페이지-확인)

## WEB

  - ### Apache 

## WEB 환경세팅

- ### httpd 설치

  <img width="1439" alt="httpd 설치" src="https://user-images.githubusercontent.com/51348720/202945040-87480059-1e2c-4070-94fa-6e775d5dcbe7.png">

  + #### httpd(Http Deamon): 웹 서버의 백그라운드에서 실행되어 들어오는 서버 요청을 대기하는 소프트웨어 프로그램 

  + #### "yum install -y https" 명령어를 사용

- ### 방화벽 개방

  <img width="663" alt="80포트 방화벽 설정" src="https://user-images.githubusercontent.com/51348720/202945782-69d08dd8-e747-4259-bbdd-8057520936d9.png">

  + #### "firewall-cmd --zone=public --add-port=80/tcp --permanent" 명령어를 사용하여 80포트 개방

  + #### /etc/httpd/conf/httpd.conf (혹은 설치 경로에 있는 httpd.conf파일)에서 port를 별도로 지정해주지 않으면 80포트에서 apache가 시작된다.

- ### 오라클 클라우드의 수신규칙 추가

  <img width="1420" alt="수신규칙 추가" src="https://user-images.githubusercontent.com/51348720/201603706-76b34a0c-14ff-4fbd-9c58-71c7d11b594c.png">

  + #### 오라클 클라우드의 인스턴스 메뉴 클릭

  + #### 해당 인스턴스의 "인스턴스 세부정보" 소메뉴의 "가상 클라우드 네트워크" 클릭

  + #### "루트 구획 내 서브넷"의 생성되어있는 서브넷 이름 클릭

  + #### "보안목록"의 생성되어있는 보안목록 이름 클릭

  + #### "수신 규칙 추가" 클릭

- ### 모든 프로토콜의 규칙 추가

  <img width="916" alt="수신규칙 추가2" src="https://user-images.githubusercontent.com/51348720/201604611-db3da3f4-693e-46f8-b689-bdf5ba02fd12.png">

- ### 방화벽을 해제한 포트번호 추가

  <img width="950" alt="수신규칙 추가" src="https://user-images.githubusercontent.com/51348720/202965069-61be3df3-6a5a-47ad-81f9-9e201e6259cb.png">

  + #### 설정 및 방화벽을 개방한 해당 WEB 서버의 포트번호 규칙 추가

- ### http 방화벽 서비스 추가

  <img width="663" alt="http 방화벽 서비스 추가" src="https://user-images.githubusercontent.com/51348720/202945976-ac049092-d59e-4c62-ace9-6a2dd0b49bec.png">

  + #### "firewall-cmd --permanent --add-service=http" 명령어를 사용

- ### https 방화벽 서비스 추가

  <img width="663" alt="https 방화벽 서비스 추가" src="https://user-images.githubusercontent.com/51348720/202946061-dce18754-02e3-468e-90d4-1ff93dbd188f.png">

  + ####  "firewall-cmd --permanent --add-service=https" 명령어를 사용

- ### 방화벽 서비스 재시작

  <img width="663" alt="방화벽 서비스 재시작" src="https://user-images.githubusercontent.com/51348720/202946196-e663543c-462a-4190-8e4a-bc14434ea824.png">

  + #### "firewall-cmd --reload" 방화벽 서비스 재시작

- ### 아파치 시스템 기동 및 상태 체크

  <img width="759" alt="아파치 시작 및 체크" src="https://user-images.githubusercontent.com/51348720/202965228-797b72b6-e3b5-42dc-98e2-46d39b10add5.png">

  + #### "systemctl start https" 명령어를 사용하여 아파치 서비스 기동

  + #### "systemctl status httpd" 명령어를 사용하여 아파치 서비스 상태 체크

- ### IP를 입력 후 페이지 확인

  <img width="1440" alt="아파치 접속" src="https://user-images.githubusercontent.com/51348720/202965435-bffc5d11-3f1b-4c06-b764-05ca28f04a7d.png">

  + #### "146.56.135.125"  => 웹 페이지 URL에 web 서버의 ip주소 입력
