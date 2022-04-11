#### props

> properties : 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 사용할 수 있다.

```js
1. 
{props이름}.defaultProps = {
    name : ...
} // default rkqt wlwjd

2.
props.children  // 태그 사이의 내용값 <props>이거</props>

3.
import propTypes from 'props-types' //props의 타입(type)지정
{props이름}.propTypes = {
	name : propTypes.string //문자열
	title : propTypes.string.isRequired //필수값
}
```

#### 클래스형 컴포넌트의 state 

#### 1. constructor

```js
constructor(props){
	super(props); //현재 클래스형 컴포넌트가 상송하고 있는 리액트의 component 클래스가 지닌 생성자 함수를 호출한다.
	//state의 초기값 (최초 초기화할 때 사용)
	this.state ={
		number = 0
	}
}
```

#### 2. class 내부에 생성

```js
class Counter extends Component {
	state = {
		number :0,
		fixedNumber : 0
	}
}
```



이렇게 2가지방법이 있는 this.setState함수를 사용하여 state 값을 변경할 때 도 다르다.

```js
// 1.
this.setState({number : number + 1});
// 2.
this.setState({number : this.state.number+1});
```



※ state 주의사항

- 배열이나 객체를 업데이트할 때, 사본을 만들고 그 사본에 값을 업데이트한 후, 사본의 상태를
  - setState, 세터함수(?)를 통해 업데이트 시킨다.

```js
const object ={
    a:1,
    b:2,
    c:3
}

const nextObject = {
    ...object,
    b:2
}
```

참고 : ... 는 spread연산자

