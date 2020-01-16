# jQuery란

### jQuery

> 제이쿼리는 자바스크립트 언어를 간편하게 사용할 수 있도록 단순환 시킨 오픈 소스 기반의 자바스크립트 라이브러리

* 제이쿼리를 이용하면 문서 객체 모델(DOM)과 이벤트에 관한 처리를 손쉽게 구현할 수 있음
* Ajax 응용 프로그램 및 플로그인도 제이쿼리를 활용하여 빠르게 개발할 수 있음



### jQuery 적용

1. jquery 파일을 다운받아 로드하는 방법
2. CDN(Content Delivery Network)을 이용하여 로드하는 방법



### jQuery 문법

```javascript
$(선택자).동작함수();
```

##### $() 함수

* $() 함수는 선택된 HTML 요소를 제이쿼리에서 이용할 수 있는 형태로 생성햊 주는 역활을 함
* HTML 태그 이름뿐만 아니라, CSS 선택자를 전달하여 특정 HTML 요소를 선택할 수 있음
* $() 함수를 통해 생성된 요소를 jQuery object라고 함



```javascript
//Window 객체의 onload() 메소드를 이용하여 문서가 모두 로드된 뒤에 코드가 실행 되도록 설정
$(window).load( function() {
    $("#win").text("창이 모두 로드됐어요!");
});

//Document 객체의 ready() 메소드를 이용하여 같은 결과를 보장함
$(document).ready( function() {
    $("#doc").text("문서가 전부 로드됐어요!");
});

//위와 같은 결과
$(function(){
  제이쿼리 코드;
})
```







