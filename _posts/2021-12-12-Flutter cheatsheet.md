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
                