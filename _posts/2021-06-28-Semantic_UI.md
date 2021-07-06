---
layout: post
title: " Semantic UI"
author: "praconfi"
tags: Translate
---

# Semantic UI 공식문서 번역

## 1. Introduction
### 통합( Integrations )

다른 라이브러리와 semantic UI 사용하기

- React
semantic UI와 React의 결합은 아직 개발중이지만 대부분의 요소들은 사용가능합니다.
참고: [https://github.com/Semantic-Org/Semantic-UI-React](https://github.com/Semantic-Org/Semantic-UI-React)

- Meteor
- Ember
- Angular

### 빌드 도구( Build tools )

Semantic UI 와 Gulp 사용하기

### 용어사전( Glossary )

**컴포넌트들의 타입**(Types of Components): Semantic UI는 품질에 따라 요소들을 다른 타입으로 정의한다. 5개의 타입은 각각 고유의 정의 형식을 사용한다.

- Globals: Globals는 사이트 전체에 적용된다. 예를들어 CSS resets, sitewide font, link, size 값들을 포함한다.
- Element: UI elements들은 하나의 기능을 가진 페이지 요소이다. 이는 하나로 존재하거나 여러개의 형식으로 기능을 공유하면서 존재할 수 있다.
- Collection: Collections는 주로 같이 쓰이는 서로다른 요소들의 묶음이다. 이는 특정상황에서 예상되는 일련의 기능들을 모아둔다.
- Views: View는 웹사이트 전반적으로 특정타입의 내용을 전달할 때 쓰이는 관습이다. 예를들어 댓글, 피드, 프로필 카드 등이 있다.
- Modules: Modules는 어떻게 보여야하는지, 어떻게 동작해야하는지 정의되어있는 요소이다. 예를들어 드랍다운, 아코디언, 팝업 등이 있다.
- Behaviors: Behaviors는 페이지가 어떻게 동작해야 하는지 설명하는 독립적인 요소이다. 예를들어 검증, 상태관리, API 요청호출 등이 있다.

**프로젝트 용어**(Project Terminology): Semantic UI는 요소들을 분리된 정의들로 나눈다.

- Component: 컴포넌트는 유저인터페이스를 위해 패키징된 일반적인 요소들을 의미한다.
- Definition: Definition은 컴포넌트의 필수기능을 보여주는 CSS와 Javascript의 묶음이다. Definition은 변수들을 이용해 임의로 수정가능한 컴포넌트의 테마를 표현한다.
- ui: ui는 요소안의 요소를 구별짓게 하는 특별한 클래스네임이다.

**정의 용어**(Definition Terminology): 시멘틱UI를 돌아다닐때 내용들이 서로다른 섹션에 묶여있는것을 볼 수 있는데 아래 정의들은 모든정의들에 일관적으로 적용된다. 이것들은 요소를 묘사할 때의 일반적인 패턴이다. 

- Component: 컴포넌트는 유저 인터페이스 요소들을 지칭하는 일반적인 용어이다.
- Definition: definition은 요소의 필수 기능을 묘사하는 CSS, JS의 묶음이다.
- Types: Types는 요소의 기본 모양을 변형시키는 버전들이다.
- Variations: variations는 요소의 속성을 변화시킨다. 예를들어 사이즈, 색상
- Content: content는 요소의 문맥상 의미이다. content는 요소의 예상되는 내용의 종류를 이름으로 갖는다.
- States: state는 요소의 상태를 나타낸다. 예를들어 loading, disabled, and active 가 있다.
- Behaviors: behaviors는 요소가 수행할수 있는 것들이다. behavior는 간단한 set value나 increment와 같은 문장이 대표된다.

일반적 용어(General Terms): 이 요어들은 일반적인 프로그래밍 용어로서 다른페이지에는 설명이 없을수 있다.

- Namespace: 속성의 적용을 위해 요소에 부여하는 이름이다. 예를들어 시멘틱 UI에서는 ui라는 네임스페이스를 사용해 구별하기 쉽게 한다.
- Gulp: gulp는 cli작업의 자동화를 위한 툴이다.
- NPM: npm은 node js 패키지들을 다운로드할때 사용되는 매니저이다.
- NODE JS: node js는 프론트엔드 개발을 위해 CLI를 실행할 때 자주 사용되는 이벤트 기반 프로그래밍 언어이다.

## 2. Usage
