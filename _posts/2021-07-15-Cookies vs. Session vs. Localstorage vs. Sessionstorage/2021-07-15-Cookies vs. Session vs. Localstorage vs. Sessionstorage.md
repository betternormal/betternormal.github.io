---
layout: post
title: "Cookies vs. Session vs. Localstorage vs. Sessionstorage"
author: "praconfi"
tags: web
---

## [ Cookies ]

쿠키는 클라이언트(브라우저)에 저장되는 key-value형식의 데이터 파일이고 만료기한이 있다.

HTTP 프로토콜은 connectionless, stateles한 특성을 가지고 있기 때문에 서버가 요청만 봐서는 누구에게서 오는지 알수 없게된다. 이때 쿠키에 사용자에 대한 정보를 담아서 서버로 보내면 서버는 송신자를 파악하고 그에 맞는 응답을 할 수 있게 된다. 쿠키는 이와같이 서버와 클라이언트간의 지속적인 데이터 교환을 위해 만들어졌고 모든 송신에 첨가된다.

쿠키 하나의 크기는 4kb이고, 하나의 도메인당 20개, 브라우저에 300개 까지 저장 가능하다.

 서버에서는 response에 set-cookie로 쿠키값을 할당하고, 브라우저에서는 document.cookie로 확인할 수 있다. 송신시에는 따로 설정하지 않아도 자동으로 request header에 첨부된다.

매번 쿠키를 보내게된다면 기본적으로 4kb의 데이터를 사용하게 되고 이중에는 불필요한 쿠키도 있기때문에 결과적으로 데이터 낭비가 발생하게 된다. 

## [ Session ]

세션은 서버에서 관리하는 사용자정보이다. 

서버는 접속하는 클라이언트마다 session Id를 발급하고, 서버에서 관리한다.

보안적으로 쿠키보다 좋지만, 사용자가 많아질수록 서버에 무리가 가게된다.

클라이언트가 서버에 접속시 서버는 session Id를 발습하고 

사용자 정보를 브라우저에 저장하는 쿠키와 달리 세션은 서버측에서 관리한다.

로그인기능에서 주로 사용된다.

## [  LocalStorage ]

쿠키의 데이터 낭비 단점을 보완하려 나온 웹스토리지이다. 

브라우저는 저장되지만 서버로 매번 전송되지는 않는다. 용량은 5~10mb이다.

데이터는 사용자가 지우지 않는한 영구적으로 저장되며, 자동로그인 기능을 구현할 때 사용된다.

## [ SessionStorage ]

LocalStarage와 비슷한 웹스토리지이다.

차이점으로는 브라우저가 닫힐때 삭제된다. 일회성 로그인 기능을 구현할 때 사용된다.

## [ Usage ]

Cookie: 팝업 오늘은 다시보지 않기

Session: 로그인

LocalStorage: 자동로그인
SessionStorage: 로그인

## [ Ref ]

- [https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies](https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies)
- [https://www.zerocho.com/category/HTML&DOM/post/5918515b1ed39f00182d3048](https://www.zerocho.com/category/HTML&DOM/post/5918515b1ed39f00182d3048)
- [https://velog.io/@kler/TIL4-로컬스토리지-세션스토리지-쿠키-정리](https://velog.io/@kler/TIL4-%EB%A1%9C%EC%BB%AC%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%84%B8%EC%85%98%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80-%EC%BF%A0%ED%82%A4-%EC%A0%95%EB%A6%AC)
- [https://racoonlotty.tistory.com/entry/쿠키와-세션-그리고-로컬-스토리지와-세션-스토리지](https://racoonlotty.tistory.com/entry/%EC%BF%A0%ED%82%A4%EC%99%80-%EC%84%B8%EC%85%98-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EB%A1%9C%EC%BB%AC-%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80%EC%99%80-%EC%84%B8%EC%85%98-%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80)