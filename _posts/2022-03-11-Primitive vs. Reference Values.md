---
layout: post
author: "praconfi"
tags: Javascript
title: "Primitive vs. Reference Values"
---
> [이 글](https://www.javascripttutorial.net/javascript-primitive-vs-reference-values/) 을 번역하여 정리했습니다  

JavaScript has two different types of values:  
JavaScript에는 두가지 타입의 값이 존재한다  
- 원시형(Primitive values)  
- 참조형(Reference values)  

원시형은 작은 크기의 데이터를 갖는 반면, 참조형은 여러값을 가진 객체일 수 있다  

## Stack and heap memory
Javascript에서 `변수`를 선언할때 Javascript엔진은 2개의 메모리 위치에 할당한다: stack and heap.  

Static data(정적 데이터)는 compile time에 크기가 정해지는 데이터이다. 아래 종류를 포함한다  
- Primitive values (`null, undefined, boolean, number, string, symbol, and BigInt`)  
- Reference values that refer to objects  

왜냐하면 정적 데이터는 변하지 않는 사이즈를 가지고 있기 때문에 JS 엔진은 고정된 크기의 메모리 공간을 할당하고, stack에 저장시킨다  

For example, the following declares two variables and initializes their values to a literal string and a number:  
예를들어 아래 예시는 두개의 변수를 선언하고, 각각 문자열과 숫자로 초기화한다  
```js 
let name = 'John';
let age = 25;
```
`name`과 `age`는 원시형이기 때문에 JS엔진은 해당 값들을 아래 사진과 같이 stack에 저장한다  
![JavaScript-stack-memory](../assets/imgs/JavaScript-stack-memory.svg)
> 많은 프로그래밍 언어(Java and C#)에서 string은 객체이다.  
> 하지만 Javascript에서는 원시형이다.  


Javascript는 객체, 함수를 heap에 저장한다. JS엔진은 이러한 객체에 고정된 크기의 메모리를 할당하지 않는다. 필요한 만큼 할당하게 된다

아래 예시는 `name`, `age`, `person`변수를 선언한다
```js
let name = 'John';
let age = 25;

let person = {
  name: 'John',
  age: 25,
};
```
내부적으로 JS엔진은 메모리를 아래 사진과 같이 할당한다  
![JavaScript-heap-memory](../asset/../assets/imgs/JavaScript-heap-memory.svg)


위 사진에서 JS엔진은 3개의 변수를 stack의 메모리에 할당한다  
그리고 새로운 객체를 heap memory에 생성한다  
마지막으로 stack메모리의 `person`변수와 heap memory의 객체를 연결시킨다  

이와 같은 이유로 person변수는 객체를 참조하고 있기 때문에 `참조형`이라 부른다  

## Dynamic properties
참조형 값은 속성을 추가, 변경, 삭제할 수 있다
```js
let person = {
  name: 'John',
  age: 25,
};

// add the ssn property
person.ssn = '123-45-6789';

// change the name
person.name = 'John Doe';

// delete the age property
delete person.age;


console.log(person);
```
Output:
```css
{ name: 'John Doe', ssn: '123-45-6789' }
```
원시형은 속성을 갖지 않기 때문에 속성을 추가할 수 없다  
만약 속성을 추가하더라도 에러를 발생시키지는 생기지는 않지만, 추가되지는 않는다  

```js
let name = 'John';
name.alias = 'Knight';

console.log(name.alias); // undefined
```
Output:
```js

undefined
```


## Copying values
원시형 값을 다른 변수에 할당할 때 JS엔진은 값을 복사한 후 새로운 변수에 할당한다.  
```js
let age = 25;
let newAge = age;
```
위 예시에서는 
1. 새로운 변수 `age`를 만들고 25로 초기화한다  
2. 다른 변수 `newAge`를 선언하고 `age`롤 여기에 할당한다  
  여기서 JS엔진은 원시형의 `복사본`을 만든 뒤 이를 `newAge`에 할당한다
![JavaScript-copy-a-primitive-value](../asset/img/../../assets/imgs/JavaScript-copy-a-primitive-value.svg)

스택메모리에서 `newAge`와 `age`는 별개의 변수이다. 만약 둘중 하나의 값을 변경해도 다른하나에 영향이 가지 않는다

For example:
```js
let age = 25;
let newAge = age;

newAge = newAge + 1;
console.log(age, newAge);
```
![](../asset/img/../../assets/imgs/JavaScript-change-a-primitive-value.svg)

참조형 변수를 다른 변수에 할당할 때, JS엔진은 참조를 추가한다.그래서 두 변수는 heap memory에 있는 같은 객체를 참조하게 된다. 즉, 둘중 하나를 변경하면 다른하나에도 영향이 가게된다

For example:
```js
let person = {
  name: 'John',
  age: 25,
};

let member = person;

member.age = 26;

console.log(person);
console.log(member);
```
1.  `person`변수를 선언한뒤 값을 객체로 할당한다  
2.  `person` 변수를 `member`변수에 할당한다  
![JavaScript-copy-a-reference-value](../assets/imgs/JavaScript-copy-a-reference-value.svg)
3. `member`객체에서 `age`속성을 변경한다  
![](../assets/imgs/JavaScript-change-a-reference-value.svg)

`person`변수와 `member`변수는 같은 객체를 참조하고 있기 때문에 `member`변수를 통해 변경된 속성값은 `person`변수에도 영향을 미치게 된다  

## Summary
- Javascript에는 2가지 유형의 값이 있다: 원시형, 참조형  
- 참조형 값에서는 속성값을 이용할 수 있다(추가, 수정, 삭제)  
- 원시형 값을 복사할 때 새로운 메모리에 값을 복사한다. 즉 하나를 변경해도 다른 하나에 영향을 미치지 않는다  
- 참조형 값을 복사할 때 두 변수는 같은 객체를 참조하게된다. 즉 하나를 변경하면 다른하나에 영향을 미치게 된다  