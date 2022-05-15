# 객체에 값 추가

> 1. ``object.assgin()`` 메소드를 사용하여 객체에 요소 추가
> 2. ``push()`` 메소드를 사용하여 객체에 요소 추가
> 3. Spread연산자(...) 를 사용하여 객체에 추가

1. ### ``object.assgin()`` 메소드를 사용하여 객체에 요소 추가

   - ``object.assign()`` 메소드는 객체 정의된 모든 속성을 다른 객체로 복사한다.

   - 즉, 하나 이상의 소스에서 대상 객체로 모든 속성을 복사한다.

     ```js
     const course = {
       name: 'JavaScript'  
     };
     const grade = {
       score: 92  
     };
     
     const finalResult = Object.assign(course,grade);
     console.log(finalResult); // { name: 'JavaScript', score: 92 }
     ```

     

2. ### ``push()`` 메소드를 사용하여 객체에 요소 추가

   - ``push()`` 함수는 배열 끝에 단일 또는 다중 요소를 추가하고 배열의 새 길이를 리턴한다.

     ```js
     const brands = ['nike', 'reebok', 'adidas'];
     const count = brands.push('venum');
     
     console.log(count);   // 4
     console.log(brands);  // [ 'nike', 'reebok', 'adidas', 'venum' ]
     ```

     - ``count``는 배열의 길이를 반환한다.

     - **배열에 포함된 객체에 요소를 추가하는 가장 간단한 방법**

       ```js
       const brands = [{nike:1500}];
       const count = brands.push({reebok:2000});
       
       console.log(count);    // 2
       console.log(brands);   // [{nike: 1500},{reebok: 2000}]
       ```

       

3. ### Spread연산자(...) 를 사용하여 객체에 추가

   - Spread연산자는 JS에서 개체를 병합하거나 복제하는 데 사용한다.

   - 개체의 모든요소가 일부 목록에 포함되어야 할 때, 사용한다.

     ```JS
     const rectangle = {
         radius: 10
     };
     const style = {
         Backcolour: 'red'
     };
     const solidRectangle = {
         ...rectangle,
         ...style
     };
     
     console.log(solidRectangle); // { radius: 10, Backcolour: 'red' }
     ```

     