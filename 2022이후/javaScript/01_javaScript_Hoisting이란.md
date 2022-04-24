# Hoisting(호이스팅)

> Hoisting(호이스팅) 개념을 알아본다.

### Hoisting이란

- 변수의 정의가 그 범위에 따라 선언과 할당으로 분리되는 것을 의미한다.
  - 즉, 변수가 함수 내에서 정의되었을 경우, 선언부분만 함수의 최상위로
  - 함수 바깥에서 정의되었을 경우, 전역 컨텍스트의 최상위로 변경된다.
- Hoisting은 쉽게 생각하여 변수를 스코프 내 최상위로 끌어 올린다고 생각하면 된다.
- let과 const변수 선언에서 Hoisting(호이스팅)이 이루어지지않는다. (var만 됨)



### 변수의 Hoisting이 변수 선언문 및 초기화. 함수는 함수 선언방식일때만 Hoisting이 된다.

예시) 변수

```javascript
console.log(a);	// undefined (원래는 이부분에서 undefined가 아니고 오류가 나와야된다.)

var a = 1;
console.log(a);	// 1
```

위의 소스에서 오류가 안나고 undefined가 출력되는 이유는 Hoisting때문이다. 위의 소스는 실제로 아래소스와 같이 실행된다.

```javascript
var a;	// 변수 선언부분만 끌어올려졌다.
console.log(a);	// undefined

a = 1;
console.log(a);	// 1
```



예시) 함수

- Hoisting이 되는 경우

  - 함수선언식 (Function Declaration)의 경우

    ```javascript
    test();
    
    function test() {
    	console.log('test');
    };
    
    test();
    ```

    실제 실행소스(Hoisting이 됨)

    ```javascript
    function test() {
    	console.log('test');
    };
    
    test();
    
    test();
    ```

    

- Hoisting이 안되는 경우

  - new Function 객체 생성의 경우

    ```javascript
    showName();	// ERROR
    var showName = new Function("", console.log("David Kwon"));
    ```

  - let/const 변수 선언의 경우

    ```javascript
    console.log(a); // a를 찾지 못해 error 발생
    
    let a = 1;
    
    console.log(a);
    ```



### Hoisting 우선순위

- 같은 이름의 var 변수 선언과 함수 선언에서의 Hoisting

  - 변수 선언이 함수 선언보다 위로 끌어올려진다.

  ```javascript
   var a = 1;
  
  function a(){
      console.log('123');
  }
  
  console.log(a);	//1
  ```

- 값이 할달되어 있지 않은 변수와 값이 할당되어 있는 변수에서의 Hoisting

  - 값이 할당되어 있지 않은 변수의 경우, 함수선언문이 변수를 덮어쓰지만 값이 할당되어 있는 변수의 경우, 변수가 함수선언문을 덮어쓰인다.

  ```javascript
  var a = 1;
  var b;
  
  function a() {
      console.log("123");
  }
  function b() {
      console.log("123");
  }
  
  console.log(a); // 1
  console.log(b); // function b
  ```



### Hoisting 주의할 점

- 코드의 가독성과 유지보수를 위해 Hoisting이 일어나지 않도록 한다.
- Hoisting을 제대로 모르더라도 함수와 변수를 가급적 코드 상단부에서 선언하면, Hoisting으로 인한 스코프 꼬임 현상은 방지할 수 있다.
- var 보다는 let, const를 사용한다.



