---
layout: post
title: "Flutter cheatsheet"
author: "praconfi"
tags: Flutter
---

# Textfield 입력중 화면 바깥을 터치해 키보드를 가리고 싶을때
```dart
return GestureDetector(
      onTap: () => FocusManager.instance.primaryFocus?.unfocus(),
      child: Scaffold(
        appBar: AppBar(
          title: Text('App bar'),
        ),
        body: Body(),
      ),
    );
```

# CustomScrollView가 IOS에서 아래로 당겨지지 않게 하고 싶을 때
```dart
CustomScrollView(
  physics: const ClampingScrollPhysics(),
)
```
                
# 키보드에서 이동 버튼을 눌렀을때 특정 이벤트를 실행시키고 싶을 때
- textInputAction을 TextInputAction.go로 설정
- onSubmitted에 콜백함수 작성
```dart
TextField(
    textInputAction: TextInputAction.go,
    onSubmitted: (value) async {
      // do something
    }
```