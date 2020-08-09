### VO와 DTO의 차이

- DTO(Data Transfer Object)
  - 계층간 데이터 교환을 위한 객체(Java Beans)
  - DB에서 데이터를 얻어 Service나 Controller 보낼 때 사용됨
  - getter/setter 메서드만 가짐
- VO(Value Object)
  - DTO와 동일 개념이지만 read only 속성을 가짐
  - VO는 특정한 비즈니스 값을 담는 객체이고, DTO는 Layer간의 통신 용도로 오고가는 객체
