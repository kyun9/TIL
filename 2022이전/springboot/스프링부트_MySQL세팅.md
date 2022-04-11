# Spring Boot MySQL 세팅

* #### 사용자 생성 및 권한 주기 및 DB 생성

  ```sql
  -- 사용자 생성 및 권한 주기 및 DB 생성
  -- 유저이름@아이피주소
  create user 'root'@'%' identified by 'root';
  -- ON DB이름.테이블명
  -- TO 유저이름@아이피주소
  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
  CREATE DATABASE blog CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
  use blog;
  
  
  -- my.ini파일 한글설정
  -- MySQL 재시작
  
  -- utf8세팅확인
  show variables like 'c%';
  ```

* #### my.ini 해당부분 한글설정

  ```sql
  
  [client]
  default-character-set=utf8
  
  [mysql]
  default-character-set=utf8
  
  [mysqld]
  collation-server = utf8_unicode_ci
  init-connect='SET NAMES utf8'
  init_connect='SET collation_connection = utf8_general_ci'
  character-set-server=utf8
  ```

* #### MySQL 프로젝트 연결

  > src/main/resources/application.yml

  ```yml
  // pom.xml --> JPA, MySQL dependency 주입
  spring:
    datasource:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/blog?serverTimezone=Asia/Seoul
      username: root
      password: root
  ```

  

### yml 파일

> * json과 비슷한 데이터형식을 가지고있음
>
> * 파일의 형식이 json처럼 생김

* 모든 스프링에 대한 설정할 수 있음
  * 예전 xml이면 boot는 yml파일에 설정
  * root-context.xml, web.xml, servlet-context.xml ==> application.yml에 설정
* properties를 사용하지않는 이유는?
  * 적었던걸 또 적어야함 
  * yml은 들여쓰기할 수 있음(편함) 





#### 참고

https://www.youtube.com/playlist?list=PL93mKxaRDidECgjOBjPgI3Dyo8ka6Ilqm