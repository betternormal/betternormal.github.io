---
layout: post
author: "praconfi"
tags: Flutter
title: "Flutter framework"
---

## Architecture
Flutter 아키텍처는 세가지 주요 계층으로 구성된다.
![archdiagram](../assets/imgs/archdiagram.png)
### 1. Framework layer
- 프레임워크 레이어는 다트로 작성된다  
- UI테마, 위젯, 레이아웃, 애니메이션, 제스쳐 등 기본 구성요소가 포함된다  
- JSON직렬화, 위치정보, 카메라 접근, 인앱결제 등 플러그인이 포함된다
### 2. Engine layer
- 핵심 C++라이브러리가 포함  
- 엔진은 I/O, 그래픽, 텍스트 레이아웃, 접근성, 플러그인 아키텍처, Dart런타임과 같은 Flutter API의 저수준 기본 요소를 구현  
- 화면에서 빠른 렌더링을 위해 Flutter 장면을 래스터화 하는 역할  
### 3. Embedder layer
- 네이티브 앱으로 통하는 진입점을 제공  
- 네이티브 서비스에 대한 접근을 위해 기본 운영체제와 커뮤니케이션(iOS shell과 Android shell을 Embedder API를 통해 통신함)  
## Skia 엔진
Skia는 Android, iOS, Chrome, Windows, Mac, Ubuntu 등 다양한 환경에서 공통 API로 화면을 그릴 수 있도록 도와주는 오픈소스 2D 그래픽 라이브러리이다. Flutter는 Skia엔진을 내장하고 있다. Flutter는 각 디바이스들의 네이티브 컴포넌트를 사용하지 않고, Skia를 통해 렌더링 하기 때문에  디바이스에 제한 없이 동일한 화면으로 렌더링이 가능하다. 

## pubspec.yaml
- pub패키지들은 종속성을 지정하기 위한 메타데이터가 필요하다. 사용자가 해당 메타정보를 확인할 수 있도록 pubspec파일에 작성한다



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
Column은 기본적으로 표시될 위젯의 크기만큼 가로길이를 갖기때문에 스크롤 가능영역이 좁을수 있다   
- ListView + children  
`같은종류의 아이템`을 n개 생성할 때 사용된다
- ListView.builder  
화면에 보여지는 부분만 `lazy`하게 생성한다
- ListView.separted  
ListView.builder의 아이템사이에 `구분선`을 추가할 때 사용된다

## SizedBox와 Container
- Container는 기본적으로 가능한한 최대한의 크기를 갖으려 한다(child가 생기면 child 크기로 줄어듬)  
- SizedBox는 위젯을 특정크기로 설정하고싶을때, 위젯간 거리를 둘 때 사용된다