> ## 타입스크립트란?
- microsoft사에서 만든 자바스크립트의 superset
- 다양한 버전의 자바스크립트로 트랜스파일 된다.
- 자바스크립트가 사용 되는 모든곳에서 사용가능하다.
- 큰 규모의 프로젝트를 위해 설계되었다.

## 장점

- 정적 타입 체크
- 클래스기반의 object
- 모듈화
- 다양한 브라우저에 최신문법 지원 (ES6를 여러 버전의 자바스크립트로 트랜스파일 가능)
- 다른 고수준의 언어와 비슷한 문법. ex) Java

### 사용방법

npm을 이용해 타입스크립트를 설치한뒤, 확장자가 .ts인 파일을 생성한뒤 타입스크립트 문법에 맞게 스크립트를 작성한다. 이후 tsc 명령어를 이용해 js파일로 트랜스파일 한다.

watch옵션을 설정하면 ts파일을 저장할 때마다 자동으로 변환된다.

```jsx
tsc fileName.ts 
tsc fileName.ts -w
```

## Types

- String
- Number
- Boolean
- Array
- Any
- Void
- Null
- Tuple
- Enum
- Generics

### Examples

```tsx
let myString: string;
let myNum: number;
let myBool: boolean;
let myVar: any;

let strArr: string[];
let numArr: number[];
let boolArr: boolean[];
// or
let strArr: Array<string>;
let numArr: Array<number>;
let boolArr: Array<boolean>;

let strNumTuple: [string, number]; 

let myVoid: void = undefined;
let myNull: null = null; // null, undefined 혼용가능

myString = 'Hello';
muNum = 1;
myBool = false;
myVar = true;

strArr = ['Hello', 'World'];
numArr = [1, 2, 3];
boolArr = [true, false, false];

strNumTuple = ['Hello', 4, 3, 2] //초과되는건 문제없다.

```

## Function

```tsx
function getSum(num1:number, num2:number):number {
	return num1 + num2;
	}

let mySum = function(num1:any, num2:any):number {
	if(typeof num1 == 'string') {
		num1 = parseInt(num1);
	} 
	if(typeof num2 == 'string') {
		num2 = parseInt(num2);
	}
	return num1 + num2 ;
}

function myVoid ():void {
	return;
}
```

## Interfaces

```jsx
interface Todo {
	title: string;
	text: string;
}

function showTodo(todo: Todo) {
	console.log(todo.title + ': ' + todo.text);
}

let myTodo = {title : 'Trash', text : 'Take out trash'}
showTodo(myTodo);
```

# Classes and Inheritance

### 접근제어자

public:  참조가능

private: 클래스 바깥에서 access하지 못하게

protected: 클래스를 상속받은경우에 acess가능

```jsx
interface Userinterface {
	name : string;
	email : email;
	register();
	payInvoice();
}

class User implements Userinterface {
	name : string;
	email : string;
	age: number;

	constructor(name: string, email : string, age: number) {
		this.name = name;
		this.email = email;
		this.age = age;
		console.log('User Created: ' + this.name);
	}
	register() {
		console.log(this.name + 'is now registered');
	}
	payInvoice() {
		console.log(this.name + 'paid invoice')
	}
}

class Menber extends User {
	id : number;
	constructor(id: number, name: string, email: string, age: number){
		super(name, email, age)
		this.id = id;
	}
	payInvoice() {
		super.payInvoice()
	}
}

let Ben: User = new Member(1, 'Ben', 'praconfi@gmail.com');
Ben.payInvoice();
```
