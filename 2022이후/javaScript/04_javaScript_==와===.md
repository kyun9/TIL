# '==' 와 '==='의 차이점

> ==는 Equal Operator이고,  ===는 Strict Equal Operator의 차이점을 확인해본다.

### == 연산자

- Equal Operator : 동등 연산자
- 자료형 타입 변환 후, 값이 동등한지 비교 (value와 value 비교)
- true/false



### === 연산자

- Strict Equal Operator : 엄격한 연산자
- 자료형 타입과 값이 동등한지 비교 (value와 data type 비교)
- true/false



#### ==를 잘못사용하면 생기는 오류

```javascript
1 == '1'   // true
1 == [1]   // true
1 == true  // true
0 == ''    // true
0 == '0'   // true
0 == false // true
```



### 권장사항

**변수를 비교하거나 어떤 비교를 위해 항상 '===' 연산자를 사용 할 것을 권장한다.**

- 가능한 '==' 연산자를 사용하지 않도록 하고, 대신 직접 자료형을 변환하여(casting) 보다 코드 가독성을 높이도록 한다.
- == 은 null, undefined 비교에 사용해보자!

