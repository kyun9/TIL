# HTTP요청2_(요청시에 데이터 실어보내기) 

* 객체 지향에서 변수는 private를 만든다. 변수의 상태는 메소드에서 변경이 되게 설계를 해야된다.

* GET방식 

  * @RequestParam
    *  ```쿼리스트링 문자열``` 받기  
    * 파라미터 하나하나씩 받기

* POST방식, PUT방식, DELETE방식

  * ```BODY```에 담아서 보내기

    * 방법이 많음!! 대표적인 2가지방식만

      * x-www-form-urlencoded 방식

        * HTML에서 FORM태그를 만들어서 보낼때 <input type="">

      * raw 방식

        * @RequestBody의 어노테이션에서 raw에 입력한 데이터를 그대로 받는다.

        * raw의 의미는 가장 기본적인 것을 보냈다는것 (text/plain을 의미한다)

        * (application/json) MIME타입 데이터를 보내고싶다면 {  "id" : 1, "username": "hyun" .... } json형식으로 보낸다.

          ```java
          @PostMapping("/http/post")
          	public String postTest(@RequestBody Member m) {
          //		return "post 요청 : "+text;
          		return "post 요청: "+ m.getId()+" "+ m.getUsername()+" "+ m.getPassword()+ " "+ m.getEmail();
          	}
          ```

          * json을 Member객체에 그대로 매핑해서 보낸준다.

* 객체(오브젝트)로 넣으면 객체로 받아버린다.

  ```java
  	@GetMapping("/http/get")
  	public String getTest(Member m) {
  		return "get 요청: "+ m.getId()+" "+ m.getUsername()+" "+ m.getPassword()+ " "+ m.getEmail();
  	}
  ```

  * m객체의 멤버변수에 값을 안넣으면 null이 들어간다.

  

