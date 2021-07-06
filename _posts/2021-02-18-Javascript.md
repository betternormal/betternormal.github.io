---
layout: post
author: "praconfi"
tags: Javascript 
title: "basic of Javascript"
---

# Javascript

> 자바스크립트는 웹페이지에 생동감을 불어넣기 위해 만들어진 프로그래밍 언어이다.
HTML과 CSS로 정적인 페이지를 만들고 그위에 상호작용하는 요소들은 JS로 구현한다.
자바스크립트로 작성한 프로그램을 script라고 부른다. 스크립트는 HTML안에 작성할 수 있는데, 웹페이지를 불러올 때 자동으로 실행된다.

브라우저에는 자바스크립트 가상 머신이라 불리는 엔진이 내장되어 있다. 

엔진의 종류는 다양한데, 대표적으로 아래와 같다.

- V8 : Chrome, Edge, Opera
- SpiderMonkey : Firefox
- IE는 버전에 따라 'Trident'나 'Chakra'라 불리는 엔진을 사용한다.

기존에 브라우저의 언어로만 여겨졌던 자바스크립트는 V8 엔진의 오픈소스화 이후 Node.js를 활용해 서버사이드 개발까지 가능하게 했다. 

# 브라우저에서 하는일

- HTML 에 DOM 추가, 삭제, 수정
- 브라우저 사용자 이벤트 반응(클릭, 포인터움직임, 키보드 등)
- 원격서버에 요청, 파일 업로드, 다운로드
- 쿠키 설정, 이용
- 클라이언트측 데이터 저장(로컬 스토리지)
- 사용자에게 질문, 메세지 alert

# 브라우저에서 할 수 없는 일

- 브라우저는 보안을 위해 자바스크립트의 기능에 제약을 걸어두었다. 이런 제약은 악성 웹페이지가 개인정보에 접근하거나 사용자의 데이터를 손상하는 것을 막기 위해 만들어 졌다.
- 메모리나 CPU같은 저수준 영역의 조작을 허용하지 않는다. 애초에 이런 접근이 필요치 않은 브라우저를 대상으로 만든 언어이기 때문이다.
- 웹페이지 내 스크립트는 디스크에 저장된 임의의 파일을 읽거나 쓰고, 복사하거나 실행할 때 제약을 받을 수 있다. 운영체제가 지원하는 기능을 브라우저가 직접쓰지 못하게 막혀있기 때문이다.
- 모던브라우저에서 파일을 다룰순 있다. 하지만 접근은 제한되어 있다. 사용자가 브러우저 창에 파일을 '끌어다 두거나' <input>태그를 통해 파일을 선택할 때와 같은 특정상황에서만 파일접근을 허용한다.
- 브라우저 내 탭과 창은 대게 서로의 정보를 알 수 없다. 그런제 자바스크립트를 사용해서 한창에서 다른창을 열때는 예외가 적용된다. 하지만 이 경우에도 도메인이나 프로토콜, 포트가 다르면 페이지에 접근할 수 없다. 이런 제약을 Same origin Policy라 부르는데 이 정책을 피하려면 두 페이지는 데이터 교환에 동의해야 하고, 동의와 관련된 특수한 자바스크립트 코드를 포함하고 있어야 한다.
- 이런 제약사항은 사용자의 보안을 위해 만들어졌다. A사이트에서 받아온 페이지가 B페이지에서 받아온 페이지상의 정보에 접근해 중요한 개인정보를 훔치는걸 막기 위해서다.
- 자바스크립트를 이용하면 페이지를 생성한 서버와 쉽게 정보를 주고받을수 있다. 하지만 타 사이트나 도메인에서 받아오는건 불가능하다. 가능하려면 원격서버에서 명확히 승인을 해줘야 한다. (HTTP헤더 등)

## 자바스크립트로 트랜스파일 할수 있는 언어들

- TypeScript : 자료의 명시화(strict data typing)에 집중해 만든 언어이다.
- CoffeeScript : 자바스크립트를 위한 'symantic sugar'이다. 짧은 문법으로 명료하고 이해하기 쉬운 코드를 작성할 수 있다.
- Flow : TypeScript와는 다른방식으로 자료형을 강제한다.
- Dart : 모바일 앱과 같이 브라우저가 아닌 환경에서 동작하는 고유의 엔진을 가진 독자적 언어이다.

## 브라우저의 동작방식과 script의 위치

>브라우저의 동작 방식
1. HTML을 파싱한다.
2. DOMtree를 생성한다.
3. Rendertree(Domtree + CSSOMtree)를 생성한다.
4. Display에 표시한다.

이때, 브라우저는 HTML을 읽어가다가 <scrpit> 태그를 만나면 파싱을 중단하고 Javascript파일을 로드한 후 HTML을 이어나간다. 
![image](https://user-images.githubusercontent.com/64571546/111636028-7312ec00-883b-11eb-93fc-09cb05c1028d.png)

이렇게 되면 Javascript가 생성되지 않은 DOM을 조작할 수 있기 때문에 스크립트 태그의 위치는 중요하다.
  
### 1. body의 최하단에 위치시키기 
  body를 다 읽고나서 스크립트를 실행시킨다.
### 2. <script defer src="script.js">
  defer 속성이 더해진 script는 html파싱이 완료된후 실행된다.
  ![image](https://user-images.githubusercontent.com/64571546/111636511-e9175300-883b-11eb-8296-90821d943c3e.png)
  
### 3. DOMContentLoaded, onload
  - DOMContentLoaded: DOM 생성이 끝난 후
  - onload: 문서에 포함된 모든 콘텐츠(...img, css)이 로드된 후

  ```
  <script>
    	// window.onload가 가장 앞에 위치!
        window.onload = function(){
            console.log("afterwindowload");
            var target = document.querySelector("#test");
            console.log(target);
        }
		// DOMContentLoaded가 두번째에 위치!
        document.addEventListener("DOMContentLoaded", function() {
            console.log("afterdomload");
            var target = document.querySelector('#test');
            console.log(target);
        });
		// 일반 script 코드가 가장 끝에 위치
        console.log("바로시작")
        var target = document.querySelector('#test');
        console.log(target);
    </script>
  ```
  ![image](https://user-images.githubusercontent.com/64571546/111636693-0fd58980-883c-11eb-9b02-cb30f0bd0949.png)


출처 : [https://ko.javascript.info/intro](https://ko.javascript.info/intro)

## for문과 while문의 차이점

> #### for문과 while문은 같은 반복문이지만 사용용도에 차이점이 있다.
> for문을 사용하는 경우
> 
> 반복횟수가 정해진 경우,
주로 배열과 함께 많이 사용

```js
let sum=0;
for(let i=0; i<10; i++){
  sum +=i;
}
console.log(sum);
```
> #### while문을 사용하는 경우
> 
>무한루프나 특정 조건에 만족할 때까지 반복해야 하는 경우,
주로 **파일 읽고 쓰기**에 많이 사용
```js
let sum=0;
i=1;
while(i<=10){
  sum +=i;
  i++
}
console.log(sum);
```

