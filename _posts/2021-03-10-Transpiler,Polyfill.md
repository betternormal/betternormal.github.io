---
layout: post
author: "praconfi"
tags: web Javascript
title: "Transpiler, Pollyfill"
---

# **등장배경**

과거 ES3이 공개되었을 땐 여러 웹 브라우저들의 독자 표준이 정리되어 있지 않은 상황이었다. 그래서 이 시절에는 어느 브라우저를 사용하든 잘 동작하는 JavaScript 코드를 짜는 브라우저 간 호환성(크로스 브라우징)을 확보하는 것이 웹 개발자들에게 큰 고민거리중 하나 였다.

이런 호환성 문제를 호환하기 위해 여러 라이브러리(Prototype, jQuery 등)가 개발되었고, 또 각 브라우저 개발사들이 ECMAScript표준을 따라 브라우저를 만들기 시작하였다.

ES5가 공개된 2009년부터 브라우저 간 호환성 문제가 조금씩 해결되기 시작하였지만, ES6(ES2015)가 나오면서 또 다른 문제점에 봉착하게 되었다. ES6(ES2015)에서는 엄청나게 많은 문법과 기능(클래스, 모듈, 분할, 템플릿 문자열, 반복자, 프록시 등)이 추가되면서 최신 버전의 JavaScript를 지원하지 않는 브라우저가 다시 발생되기 시작한 것이다.

브라우저를 이용하는 사용자들은 구형 브라우저를 업데이트하지 않고 사용하는 일들이 빈번하고, 최신 버전의 브라우저를 사용한다고 하더라도, 각 브라우저마다 업데이트 주기가 다르므로 브라우저마다 지원하는 JavaScript 기능이 조금씩 다르다는 문제점에 봉착하게 된다.

이런 문제를 해결하기 위해, 2가지 도구가 탄생하게 되었는데, 바로 **트랜스파일러(Transpiler)와 폴리필(Polyfill)이다.**

### **크로스 브라우징**

> 표준 웹 기술을 채용하여 다른 기종 혹은 플랫폼에 따라 달리 구현되는 기술을 비슷하게 만들고, 어느 한쪽에 최적화되어 치우치지 않도록 공통 요소를 사용하여 웹 페이지를 제작하는 기법을 말한다. 또한 지원할 수 없는 다른 웹 브라우저를 위한 장치를 구현하여 모든 웹 브라우저 사용자가 방문했을때 정보로서의 소외감을 느끼지 않도록 하는 방법론적 가이드를 의미하는 것이다.                                                                                                                                - Mozilla -

⇒ Html, CSS, JavaScript 작성시 W3C의 웹 규격에 맞는 코딩을 함으로써 어느 브라우저에서나 또는 기기에서 사이트가 제대로 보여지고 작동되도록 하는 기법을 말한다.

---

# 1. **Transpiler(Babel, TypeScript)**

트랜스파일러는 최신 버전 JavaScript의 문법을 똑같이 동작하는 이전 버전 JavaScript의 문법으로 바꾸어주는 도구이다. 이를 이용해 개발자는 최신 버전으로 코딩을 하고, 실제로 배포할 코드는 구형 브라우저에서도 잘 동작하도록 변환해 줄 수 있다.

## Babel

