**캘린더 프로젝트**

> #### 목차
>
> - [목적](#목적)
> - [프로젝트 인원](#프로젝트-인원)
> - [환경구성](#환경구성)
> - [기능요구 사항](#기능-요구사항)

> ### 목적
>
> - **사원들과 스터디의 목적으로 시작한 일정관리 및 채팅기능이 있는 프로젝트**

> ### 프로젝트 인원
>
> - **김형직 과장**
> - **백상열 과장**
> - **김재성 대리**
> - **조원주 대리**
> - **김도환 사원**
> - **김우석 사원**
> - **김준희 사원**
> - **조혜주 사원**

> ### 환경구성
>
> - **VM : Oracle Cloud**
> - **OS : centOS 7**
> - **DB : MySQL ver 8**
>
> > **DB 환경세팅**
> >
> > - **yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-5.noarch.rpm**
> >   + **yum의 repository 설치**
> > - **yum install -y mysql-server**
> >   - **MySQL 서버 설치**
> > - **systemctl enable mysqld**
> >   - **서버 재부팅 시 MySQL 서버 자동으로 시작하도록 설정**
> > - **systemctl restart mysqld**
> >   - **mysql server 재시작**
> > - **grep "temporary password" /var/log/mysqld.log**
> >   - **MySQL root 계정 임시 비밀번호 찾기**
> > - **mysql -u 사용자계정명 -p**
> >   - **MySQL 접속**
> > - **alter user 'root'@'localhost' identified by '변경할 비밀번호'; **
> >   - **최초 비밀번호 설정(대소문자 특수문자 조합필요 ex)New1234! )**
> > - **create user dbadmin@'%' identified by '변경 비밀번호';**
> >   - **사용자 생성**
> > - **GRANT ALL PRIVILEGES ON \*.\* TO '유저명'@'%';**
> >   - **모든 DB에 및 테이블에 관한 접근 권한을 부여**
> > - **flush privileges;**
> >   - **설정한 권한 적용**
> > - **firewall-cmd --zone=public --add-port=3306/tcp --permanent**
> >   - **방화벽 3306포트(mysql default포트) 개방**
> > - **firewall-cmd --permanent --add-service=mysql**
> >   - **MySQL 서비스 추가**
> > - **firewall-cmd --reload**
> >   - **방화벽 서비스 재시작**
>
> - **WEB : Apache**
> - **WAS : JBoss**

> ### 기능 요구사항
>
> > #### 분류
> >
> > - **사용자**
>
> > #### 기능
> >
> > > ##### 회원가입
> > >
> > > - **사용자를 추가할 수 있는 기능**
> >
> > > ##### 로그인
> > >
> > > - **사용자가 로그인을 할 수 있는 기능**
> > > - **사용자가 아이디를 찾을 수 있는 기능**
> >
> > > ##### 로그아웃
> > >
> > > - **사용자가 로그아웃 할 수 있는 기능**
> >
> > > ##### 내 정보
> > >
> > > - **사용자가 프로필을 볼 수 있는 기능**
> > > - **사용자가 프로필을 수정 할 수 있는 기능**
> > > - **사용자가 패스워드를 변경 할 수 있는 기능**
> > > - **사용자의 계정을 탈퇴 할 수 있는 기능**
> >
> > > ##### 친구 또는 그룹 목록
> > >
> > > - **사용자가 추가한 그룹이나 친구의 목록을 확인하는 기능**
> > > - **사용자의 친구 및 그룹 추가 기능**
> > > - **사용자의 친구 및 그룹 삭제 기능**
> >
> > > ##### 즐겨찾기
> > >
> > > - **중요하다고 생각되는 메모의 중요도를 표시 및 해제하는 기능**
> >
> > > ##### 검색
> > >
> > > - **해당 연도 및 월, 내용이 포함된 캘린더 검색 기능**
> > > - **주간별, 월별로 한눈에 보게하는 기능**
> >
> > > ##### 메모
> > >
> > > - **사용자가 선택한 해당 날짜에 메모를 하는 기능**
> > > - **메모 삭제 기능**
> > > - **메모 수정 기능**
> >
> > > ##### 커뮤니티 / 자유게시판
> > >
> > > - **사용자들끼리의 파일 공유를 위한 업로드 기능**
> > > - **사용자들끼리의 소통을 위한 커뮤니티 글 작성 기능**
> > > - **작성된 글에 대한 답변 및 대댓글 기능**
> > > - **작성된 글 및 댓글 삭제 기능**
> >
> > > ##### 미리알림
> > >
> > > - **사용자가 설정한 날짜의 메모를 알려주고, 설정 및 해제 기능**