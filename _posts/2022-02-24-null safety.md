---
layout: post
author: "praconfi"
tags: Flutter
title: "null safety"
---
> 많은 프로그램의 runtime(프로그램 실행중) 에러중 가장 큰 비중을 차지하는 에러는 NPE(Null Point Exception)  
> null safety는 NPE으로부터 안전한 코드를 작성하는것을 의미  
> edit-time에 체크해, runtime에 NPE가 발생하지 않는 코드를 작성하게 해준다  
> dart 2.12, flutter 2 이상부터 적용

# 규칙
- nullable한 자료형을 제공함으로써 컴파일러가 nullable 변수들을 확인하고, NPE가 예측되면 컴파일단계에서 확인하고 알려준다  
- null 값이 들어갈 수 있는 변수 (선언시 '?' 필요)
- null 값이 들어가면 안되는 변수 (선언시 초기화 필요)
- Class 내의 변수 반드시 선언과 동시에 초기화  
- 생성자를 통해 나중에 초기화되는 class 변수나, 앱이 실행되면서 초기화되는 변수라면 `late 키워드`를 변수앞에 붙이고, 생성자에는 required 키워드를 변수앞에 붙인다  
- 불분명한 상황에 `null assertion operator(!)`를 남발하면 런타임에서 NPE가 생기기 때문에, 확실한 상황에서만 사용한다

# BEFORE null-safety 
- 모든 자료형은 Object의 상속을 받고, Null자료형도 Object의 하위클래스 
- 변수값이 초기화되지 않았거나 null값이 전달되면 컴파일 에러는 발생하지 않고 `런타임 과정에서 오류`가 발생  
![hierarchy-before](../assets/imgs/hierarchy-before.png)



# AFTER null-safety 
![hierarchy-after](../assets/imgs/hierarchy-after.png)

- null 자료형은 Object의 하위클래스가 아닌 `nullable(변수 뒤에 ?를 붙여 선언)`의 하위클래스가 된다.
- null 자료형을 분리하고 다른 자료형들의 null을 허용하지 않는다.
- 변수를 초기화하지 않고 nullable한 표현이 없으면 컴파일이 진행되지 않는다
- nullable변수와 기존 변수의 값전달시 null check가 추가됨(변수 뒤에 !를 붙여 선언), null이라면 에러를, 아니라면 그대로 진행한다  



## Ref
- [참고문서](https://dart.dev/null-safety/understanding-null-safety)  
- [참고글](https://youtu.be/tP9TcrUZoIs)


