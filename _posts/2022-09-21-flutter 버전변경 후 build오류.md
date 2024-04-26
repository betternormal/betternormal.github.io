---
layout: post
author: "praconfi"
tags: Flutter
title: "flutter 버전변경 후 build 오류"
---

![buildError](../assets/imgs/2022-09-21/compileFlutterBuildDebug.png)

1. fvm으로 최신의 stable한 버전으로 변경
   - `fvm global 3.16.6` 명령어로 글로벌하게 변경가능하다
   - flutter버전은 3개월이전이 안정적이고 좋다

2. gradle 버전확인
    - 해당 플러터 버전으로 새로운 프로젝트를 만든뒤, 사용된 gradle버전을 확인한다
    - cli로 gradle관련 설정을 새 flutter 버전에 맞게 migration 가능한듯? [참고](https://docs.flutter.dev/release/breaking-changes/androidx-migration#what-if-i-cant-use-android-studio)

3. pubspec.lock 제거

4. updated 된 패키지 업데이트
   
    ```
    flutter pub outdated
    flutter pub upgrade --major-versions
    ```

5. clean 후 패키지 재설치
    ```
    flutter clean
    flutter pub get
    ```