[바벨(Babel)](https://babeljs.io/)은 [트랜스파일러(transpiler)](https://en.wikipedia.org/wiki/Source-to-source_compiler)로, 모던 자바스크립트 코드를 구 표준을 준수하는 코드로 바꿔준다.

바벨의 주요 역할

1. 트랜스파일러 – 최신문법의 코드가 구 표준을 준수하는 코드로 변경된다. [웹팩(webpack)](http://webpack.github.io/)과 같은 모던 프로젝트 빌드 시스템은 코드가 수정될 때마다 자동으로 트랜스파일러를 동작시켜준다. 이런 과정이 없으면 개발이 끝난 코드를 통합하는 데 어려움이 있을 수 있다.
2. 폴리필
폴리필(poly`fill`)은 말 그대로 구현이 누락된 새로운 기능을 메꿔주는(`fill in`) 역할을 한다.

    스크립트에 새로운 함수를 추가하거나 수정해서 스크립트가 최신 표준을 준수 할 수 있게 작업할 수 있다.

    **주목할 만한 폴리필** 

    - [core js](https://github.com/zloirock/core-js) – 다양한 폴리필을 제공합니다. 특정 기능의 폴리필만 사용하는 것도 가능합니다.
    - [polyfill.io](http://polyfill.io/) – 기능이나 사용자의 브라우저에 따라 폴리필 스크립트를 제공해주는 서비스입니다.

# 2. **Polyfill**

JavaScript 구동 환경에는 여러가지 문법과 기능이 추가되는데 이를 어느 브라우저 환경에서도 사용할 수 있도록 똑같이 구현해놓은 라이브러리를 폴리필(Polyfill)이라 한다. 

**1. 브라우저 트랜드 확인**

현재 자주사용되고 있는 브라우저는 무엇인지, 어떤 추세이고, 어떤 위치에 있는지 인식을 하고 있는 것이 중요하다. 또한 가장 점유율이 높은 브라우저부터 확인하는 것이 기본이다. 만약 내국인을 상대로 서비스를 할때는 현재 크롬의 점유율이 가장높고, 그 다음 IE로 나타난다. 사파리 같은 경우는 점유율이 가장 낮기때문에 고려를 하되 가장 높은 점유율을 기록하고 있는 크롬보다는 약하게 고려를 하는 것이 좋다.

**2. 크로스브라우징 여부 확인하기**

자신이 JavaScript를 통해 구현한 코드가 어느 브라우저에서도 지원이 되는지 확인하기 위해서는 구글링에 도움을 받는 것이 좋다. 아래의 주소는 JavaScript, CSS 등 브라우저 지원여부 (크로스 브라우징 여부) 를 확인할 수 있는 웹사이트이다.

[http://caniuse.com](http://caniuse.com/)

**3. 버그리포트 참고하기**

Github에는 여러가지 버그 관련 정보가 공유되는데, 어떤 버그들이 존재하는지 정확하게 인식하고 있다면 쓸데 없는 시간낭비를 하지 않아도 되니 참고하는게 좋다.

**4. 구현하기**

크로스브라우징 여부를 확인했다면 브라우저에 상관없이 동일한 개발 환경을 지원할 수 있도록 코드나 플러그인을 제공하는 Polyfill 라이브러리를 사용하거나 직접 구현을 해줘야 한다.

아래 그림을 보면 크롬에서는 Array.prototype.fill() 함수를 지원하지만, IE에서는 지원하지 않는 것을 확인할 수 있다.

![https://blog.kakaocdn.net/dn/w7eFU/btqBkOEyBca/4nnzpsgOsH4cwrTZSSDkbK/img.png](https://blog.kakaocdn.net/dn/w7eFU/btqBkOEyBca/4nnzpsgOsH4cwrTZSSDkbK/img.png)

- 크롬 브라우저 -

![https://blog.kakaocdn.net/dn/cioFi5/btqBox2H88n/qGXvpo2zKNBBk4e0Fn40sk/img.png](https://blog.kakaocdn.net/dn/cioFi5/btqBox2H88n/qGXvpo2zKNBBk4e0Fn40sk/img.png)

- IE 브라우저 -

### 구현방법

**(1) 직접 구현하기**

MDN 웹사이트에 기록되어 있는 Document를 살펴보면 페이지 하단에 '폴리필' 카테고리에 구현된 소스가 존재한다. 이를 이용하면 보다 효율적으로 폴리필을 구현할 수 있다.

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/fill](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

[Array.prototype.fill()
fill() 메서드는 배열의 시작 인덱스부터 끝 인덱스의 이전까지 정적인 값 하나로 채웁니다.
developer.mozilla.org](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

![https://blog.kakaocdn.net/dn/b2qP7R/btqBoN5iie1/0YpWivkM62bkFBjdSpkdZk/img.png](https://blog.kakaocdn.net/dn/b2qP7R/btqBoN5iie1/0YpWivkM62bkFBjdSpkdZk/img.png)

- 폴리필 소스 -

**(2) 라이브러리 사용하기**

npm 내에 기술된 라이브러리들은 점점 더 방대하게 증가하고 있다. npm 웹사이트에 접속하여 해당 환경에 알맞은 폴리필 라이브러리를 설치해 적용하면 된다.

React사용시에는 npm을 통해 react-app-polyfill 라이브러리를 설치하면 된다.

---

표준 브라우저 기능을 사용하도록 전환하는 데 도움이되는 polyfill 목록

- [github/eventlistener-polyfill](https://github.com/github/eventlistener-polyfill#readme)
- [github/fetch](https://github.com/github/fetch#readme)
- [github/form-data-entries](https://github.com/github/form-data-entries#readme)
- [iamdustan/smoothscroll](https://github.com/iamdustan/smoothscroll#readme)
- [javan/details-element-polyfill](https://github.com/javan/details-element-polyfill#readme)
- [jonathantneal/closest](https://github.com/jonathantneal/closest#readme)
- [kumarharsh/custom-event-polyfill](https://github.com/kumarharsh/custom-event-polyfill#readme)
- [marvinhagemeister/request-idle-polyfill](https://github.com/marvinhagemeister/request-idle-polyfill#readme)
- [mathiasbynens/Array.from](https://github.com/mathiasbynens/Array.from#readme)
- [mathiasbynens/String.prototype.codePointAt](https://github.com/mathiasbynens/String.prototype.codePointAt#readme)
- [mathiasbynens/String.prototype.endsWith](https://github.com/mathiasbynens/String.prototype.endsWith#readme)
- [mathiasbynens/String.prototype.startsWith](https://github.com/mathiasbynens/String.prototype.startsWith#readme)
- [medikoo/es6-symbol](https://github.com/medikoo/es6-symbol#readme)
- [nicjansma/usertiming.js](https://github.com/nicjansma/usertiming.js#readme)
- [rubennorte/es6-object-assign](https://github.com/rubennorte/es6-object-assign#readme)
- [stefanpenner/es6-promise](https://github.com/stefanpenner/es6-promise#readme)
- [webcomponents/template](https://github.com/webcomponents/template#template)
- [webcomponents/URL](https://github.com/webcomponents/URL#readme)
- [webcomponents/webcomponentsjs](https://github.com/webcomponents/webcomponentsjs#readme)
- [WebReflection/url-search-params](https://github.com/WebReflection/url-search-params#readme)
- [yola/classlist-polyfill](https://github.com/yola/classlist-polyfill#readme)

# example

간단한 예로 Promise 객체는 기존에 존재하지 않는 ES6에서 추가된 객체로, ES6 이전에서 new Promise()를 하는 경우 JavaScript의 Syntax 이지만 정의되지 않는 function 이라는 의미에서 'Promise is not a function' 의 결과를 보여준다. 이때 Poliyfill 개념을 이용해 Promise를 사용할 수 있도록 정의해준다.
