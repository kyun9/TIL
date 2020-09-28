# HTTP요청1_(개발자도구로 요청확인하기)

### 어노테이션

* @Controller and @ RestController

  * @Controller
    * 사용자가 요청 --> 응답(HTML 파일)
  * @RestController
    * 사용자가 요청 --> 응답(Data)

* Mapping

  * @GetMapping("/http/get")  == select
    * 인터넷 브라우저 요청은 무조건 get요청밖에 할 수 없다.
  * @PosttMapping("/http/post") == insert
  * @PutMapping("/http/put")  == update
  * @DeleteMapping("/http/delete")  == delete

  > put, delete, post 요청을 확인하는 용도로 **Postman**을 쓴다.

### 개발자 도구 보는법

* Genneral

  * Request URL : 내가 request한 주소
  * Request Method : request한 방식 (GET/POST)
  * State Code :  200(정상), 405(해당 메소드가 허용되지않는다)....

* Response Headers

  > 서버가 나한테 어떻게 response해줬는지

  * Content Type :  (text/html; charset=UTF-8 : 응답을 해줄때 text인데 html text야 인코딩이 utf8뢰 되어있어)

* Request Headers

  > 내가 웹 브라우저를 통해서 서버에 요청할 때의 해더임

  