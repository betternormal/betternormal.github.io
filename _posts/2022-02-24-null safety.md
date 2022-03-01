---
layout: post
author: "praconfi"
tags: Flutter
title: "null safety"
---

> dart 2.12, flutter 2 이상부터 적용

null safety는 NPE(Null Point Exception)으로부터 안전한 코드를 작성하는것을 의미한다  
Runtime(프로그램 실행중)에 발생할 수 있는 NPE를 Compile time에 확인하고 수정할 수 있도록 해준다  
이는 nullable한 자료형을 제공함으로써 컴파일러가 nullable 변수들을 확인하고, NPE가 예측되면 컴파일단계에서 확인하고 알려준다  
## BEFORE null-safety 
![hierarchy-before](../assets/imgs/hierarchy-before.png)

모든 자료형은 Object의 상속을 받고, Null자료형도 Object의 하위클래스이다. 변수값이 초기화되지 않았거나 null값이 전달되면 컴파일 에러는 발생하지 않고 런타임 과정에서 오류가 발생했다.

## AFTER null-safety 
![hierarchy-after](../assets/imgs/hierarchy-after.png)

null 자료형은 Object의 하위클래스가 아닌 nullable(변수 뒤에 ?를 붙여 선언)의 하위클래스가 된다.
null 자료형을 분리하고 다른 자료형들의 null을 허용하지 않는다.

- 변수를 초기화하지 않고 nullable한 표현이 없으면 컴파일이 진행되지 않는다
- nullable변수와 기존 변수의 값전달시 null check가 추가됨(변수 뒤에 !를 붙여 선언),
null이라면 에러를, 아니라면 그대로 진행한다
- 생성자를 통해 나중에 초기화될 예정인 변수라면 late 키워드를 변수앞에 붙이고, 생성자에는 required 키워드를 변수앞에 붙인다


## Ref
- [참고문서](https://dart.dev/null-safety/understanding-null-safety)  
- [참고글](https://youtu.be/tP9TcrUZoIs)


