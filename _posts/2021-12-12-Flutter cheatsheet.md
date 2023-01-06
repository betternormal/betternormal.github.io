---
layout: post
title: "Flutter cheatsheet"
author: "praconfi"
tags: Flutter
---

# 프로젝트 생성
```dart
flutter create my_app
```

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

## Build이후 바로 실행시킬 함수 ex) 초기 데이터 fetch
- Future.microtask
- Future.delayed(Duration.zero, () =>...)

위젯이 빌드되면 initState -> build 순으로 호출하게 되는데, build가 되기 전에는 setState가 호출이 되면 안 된다.
fetchItems안에 notifyListeners는 build안에 setState와 같은 역할을 한다.
고로, initState에서 처음 데이터를 가져오되, build 이후 실행이 되어야 하기 때문에 Future.microtask로 잠깐의 딜레이를 주고, build 이후 호출이 되게 한다.

```dart
@override
initState() {
  super.initState();
  Future.microtask(() =>Provider.of<InfiniteProvider>(context, listen: false).fetchItems());
}
```

## initstate에서 async를 사용해야 하는 경우
initstate에서 async를 사용하는건 ui의 inconsistance를 야기시킬수 있기 때문에 해당 메소드 내부에서 기다리게 현재 프레임이 끝나고 호출될 수 있도록 `WidgetsBinding.instance!.addPostFrameCallback`를 사용한다
```dart
Widget build(BuildContext context) {
  
  final authState = context.watch<AuthProvider>().state;
  // 빌드 내에서 네비게이션을 하기때문에 safe 한 operation을 위해 현제 빌드 이후 동작하도록 스케줄링
  if (authState.authStatus == AuthStatus.authenticated) {
    WidgetsBinding.instance!.addPostFrameCallback((_) {
      Navigator.pushReplacementNamed(context, MapScreen.routeName);
    });
  } else if (authState.authStatus == AuthStatus.unauthenticated) {
    WidgetsBinding.instance!.addPostFrameCallback((_) {
      Navigator.pushReplacementNamed(context, SignInScreen.routeName);
    });
  }

  <!-- ... -->
}
```

## Datetime을 한국포맷(연, 월, 일)로 수정할 때
```dart
DateFormat('yyyy년 MM월 dd일').format(item.createdAt!),
```

