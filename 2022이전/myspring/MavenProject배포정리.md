### Maven Project 배포 정리 

- 메이븐은 자바소스파일(war 또는 jar파일)을 빌드(build), 라이브러리 의존성(dependency), 컴파일(compile), 배포(deploy)를 해결해주는 도구
  - 즉) 자바용 프로젝트 관리도구
- pom.xml구성
  - <property> : pom.xml내의 dependency환경 설정을 위한 변수를 세팅
  - <dependency> : 라이브러리들 명시
  - <build>내에 <plugin> : Maven project build를 위한 라이브러리 명시
- WAR와 JAR
  - JAR(Java Archive) :
    -  Application으로 bin내에 있는 .class파일을 패키지로 묶은 것
  - WAR(Web application ARchive) : 
    - Application으로 webapp폴더 아래 있는 파일들이 war로 묶여지는 것
    - WAR파일의 명은 pom.xml에 있는 [artifact id +  version + packaging]으로 정해짐



- WAR파일 배포 시, 폴더 경로

  - 설정) 프로젝트 preference > Deployment Assembly에서 확인가능

  1. src/main/java : java파일들이 컴파일되어 생성된 .class파일은 /WEB-INF/classes폴더 하위에 옮겨져 저장된다.
  2. src/main/resources : xml파일 및 mybatis등의 파일들은 /WEB-INF/classes 폴더 하위에 저장
  3. Maven Dependencies : Maven에 설정한 라이브러리들은 /WEB-INF/libs 폴더 하위에 저장





- 프로젝트 export 할 때, mvn package와 export의 차이

  - mvn package 

    - 컴파일된 결과물을 패키지 파일로 생성

    - 컴파일, 테스트, 빌드를 숭행하여 패키지 파일을 생성한다.

    - 프로젝트 이름, 버전, 패키징 옵션에 맞게 파일이 생성됨

    - pom.xml에서 설정값에 맞게 war파일이 생성

      - artifactId : 프로젝트 이름 

      - version : 버전

      - packaging : 패키징 옵션

        ```xml
        <artifactId>test</artifactId>
        <version>1.0</version>
        <packaging>war</packaging>
        
        // test-1.0.war 파일 생성
        ```

        





