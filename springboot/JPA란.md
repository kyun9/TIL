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





## 참고

https://www.youtube.com/playlist?list=PL93mKxaRDidG_OIfRQ4nztPQ13y74lCYg   4 ~ 5강