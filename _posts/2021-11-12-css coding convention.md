---
layout: post
title: "CSS coding convention"
author: "praconfi"
tags: CSS
---

# CSS coding convention

1. **id와 class 네이밍**
요소의 목적을 설명할수 있는 이름을 사용한다
    
    ```css
    /* Not recommended: meaningless */
    #abc-1231 {}
    ```
    
    ```css
    /* Recommended: specific */
    #gallery {}
    #login {}
    .video {}
    ```
    
2. **id와 class 네이밍 스타일**
의미전달이 된다면 가능한 짧게 정한다
    
    ```css
    /* Not recommended */
    #navigation {} /* 너무 길다 */
    .atr {} /* 의미전달이 안된다 */
    ```
    
    ```css
    /* Recommended */
    #nav {}
    .author {}
    ```
    
    id나 class이름에 구분이 필요하다면 dash로 구분한다8.
    
    ```css
    /* Not recommended */
    .errorstatus {}
    .error_status {}
    ```
    
    ```css
    /* Recommended */
    #video-id {}
    .ads-sample {}
    ```
    
3. **선택자 사용시 불필요한 상위선택자의 사용은 지양한다**
성능상의 이유
    
    ```css
    /* Not recommended */
    ul#example {}
    div.error {}
    ```
    
    ```css
    /* Recommended */
    #example {}
    .error {}
    ```
    
4. **단축속성의 사용**
코드의 가독성이 좋아진다 [참고링크](https://developer.mozilla.org/ko/docs/Web/CSS/Shorthand_properties)
    
    ```css
    /* Not recommended */
    background-color: #000;
    background-image: url(images/bg.gif);
    background-repeat: no-repeat;
    background-position: top right;
    ```
    
    ```css
    /* Recommended */
    background: #000 url(images/bg.gif) no-repeat top right;
    ```
    
5. **0 단위**
필요한 경우가 아니면 0에는 단위를 붙이지 않는다
    
    ```css
    /* Not recommended */
    margin: 0px;
    padding: 0em;
    ```
    
    ```css
    /* Recommended */
    margin: 0;
    padding: 0;
    ```
    
6. **소수점 표기시 0**
0으로 시작되는 값은 0을 지운다
    
    ```css
    /* Not recommended */
    font-size: 0.8em;
    ```
    
    ```css
    /* Recommended */
    font-size: .8em;
    ```
    
7. **16진법 색상 표기**
가능하다면 3자로 표기한다
    
    ```css
    /* Not recommended */
    color: #eebbcc;
    ```
    
    ```css
    /* Recommended */
    color: #ebc;
    ```
    
8. **선언 순서**
가능하다면 알파벳 순서로 선언한다
    
    ```css
    /* Recommended */
    background: fuchsia;
    border: 1px solid;
    color: black;
    text-align: center;
    ```
    
9. **선언 방식**
속성 이름 뒤에 space 하나를 사용한다
    
    ```css
    font-weight:bold;
    ```
    
    ```css
    font-weight: bold;
    ```
    
10. **세미콜론사용**
일관성을 위해 모든 선언 뒤에 세미콜론을 사용한다
    
    ```css
    /* Not recommended */
    .test {
      display: block;
      height: 100px
    }
    ```
    
    ```css
    /* Recommended */
    .test {
      display: block;
      height: 100px;
    }
    ```
    
11. **선택자 블럭**
선언자와 블럭사이는 스페이스 하나이고, 시작브라켓은 선언자와 같은 선상에 배치한다
    
    ```css
    /* Not recommended */
    #video{
      margin-top: 1em;
    }
    /* Not recommended */
    #video
    {
      margin-top: 1em;
    }
    ```
    
    ```css
    /* Recommended */
    #video {
      margin-top: 1em;
    }
    ```
    
12. **다중선택자 구분**
여러개의 선택자를 사용할 때 각 선택자를 새 줄에 선언한다
    
    ```css
    /* Not recommended */
    a:focus, a:active {
      position: relative; top: 1px;
    }
    ```
    
    ```css
    /* Recommended */
    h1,
    h2,
    h3 {
      font-weight: normal;
      line-height: 1.2;
    }
    ```
    
13. **블럭 구분**
블럭과 블럭사이는 하나의 빈줄로 구분한다
    
    ```css
    html {
      background: #fff;
    }
    
    body {
      margin: auto;
      width: 50%;
    }
    ```
    
14. **속성값에 홑따옴표 사용**
선택자의 속성값은 홑따옴표를 사용한다
URI 값에는 따옴표를 사용하지 않는다
    
    ```css
    /* Not recommended */
    @import url("https://www.google.com/css/maia.css");
    
    html {
      font-family: "open sans", arial, sans-serif;
    }
    ```
    
    ```css
    /* Recommended */
    @import url(https://www.google.com/css/maia.css);
    
    html {
      font-family: 'open sans', arial, sans-serif;
    }
    ```
    
15. **섹션 주석**
주석을 이용해 섹션별 css를 구분한다
    
    ```css
    /* Header */
    
    #adw-header {}
    
    /* Gallery */
    
    .adw-gallery {}
    
    /* Footer */
    
    #adw-footer {}
    ```
    

**참고**

- [구글 스타일가이드](https://google.github.io/styleguide/htmlcssguide.html)