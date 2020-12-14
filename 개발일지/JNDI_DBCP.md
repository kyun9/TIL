### JNDI, DBCP

1. 사용자가 요청을 한다.
2. 요청은 Control을 거쳐 Model로 전달된다.
3. Model로 넘어간 요청은 JNDI에 등록된 데이터베이스 객체(type : DataSource)를 검색한다.
4. JNDI를 통해 찾은 객체로부터 커넥션을 획득한다.
5. 데이터베이스 작업이 끝난후, 획득한 커넥션을 반납한다.

![img](https://t1.daumcdn.net/cfile/tistory/224CD845582D373205)



### 참고

JNDI와 DBCP를 이용한 DB연동하는 방법 : https://all-record.tistory.com/104