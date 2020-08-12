# Maven이란

### Maven?

> Maven은 자바 프로젝트의 빌드(build)를 자동화 해주는 빌드 툴(build tool)

* 특징
  * 빌드 절차 간소화
  * 동일한 빌드 시스템 제공
  * 프로젝트 정보 제공
* 차이점
  * ant
    * ant는 비교적 자유도가 높음 (전처리, 컴파일, 패키징, 배포 가능)
    * Maven은 정해진 life cycle에 의하여 작업 수행하며, 전반적인 프로젝트 관리 기능까지 포함하고 있음. (Build Tool + Project Management)
  * gradle
    * XML 대신 groovy 스크립트를 사용하여 동적인 빌드 가능
    * maven은 멀티프로젝트에서 상속구조인데, gradle은 주입 방식임, 멀티 프로젝트에서 gradle이 더 적합



### Maven이 참조하는 설정 파일

> settings.xml, pom.xml 두 개의 설정파일을 알아보면 된다.

* settings.xml

  * maven tool 자체에 관련된 설정을 담당
  * MAVEN_HOME/conf/ 아래 위치 (MAVEN_HOME은 환경병수에 설정된 경로를 의미함)

  

* pom.xml

  * Project Object Model
  * 프로젝트에 최상위 디렉토리에 위치하며 프로젝트에 1개임
  * 프로젝트 내 빌드 옵션을 설정하는 부분 
  *  분석
    1. 프로젝트 정보
    
    2. 의존성 라이브러리 정보
    
    3. build 정보



### pom.xml앨리먼트 태그

* `<groupId>` : 프로젝트의 패키지 명칭

* `<artifactId>` : artifact 이름, groupId 내에서 유일해야 한다.

  ```java
   <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
  ```

* `<version>` : artifact 의 현재버전 ex. 1.0-SNAPSHOT

* `<name>` : 어플리케이션 명칭

* `<packaging>` : 패키징 유형(jar, war 등)

* `<distributionManagement>` : artifact가 배포될 저장소 정보와 설정

* `<parent>` : 프로젝트의 계층 정보

*  `<dependencyManagement>`: 의존성 처리에 대한 기본 설정 영역

* `<dependencies>` : 의존성 정의 영역

*  `<repositories>`: 이거 안쓰면 공식 maven 저장소를 활용하지만, 사용하면 거기 저장소를 사용

* `<build>` : 빌드에 사용할 플러그인 목록을 나열

*  `<reporting>`: 리포팅에 사용할 플러그인 목록을 나열

* `<properties>` : 보기좋게 관리가능, 보통 버전에 많이 쓴다.

  ```java
    <!-- properties 에 이렇게 추가하면 -->
    <spring-version>4.3.3.RELEASE</spring-version>
  
    <!-- dependencies 에 이렇게 쓸수 있다. -->
    <version>${spring-version}</version>
  ```

  









##### 출처

https://sjh836.tistory.com/131

https://jeong-pro.tistory.com/168