##  스프링 DB 접근 기술

>- H2 데이터베이스 설치
>- 순수 JDBC
>- 스프링 통합테스트
>- 스프링 JdbcTemplate
>- JPA
>- 스프링 데이터 JPA

### JPA

- JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
- JPA를 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
- JPA를 사용하면 개발 생산성을 크게 높일 수 있다.



1. **build.gradle 파일에 JPA, h2 데이터베이스 관련 라이브러리 추가**

```java
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    //implementation 'org.springframework.boot:spring-boot-starter-jdbc'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    runtimeOnly 'com.h2database:h2'
    testImplementation('org.springframework.boot:spring-boot-starter-test') {
        exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    }
}
```

`spring-boot-starter-data-jpa` 는 내부에 jdbc 관련 라이브러리를 포함한다. 따라서 jdbc는 제거해도 된다.



2. **스프링 부트에 JPA 설정 추가**

`resources/application.properties`

```java
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none
```

주의!: 스프링부트 2.4부터는 spring.datasource.username=sa 를 꼭 추가해주어야 한다. 그렇지
않으면 오류가 발생한다.

- `show-sql` : JPA가 생성하는 SQL을 출력한다.
- `ddl-auto` : JPA는 테이블을 자동으로 생성하는 기능을 제공하는데 none 를 사용하면 해당 기능을 끈다.
  - `create` 를 사용하면 엔티티 정보를 바탕으로 테이블도 직접 생성해준다. 해보자.



3. **JPA 엔티티 매핑**

```java
package hello.hellospring2.domain;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity  // JPA가 관리하는 엔티티 
public class Member {
	
	@Id @GeneratedValue(strategy = GenerationType.IDENTITY) // id는 pk 시퀀스이다. DB가 알아서 생성해주는게 IDENTITY이다. 
	private Long id;
	
	private String name;

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
}
```



4. **JPA 회원 리포지토리**

```java
package hello.hellospring2.repository;

import java.util.List;
import java.util.Optional;

import javax.persistence.EntityManager;

import hello.hellospring2.domain.Member;

public class JpaMemberRepository implements MemberRepository {
	private final EntityManager em;

	public JpaMemberRepository(EntityManager em) {
		this.em = em;
	}

	public Member save(Member member) {
		em.persist(member);
		return member;
	}

	public Optional<Member> findById(Long id) {
		Member member = em.find(Member.class, id);
		return Optional.ofNullable(member);
	}

	public List<Member> findAll() {
		return em.createQuery("select m from Member m", Member.class).getResultList();
	}

	public Optional<Member> findByName(String name) {
		List<Member> result = em.createQuery("select m from Member m where m.name = :name", Member.class)
				.setParameter("name", name).getResultList();
		return result.stream().findAny();
	}
}
```



4. **서비스 계층에 트랜잭션 추가**

```java
import org.springframework.transaction.annotation.Transactional

@Transactional
public class MemberService {}
```

- `org.springframework.transaction.annotation.Transactional` 를 사용하자.
- 스프링은 해당 클래스의 메서드를 실행할 때 트랜잭션을 시작하고, 메서드가 정상 종료되면 트랜잭션을
  커밋한다. 만약 런타임 예외가 발생하면 롤백한다.
- **JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다.**



5. **JPA를 사용하도록 스프링 설정 변경**

```java
package hello.hellospring;
import hello.hellospring.repository.*;
import hello.hellospring.service.MemberService;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import javax.persistence.EntityManager;
import javax.sql.DataSource;
@Configuration
public class SpringConfig {
private final DataSource dataSource;
 private final EntityManager em;
 public SpringConfig(DataSource dataSource, EntityManager em) {
 this.dataSource = dataSource;
 this.em = em;
 }
 @Bean
 public MemberService memberService() {
 return new MemberService(memberRepository());
 }
 @Bean
 public MemberRepository memberRepository() {
// return new MemoryMemberRepository();
// return new JdbcMemberRepository(dataSource);
// return new JdbcTemplateMemberRepository(dataSource);
 return new JpaMemberRepository(em);
 }
}
```

> 참고: JPA도 스프링 만큼 성숙한 기술이고, 학습해야 할 분량도 방대하다. 다음 강의와 책을 참고하자.
> - 인프런 강의 링크: 인프런 - 자바 ORM 표준 JPA 프로그래밍 - 기본편
> - JPA 책 링크: 자바 ORM 표준 JPA 프로그래밍 - YES24