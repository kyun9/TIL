### Swagger

> * REST API 개발시 문서를 자동으로 만들어주는 프레임워크
>
>   (REST API : 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고 받는 것이며 HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD를 적용하는 것을 의미함.)
>
> * 많은 API관리를 통해 정확한 협업과 소통이 가능하다!

- 간단한 설정으로 프로젝트에 지정한 URL들을 HTML화면으로 확인
- API에 대한 메뉴얼 자동생성
- Postman과 같은 API테스트 가능
- 소스코드 빌드시 문서 자동 생성



#### Swagger 어노테이션

* @Api 

  * 해당 클래스가 Swagger 리소스라는 것을 명시합니다.
  * Controller 단위로 API 메타데이터 명시 (class단위)
    * *value* : 태그를 작성
    * *tags* : 사용하여 여러개의 태그를 정의할 수 있음

* @ApiOperation

  * 한 개의 operation(즉 API URL과 Method)을 선언합니다.
    * *value*  : API에 대한 간략한 설명 (제목같은 느낌)
    * *notes* : 더 자세한 설명을 작성해줍니다.

* @ApiResponse

* - operation의 가능한 response를 명시합니다.

  - - *code* : 응답코드를 작성합니다.
    - *message* : 응답에 대한 설명을 작성합니다.
    - *responseHeaders* : 헤더를 추가할 수도 있습니다.

* @ApiParam

* - 파라미터에 대한 정보를 명시합니다.

  - - *value* : 파라미터 정보를 작성합니다.
    - *required* : 필수 파라미터이면 true, 아니면 false를 작성합니다.
    - *example* : 테스트를 할 때 보여줄 예시를 작성합니다.

* @ApiModel, @ApiModelProperty 

  * Model설명,  Class 필드에 대한 설명(vo의 get메소드)

  

```java
@RestController
@Api(value = "BoardController V2")
@RequestMapping("/v1/api")
public class BoardControllerV1 {

    @ApiOperation(value = "exam", notes = "예제입니다.")
    @ApiResponses({
            @ApiResponse(code = 200, message = "OK !!"),
            @ApiResponse(code = 500, message = "Internal Server Error !!"),
            @ApiResponse(code = 404, message = "Not Found !!")
    })
    @GetMapping(value = "/board")
    public Map<String, String> selectOneBoard(@ApiParam(value = "게시판번호", required = true, example = "1") @RequestParam String no) {
        Map<String, String> result = new HashMap<>();
        result.put("author", "victolee");
        result.put("content", "V1 API 내용");
        return result;
    }
}
```



![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F99FAD94F5E566165195574)





#### 참고

https://github.com/swagger-api/swagger-core/wiki/Swagger-2.X---Annotations#apiresponse

https://victorydntmd.tistory.com/341

