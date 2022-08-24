---
layout: post
title: "HTML coding convention"
author: "praconfi"
tags: HTML
---

# HTML coding convention

1. **프로토콜**
외부 리소스를 참조할 때 가능하면 https 프로토콜을 사용한다( http만 존재하는경우 예외 )
    
    ```html
    <!-- Not recommended: 프로토콜이 빠져있다 -->
    <script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
    
    <!-- Not recommended: HTTP를 사용했다 -->
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
    ```
    
    ```html
    <!-- OK -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
    ```
    
2. **들여쓰기를 할땐 2spaces를 사용한다 ( 내부회의 필요 )**
탭
- 장점: 기존 사용방식, 눈에 잘들어온다
- 단점: ide, 에디터에 따라 너비가 달라서 이상하게 보이는경우 생김
2spaces
- 장점: 일관성 유지가능, 구글 코딩스타일
- 단점: 탭보다 들여쓰기가 눈에 잘 안들어온다
3. **소문자 사용**
소문자만 사용한다 (태그, 속성, 속성값 모두 소문자 사용)
    
    ```html
    <!-- Not recommended -->
    <A HREF="/">Home</A>
    
    <!-- Not recommended -->
    color: #E5E5E5;
    ```
    
    ```html
    <!-- Recommended -->
    <img src="google.png" alt="Google">
    
    <!-- Recommended -->
    color: #e5e5e5;
    ```
    
4. **인코딩**
UTF-8을 사용하고, 사용중인 에디터도 UTF-8인지 확인한다
    
    ```html
    <meta charset="utf-8">
    ```
    
5. **주석**
필요에 따라 코드를 설명한다
무엇을 다루는지, 어떤 목적인지, 왜 해당코드가 사용되었는지 등
6. **시멘틱한 요소**
목적에 맞는 HTML태그를 사용한다
결과는 같지만 접근성, 재사용성, 코드효율성, 검색엔진 노출면에서 불리하다
    
    ```html
    <!-- Not recommended -->
    <div onclick="goToRecommendations();">All recommendations</div>
    ```
    
    ```html
    <!-- Recommended -->
    <a href="recommendations/">All recommendations</a>
    ```
    
7. **멀티미디어 대체제**
그림이나 미디어 로드에 실패할 경우 보여지는 메세지를 설정한다
    
    ```html
    <!-- Not recommended -->
    <img src="spreadsheet.png">
    ```
    
    ```html
    <!-- Recommended -->
    <img src="spreadsheet.png" alt="Spreadsheet screenshot.">
    ```
    
8. **type 속성 제거**
HTML5 이후 CSS와 script파일을 추가할 때 type을 지정해주지 않아도 된다
    
    ```html
    <!-- Not recommended -->
    <link rel="stylesheet" href="https://www.google.com/css/maia.css"
        type="text/css">
    
    <!-- Not recommended -->
    <script src="https://www.google.com/js/gweb/analytics/autotrack.js"
        type="text/javascript"></script>
    ```
    
    ```html
    <!-- Recommended -->
    <link rel="stylesheet" href="https://www.google.com/css/maia.css">
    
    <!-- Recommended -->
    <script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>
    ```
    
9. **Line-Wrapping**
html코드가 길어지면 가독성을 위해 줄바꿈을 할 수 있다. 줄바꿈 할 경우 원래의 라인에서 4개이상의 공백을 들여쓴다
    
    ```html
    <md-progress-circular md-mode="indeterminate"
                          class="md-accent"
                          ng-show="ctrl.loading"
                          md-diameter="35">
    </md-progress-circular>
    ```
    
10. **속성값을 할당할 때 쌍따옴표를 사용한다**
기능적으로 차이는 없지만 통일성있게 사용해야한다. 구글 스타일가이드에서는 쌍따옴표를 권장한다
    
    ```html
    <!-- Not recommended -->
    <a class='maia-button maia-button-secondary'>Sign in</a>
    ```
    
    ```html
    <!-- Recommended -->
    <a class="maia-button maia-button-secondary">Sign in</a>
    ```

11. **HTML Validity**  
HTML이 유효하게 잘 작성되었는지 [체크해주는 툴](http://validator.kldp.org/)을 이용해서 문제되는 부분을 수정한다.

    
    ![문제가 있는 경우 위와같이 error와 warning을 알려준다](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0558eff6-b2f7-4c4d-89b6-e23948759ddb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211110%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211110T005456Z&X-Amz-Expires=86400&X-Amz-Signature=7ba9081c3ee9f94b77e2269297aa9feb82fdb05320ea84ee4c869bcccf62b09f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)
    
    문제가 있는 경우 위와같이 error와 warning을 알려준다
    
    ![하단에는 문제되는 상세내용을 알려준다. 오래된 방식의 문법도 에러로 표시해 최신문법을 적용하도록 도와준다. ](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7519d90d-1ae7-4b8d-afdd-a2bb7be595a2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20211110%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211110T005514Z&X-Amz-Expires=86400&X-Amz-Signature=c6e3b61d0d18e0b1f3a16f430beaf952ffaacbfcaa27d083d672a0a20145f409&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)
    
    하단에는 문제되는 상세내용을 알려준다. 오래된 방식의 문법도 에러로 표시해 최신문법을 적용하도록 도와준다. 
    
    자주나오는 오류내용은 [여기](https://blog.naver.com/rebehayan/221913804146)에서 확인해볼 수 있다.

**참고**

- [구글 스타일가이드](https://google.github.io/styleguide/htmlcssguide.html)