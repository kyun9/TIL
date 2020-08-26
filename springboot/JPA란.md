# JPA이란?

* ### JPA는 Java Persistence API이다

  * 영속성(persistence)은 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지않는 데이터의 특성을 의마한다.
  * RAM은 휘발성 데이터를 저장해(컴퓨터 꺼지면 데이터 사라져) -> 하드디스크(파일시스템 = 비휘발성)에 저장해서 영구적으로 저장함
  * 자바에서는 DBMS(하드디스크의 일정부분을 잘라서 사용함)으로 관리를 하고 기록해
    * JPA는 자바에 데이터를 영구히 기록할수 있는 환경을 제공하는 API라는 것
    * JPA는
      *  자바프로그램을 할때 영구적으로 데이터를 저장하기 위해 필요한 인터페이스가 JPA이다.
    * API란? Application programming Interface
      * Application -> 프로그램을 의미
      * programming -> 프로그래밍
      * Interface -> 인터페이스   
        * 인터페이스를 통해서 프로그래밍을 하고 프로그래밍을하면 프로그램이 만들어짐
      * 프로토콜 : 약속 -> 권리가 동등하다. ex) www
      * 인터페이스 : 약속 -> 규칙(프로그램을 만들었어서 다른 사람들과 공유하고 싶어. -> 사용을 원하면 내가 정해놓은 규칙을 지켜)  ==> 즉 인터페이스를 통해서 프로그램을 짜면 그것이 API이다. 상하관계가 존재합니다.  

* ### JPA는 ORM 기술이다

  * ORM(Object Relational Mapping)
  * 오브젝트를 데이터베이스에 연결하는 방법론 같은거
  * 모델링 = 추상적인 개념을 현실세계에 뽑아내는것을 의미
  * DML : 데이터베이스에서 집어 넣을때  Input(DELETE, UPDATE, INSERT), 가져올때 output(SELECT)
  * 자바에서의 데이터 타입과 데이터베이스의 데이터타입이 다르다(그래서 데이터베이스에 있는 테이블을 ``모델링``해야한다. class로) => (테이블을 통한 relational mapping(TRM))
    * 이걸 역으로 바꿔버림!
    * 클래스를 만들면 데이터베이스의 테이블을 자동생성할수 있음
      * 이때 필요한것이 JPA가 가지고있는 인터페이스이다.  

* ### JPA는 반복적인 CRUD 작업을 생략하게 해준다.

  * select 1건, select All, delete 1건, update 1건, insert 1건  = 굉장히 자주일어나는 반복적인 일(CRUD)
  * 이러할때 1차적으로 자바에서 DB에 connection을 요청 -> DB가 신분확인하고 session을 오픈 -> 연결이됨 자바에서는 connection을 가짐 ->두번째 요청시에는 쿼리를 요청할 수 있음, 쿼리를 통한 data를 자바에 응답함 -> 자바에서 받아서 자바 Object로 변경해서 받음 
  * 즉 위의 경우가 단순한 반복로직임(노가다!!)
  * JPA를 사용하면 줄일수 있음
    * 전송된 쿼리에 응답이 있을때 함수하나로 제공해준다!  
  
* ### JPA는 영속성 컨텍스트를 가지고 있다.

  * 영속성 : 어떤 데이터를 영구적으로 저장하게 해주는 것!
    * 자바에서는  데이터베이스(MySQL)에 저장한다.
  * context(컨텍스트)
    * ex) 난 너의 모든 컨텍스트를 가지고있어(난 너의 모든것을 다 알고 있어) ---> 즉 모든 정보를 가지고있는 것을 의미(어떤 대상의 컨텍스트(모든 정보)) 
  * 영속성 컨텍스트 :  데이터를 영구적으로 저장해야하는 컨텍스트를 가지고있다.
  * 즉 자바가 데이터베이스에 저장하고 데이터를 가지고올때의 모든 정보를 영속성컨텍스트가 가지고있고 이를 통해서 확인할수 있다.
    * (= 데이터베이스에 값을 저장할 때 direct하게 접근해서 저장하는게 아니라 중간에 영속성 컨텍스트(자바가 데이터베이스에 데이터를 저장해야되는 모든것들 알고 있는 것)를 통해서 데이터베이스에 던진다.-> 그럼 저장이 됨 --> (영속성컨텍스트와 데이터베이스의 데이터가 동기화))
    * select 요청 -> 영속성 컨텍스트에 요청 -> 영속성컨텍스트가 데이터베이스에게 요청 -> 받음 -> 자바Object -> 돌려줌
    * 3개의 데이터는 일치함(자바요청, 영속성컨텍스트, 데이터베이스)

* ### JPA는 DB와 OOP의 불일치성을 해결하기 위한 방법론을 제공한다. (DB는 객체저장 불가능)

  * 데이터베이스의 테이블들의 관계(PK,FK)들은 Integer데이터를 가지지만 Object를 가지는 건 아니야

  * 자바의 관점에서는 객체(Object)로 묶을 수 있어

    ```java
    class Team{
    	int id;
    	String name;
    	String year;
    }
    
    class Player{
    	int id;
    	String name;
    	Team team;	//select안하고 이렇게 표현할수 있어
        //Object로 만든거임(진정한 OOP(객체지향)를 이용할 수 있음.)
    }
    //즉 ORM을 하면 모델을 만들때 자바가 주도권을 쥐고있는 모델을 만들 수 있다.
    //INSERT,SELECT할 때, JPA가 자동으로 맵핑해서 데이터를 넣어줄거임 
    ```

* ### JPA는 OOP의 관점에서 모델링을 할 수 있게 해준다. (상속, 콤포지션, 연관관계)

  ```java
  class Car extends EntityDate{
      int id;//pk
      String name;
      String color;
      Engine engine;	//fk
  }	
  class Engine extends EntityDate{
      int id;//pk
      int power;
  }
  class EntityDate{
      TimeStamp createDate;
      TimeStamp updateDate;
  }
  
  //테이블 자동생성 
  // Car(id, name, color, engineId, createDate, updateDate)
  //	Engine(id, power, createDate, updateDate)
  ```

  * OOP관점에서 테이블이 생성됨

* ### 방언 처리가 용이하여 Migration 하기 좋음. 유지보수에도 좋음

  * 스프링 -> JPA -> DB
    * JPA는 수많은 방언들(dialect=oracle, mysql, mssql....)을 지원해줌 
    * JPA 추상화 객체를 두고 원하는 DB를 연결하면 바뀜(용이하다. SQL자유로움)







## 참고

https://www.youtube.com/playlist?list=PL93mKxaRDidG_OIfRQ4nztPQ13y74lCYg   4 ~ 7강