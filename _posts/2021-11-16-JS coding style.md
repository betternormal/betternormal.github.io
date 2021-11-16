---
layout: post
title: "JS coding style"
author: "praconfi"
tags: Javascript
---

# JS coding style

1. **파일명**  
파일명은 소문자로 작성하고 '-'나 '_'를 포함할 수 있다
    
    ```jsx
    // Recommended
    index.js
    file-name.js
    file_name.js
    ```
    
2. **파일 인코딩**  
UTF-8로 설정한다
3. **들여쓰기**  
2spaces 
4. **중괄호의 사용**  
중괄호 시작 후 줄바꿈
중괄호 내 코드가 없는경우 바로 닫기
    
    ```jsx
    // Recommended
    class InnerClass {
      constructor() {}
      /** @param {number} foo */
      method(foo) {
        if (condition(foo)) {
          try {
            something();
          } catch (err) {
            recover();
          }
        }
      }
    }
    ```
    
5. **const와 let을 이용한 변수선언**  
기본적으로 const를 사용하지만 재할당이 필요한 변수는 let으로 선언한다
6. **네이밍**
- 클래스: 파스칼케이스 ex) `User`
- 함수, 변수, 객체: 카멜케이스 ex) `myFunction`
처음보는 사람도 이해할 수 있도록 상세히 적는다. 길이를 줄이기보다는 의미전달에 목적을 둔다.
누구나 아는 단축어는 줄여도 좋지만 그렇지 않은경우 이해하기 모호해 질 수 있기 때문이다
    
    ```jsx
    // Recommended
    errorCount          
    dnsConnectionIndex  
    referrerUrl         
    customerId  
    ```
    
    ```jsx
    // Not Recommended
    n                   // 아무의미가 없다
    nErr                // n이 모호하다
    nCompConns          // n이 모호하다
    wgcConnections      // 의미파익이 어렵다
    ```
    
7. **변수선언은 한줄에 하나씩 한다**
    
    ```jsx
    // Not Recommended
    let a = 1, b = 2;
    ```
    
    ```jsx
    // Recommended
    let a = 1;
    let b = 2;
    ```
    
8. **동치연산자**  
일치하는경우 ===, 아닌경우 !==를 사용한다  
==와 !=를 사용하는 경우 연산되기 전에 비교할 수 있는 상태로 변환하기 때문에 기대와 다른 결과를 보게 될 수 있다
9. **홑따옴표 사용**  
문자열 표현 시 홑따옴표를 사용한다 
10. **세미콜론의 사용**  
문장의 끝에는 세미콜론을 사용한다. 사용하지 않더라도 코드실행시 자동으로 붙기 때문에 문제는 없다
11. **배열의 생성**  
생성자방식이 아닌 리터럴 방식을 사용한다
    
    ```jsx
    // Not Recommended
    let fruits = new Array('사과', '바나나');
    ```
    
    ```jsx
    // Recommended
    let fruits = ['사과', '바나나'];
    ```
    
12. **객체의 생성**  
생성자 방식이 아닌 리터럴 방식을 사용한다
    
    ```jsx
    // Not Recommended
    let fruits = new Object();
    ```
    
    ```jsx
    // Recommended
    let fruits = {};
    ```
    
13. **객체 Key값**  
따옴표의 유무를 혼용하지 않는다
    
    ```jsx
    // Not Recommended
    {
      width: 42, // struct-style unquoted key
      'maxWidth': 43, // dict-style quoted key
    }
    ```
    
14. **Loop (for문)**  
ES6이후 네가지종류의 for문이 존재한다.  
목적이 조금씩 다르지만 거의 같은 기능을 수행한다. 가능한경우 for - of 를 사용한다
- for: 속도가 가장 빠름
    
    ```jsx
    for (let i = 0; i < array.length; i++) {
        console.log(array[i]);
    }
    ```

- forEach: 콜백함수의 인자로 배열의 값들이 차례로 들어온다 

    ```jsx
    arr.forEach((val)=> {
        console.log(val);
    })
    ```

- for in: 객체에서 사용( key값은 순회가능하나 value는 직접접근 불가 )

    ```jsx
    for (let i in object) {
        console.log(object[i]);
    }
    ```

- for of: 가장최신, Array, Map, Set, arguments 순회가능

    ```jsx
    for (let i of object) {
        console.log(object[i]);
    }
    ```
    
15. **Template literals**  
string에서 간편하게 자바스크립트 변수값을 넣을 때 사용된다
따옴표 대신 백틱 ` 을 사용한다
    
    ```jsx
    // 기존방식
    let a = 2000;
    let b = 21;
    let c = "11월";
    
    let str = "올해는 " + (a + b) + "년이고 " + c + "입니다";
    console.log(str);   // 올해는 2021년이고 11월입니다
    ```
    
    ```jsx
    // **Template literals 사용후**
    let a = 2000;
    let b = 21;
    let c = "11월";
    
    let str = `올해는 ${a + b}년이고 ${c}입니다`;
    console.log(str);   // 올해는 2021년이고 11월입니다
    ```
    
16. **Spread operator**  
문자열, 배열, 객체 등 반복가능한 object를 개별요소로 분리한다
    
    ```jsx
    // 문자열 예제
    let str1 = 'string'; 
    let str2 = [...str1];
    console.log(str2) // ['s', 't', 'r', 'i', 'n', 'g']
    
    // 배열 예제
    let arr1 = [1, 2, 3, 4, 5]; 
    let arr2 = [...arr1, 6, 7, 8, 9]; 
    console.log(arr2); // [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
    
    // 배열 병합 예쩨
    let arr1 = [1,2,3]; 
    let arr2 = [4,5,6]; 
    let arr = [...arr1, ...arr2]; 
    console.log(arr); // [ 1, 2, 3, 4, 5, 6 ]
    
    // 함수 파라메터 예제
    function add(...rest) {
      let sum = 0;
      for (let item of rest) {
        sum += item;
      }
      return sum;
    }
    console.log( add(1) ); // 1
    console.log( add(1, 2) ); // 3
    console.log( add(1, 2, 3) ); // 6
    ```
    
17. **Destructuring**  
[ val1, val2, val3 ] = 배열변수명  
을 하게되면 변수에 저장되어있던 배열의 값들이 val1, val2, val2로 들어간다  
객채를 구조분해 할당 하는경우 key값을 매치해 값을 저장한다
    
    ```jsx
    // 배열 예제
    let arr = ["Bora", "Lee"]
    let [firstName, surname] = arr;
    console.log(firstName); // Bora
    console.log(surname);  // Lee
    
    // 객체 예제
    let options = {
      title: "Menu",
      width: 100,
      height: 200
    };
    let {title, width, height} = options;
    alert(title);  // Menu
    alert(width);  // 100
    alert(height); // 200
    ```
    
18. **Rest parameter**  
함수의 인자로 정해지지 않은 수를 받을 수 있다. 이를 배열로 받게된다.
    
    ```jsx
    function func(...rest) {
      console.log(Array.isArray(rest)); // true
      console.log(rest); // [ 1, 2, 3, 4, 5 ]
    }
    func(1, 2, 3, 4, 5);
    ```
    
19. JS doc  
추가할 예정  
참고영상: [https://youtu.be/YK-GurROGIg](https://youtu.be/YK-GurROGIg)