---
layout: post
author: "praconfi"
tags: Tips
title: "Google search tips"
---

> 개발자에게 검색능력은 생산성에 큰 영향을 미친다  
> 1. 정확한 솔루션 검색하기  
> 2. 찾은 솔루션 이해하기  
> 3. 원하는대로 수정해서 사용하기  
> 위 단계들을 효율적으로 하기위한 검색 팁들을 알아두면 좋다  

## 1. 정확히 일치하는 키워드 검색
`"keyword"` 쌍따옴표 사용하기  
에러메세지를 검색하는경우 비슷한 단어가 들어간 수많은 에러메세지가 나오면 정확히 내가 찾는 에러를 다시 찾는 수고가 필요하다  
검색하려는 내용이 모두 담겨있고, 내용의 단어들 순서 까지 일치하는 결과를 검색하려면 `"inbound marketing"` 같이 따옴표 안에 검색어를 넣는다

## 2. 자연어 보다는 키워드의 나열로 검색
```js
// Not Recommended
How can I add drag-and-drop feature to my website

// Recommended
implement drag and drop html javascript
```

## 3. 특정 키워드 제거
javascript에 대해 검색하고 싶지만 php 대한 검색결과는
제외하고 싶다면  
```
implement drag and drop html javascript -php
```
으로 검색하면 된다. `다중적용`도 가능하다.

## 4. 특정사이트의 글만 검색
개발관련 검색을 하다보면 stackoverflow나 medium을 보게되는데 이 둘은 성격이 다르다  
- medium: 길고 자세한 설명 + 튜토리얼  
- stackoverflow: 간단명료한 코드  
상황에 따라 맞는 웹사이트에서 정보를 얻는다
```
site:stackoverflow.com implement drag and drop html javascript
```

## 5. 최근글 검색(특정기간 전후 설정 가능)
`after:2020` 과 같이 키워드와 연도를 적는다  
코드는 버전이 올라가면 구현방식도 달라지기 때문에 최근의 글을 보는것이 좋다
```
implement drag and drop html javascript after: 2020
```


## 6. 논리연산자 AND, OR 사용하기
둘다 포함하고있는 검색결과, 둘중에 하나라도 포함하고있는 결과를 찾고싶을때

## 7. 특정 부분을 모를때
**`*`** asterisk를 와일드카드로 사용해서 모르는부분에 채워두면 알아서 검색이 된다.
ex) 아*유(아이유)

## 8. 관련된 내용 검색할때
related:검색할 내용

## 9. 숫자로 범위를 정할수 있는 검색결과
"president korea"1900..1950

## 10. 단어의 정의를 보고싶을때
define:단어

## 11. 특정 파일타입을 찾을때(pdf)
"IELTS 12" filetype:pdf

## 12. 모르는 번호 검색하기
phonebook:123-4567

