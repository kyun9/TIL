# Lombok 세팅(Maven설명)

* c/user/{유저네임}/.m2/repository

  *  메이븐이 관리하는 라이브러리들(특정하게 pom.xml에 기준이 되면 다운이 되는 폴더임)
  * pom.xml에 <groupId>태그안에 경로에 저장되어있어
  * 여기서 lombok 경로(org.projectlombok)로 들어가서 최신.jar파일 실행후(java -jar 최신.jar) 경로는 eclipse.exe로 실행후 이클립스 재시작

* lombok

  * ```java
    package com.cos.blog.test;
    
    import lombok.AllArgsConstructor;
    import lombok.Data;
    import lombok.NoArgsConstructor;
    import lombok.RequiredArgsConstructor;
    
    //@Getter
    //@Setter
    @Data
    @AllArgsConstructor // 전체 생성자
    @NoArgsConstructor // 빈생성자
    public class Member {
    	private int id;
    	private String username;
    	private String password;
    	private String email;
    }
    
    
    //요새 쓰는 방법 - final
    //원래 데이터베이스에 있는 값을 가져와서 집어 넣기 때문에
    // final 불변성 문제 해결하기 위해서
    
    @Data
    @RequiredArgsConstructor //final붙은 얘들에 대한 생성자를 만들어준다.
    public class Member {
    	private final int id;
    	private final String username;
    	private  String password;   //만일 변경해야되면 final을 안붙임
    	private final String email;
    }
    
    @Data
    @NoArgsConstructor // 빈생성자
    public class Member {
    	private int id;
    	private String username;
    	private String password;
    	private String email;
        
    	/*
    	 * Member m = new Member(1, "ssar", "1234", "email");에서
    	 * Member m = new Member("ssar", "1234", "email"); 이렇게 쓸려면 override를 해야돼
    	 * 하지만 @Builder를 사용하면 
    	 * Member m = Member.builder().username("ssar").password("1234").email("ssar@nate.com").build()로
    	 * 자유롭게 생성자를 구현할 수 있다.
    	 * */
    	@Builder 
    	public Member(int id, String username, String password, String email) {
    		this.id=id;
    		this.username= username;
    		this.password = password;
    		this.email= email;
    	}
    }
    ```

* 그럼 바로 Controller에서 getter/setter/생성자 사용할 수 있음

* Lombok을 사용하면 Builder라는 어노테이션 하나로 빌더패턴을 만들어준다!!! 

  * 생성자의 파라미터의 순서를 안지켜도된다.

  * ### 짱 편하다!