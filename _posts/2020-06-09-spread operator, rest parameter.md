---
layout: post
author: "praconfi"
tags: Javascript
title: "spread operator, rest parameter, default parameter"
---

## rest parameter
- `정해지지않은` 수의 파라미터를 받아올 때 `spread연산자(...)를` 사용하여 `배열`형식으로 가져오는것을 말한다  
- 배열이기 때문에 foreach등의 메소드를 사용할 수 있다  
- 사용방법은 파라미터 앞에 (...)를 붙이면 된다  
```js
function poo (...rest){
  console.log(Array.isarray(rest)); // true
  console.log(rest); // [1, 2, 3, 4, 5]
}
poo(1, 2, 3, 4, 5);

function add (x, y, ...rest); // 앞에 파라미터는 일반적인 파라미터로도 받을 수 있다.
```

## spread operator
spread 연산자는 함수의 호출시에 연산자의 대상배열들을 하나하나의 개별 요소로 분리한다.  
```js
//배열
console.log(...[1,2,3]); // 1,2,3
const arr = [1,2,3];
console.log([...arr, 4, 5, 6]); // [1, 2, 3, 4, 5, 6]

//객체
const o1 = {x:1, y:4};
const o2 = {...o1, z :7};
console.log(o2); // {x:1, y:4,z:7};

// 문자열
console.log(...'Hello'); // H e l l o

// 함수에서 사용방법
const arr = [1,2,3];
foo(...arr); // arr 각각요소를 매개변수로 전달한다.
```
## arguments와의 차이점
ES5에서도 가변인자 함수의 경우 ...args객체를 통해 인자값을 확인 할 수 있다.
```js
var foo = function(){
  console.log(arguments);
}; 
foo(1,2); // {'0':1, '1':2}
```
차이점이라면 arguments는 `유사배열객체`이고 rest는 `배열`이다.   
유사배열객체란 배열처럼 사용할 수 있는 '객체'이다. 고로 배열의 메소드를 사용할수없다.  
하지만 순회가능한 특징이있고, length 값을 알 수 있다.  
ES6에서는 arrow function에 arguments는 사용할 수 없고 rest파라미터를 사용하면
더 간편한 코드를작성할수 있다.  

## default parameter
기본함수 매개변수에 값이 없거나 undefined 가 전달 될 경우 매개변수의 `기본값`을 설정, 사용할수 있다.
```js
function multiply(a,b=1){
  return a*b;
}
multiply(2, 5); //10
multiply(2); //2
multiply(3, undefined); //3
```
