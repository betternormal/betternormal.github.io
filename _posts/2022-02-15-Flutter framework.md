---
layout: post
author: "praconfi"
tags: Flutter
title: "Flutter framework"
---

# Flutter framework

## main()와 runApp()

- main함수는 java와 비슷하게 `프로그램의 시작점`이다
- runApp함수는 위젯트리의 `최상단 위젯`을 스크린에 붙이는 함수이다

## Hot Reload와 Hot Restart

- Hot Reload : 앱의 State는 유지하되 Widget Tree만 재구성하고 main() 및 initState()는 다시 호출되지 않는다.
- Hot Restart : 앱을 새로 시작하며 기존의 State를 잃게 된다.

## StatelessWidget와 StatefulWidget
- SLW은 단한번만 build()를 하고, SFW은 상태가 변경될 때마다 build()를 하기 때문에, 상태값이 필요하지 않은 위젯은 SLW으로 만드는게 성능상 유리하다

## List를 그리는 방식들

- Column + SingleChildScrollView  
전체아이템이 mount되고, paint된다  
`다른종류의 아이템`들을 나열할 때 사용된다
- ListView + children  
`같은종류의 아이템`을 n개 생성할 때 사용된다
- ListView.builder  
화면에 보여지는 부분만 `lazy`하게 생성한다
- ListView.separted  
ListView.builder의 아이템사이에 `구분선`을 추가할 때 사용된다

