# 객체의 키 가져오기

> 1. `Object.keys()` 메소드를 사용하여 객체의 키 가져오기
> 2. `Object.entries(obj)` 메소드를 사용하여 객체의 키 가져오기
> 3. `for` 루프를 사용하여 객체의 `key` 가져오기

1. ### `Object.keys()` 메소드를 사용하여 자바스크립트 객체의 키 가져오기

   - ``Object.keys()`` 함수는 자바스크립트 객체의 키를 포함하는 배열을 반환한다.

     ```js
     var fruitsArr1 = ["Apple", "Orange", "Mango", "Banana"];
     var fruitsObj2 = { 0: "Apple", 4: "Orange", 2: "Mango", 3: "Banana"};
     var fruitsObj3 = { "id": "1", "name": "mango", "color": "yellow"};
     
     console.log(Object.keys(fruitsArr1)); // ["0", "1", "2", "3"]
     console.log(Object.keys(fruitsObj2)); // ["0", "2", "3", "4"]
     console.log(Object.keys(fruitsObj3)); // ["id", "name", "color"]
     ```
   
     - 키가 숫자인 경우 `Object.keys()` 함수는 숫자 키의 배열을 정렬된 순서를 반환한다.
   
   

2. ### `Object.entries(obj)` 메소드를 사용하여 객체의 키 가져오기

   - `Object.entries(obj)` 메소드는 `Object.keys()` 함수보다 다양하고 유연하다.

   - 전체 개체를 작은 배열로 나눈다. [key, value] 형식의 키-값 쌍으로 구성된다.

   - `Object.keys()`를 사용하면 객체의 키만 가져오지만 `Object.entries(obj)`를 사용하면 `keys`와 해당 `values`를 포함하여 객체의 모든 항목을 가져올 수 있다.

     ```js
     const brands = ['nike', 'reebok', 'adidas'];
     const count = brands.push('venum');
     
     console.log(count);   // 4
     console.log(brands);  // [ 'nike', 'reebok', 'adidas', 'venum' ]
     ```

     - `Object.entries(obj)`는 배열로 소멸된 키-값 쌍을 반환한다. 반환 유형은 배열의 배열이며, 각 하위 배열에는 키와 값이라는 두 가지 요소이다. 

     - `[[key1, value1], [key2, value2], [key3, value3] ... ]`와 같다.

       ```js
       var fruitsObj3 = { "id": "1", "name": "mango", "color": "yellow"};
       console.log(JSON.stringify(Object.entries(fruitsObj3)));
       // "[["id","1"],["name","mango"],["color","yellow"]]"
       ```
     
     - 주로 다음과 같이 사용된다.

       ```js
       for (const [key, value] of Object.entries(fruitsObj3)) {
         console.log(`${key}: ${value}`);
       }
       
       // output
       id: 1
       name: mango
       color: yellow
       ```
     
       

3. ### `for` 루프를 사용하여 객체의 `key` 가져오기

   ```js
   var obj = { "id": "1", "name": "mango", "color": "green"};
   
   for(let i in obj) {
     console.log(i); // key
     console.log(obj[i]); // value against the key
   }
   
   //output
   id
   1
   name
   mango
   color
   green
   ```

   

   
