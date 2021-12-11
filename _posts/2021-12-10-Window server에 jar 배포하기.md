---
layout: post
title: "Window server에 jar 배포하기"
author: "praconfi"
tags: spring os
---

# Window server에 jar 배포하기
스프링부트로 개발된 프로젝트를 window os 서버에 배포하는 과정을 정리했다.  
배포방법에는 `foreground`와 `background`배포가 있는데 전자의 방법은 콘솔창을 닫으면 해당 프로세스도 종료되는 방식이다. 서버는 콘솔창이 닫히더라도 진행되어야 하기 때문에 후자의 방법이 권장된다.

[TIP] 콘솔창을 열 때 해당 디렉토리의 주소에 `cmd`를 입력하면 현재 디렉토리가 터미널에 열리게 된다.
![스크린샷 2021-12-07 13 47 03](https://user-images.githubusercontent.com/64571546/145666593-bc3231b0-e0f8-4c78-8dd1-ffa30a4a5149.png)
## foreground 배포
```bash
java -jar JAR-NAME.jar
```
![스크린샷 2021-12-07 13 48 15](https://user-images.githubusercontent.com/64571546/145666645-4367f5c6-9876-4107-8755-eb765f131f1e.png)

## background 배포
```bash
javaw -jar JAR-NAME.jar
```
## 프로세스 종료
```bash
// javaw 이름으로 실행중인 프로세스를 검색한다
tasklist /svc | findstr javaw 

// 검색된 프로세스의 id값을 이용해 프로세스를 종료한다
taskkill /pid PID /f
taskkill /pid 3778 /f
```

>javaw.exe파일을 복사해 이름을 바꾸면 해당이 이름으로 동작하게 되기 때문에 여러개의 프로세스를 백그라운드로 실행시킬 때는 이름을 명확하게 지정하는게 좋다.