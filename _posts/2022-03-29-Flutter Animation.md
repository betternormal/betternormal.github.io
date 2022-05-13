---
layout: post
author: "praconfi"
tags: Flutter
title: "Flutter Animation"
---

## Hero widget

여러 페이지에 같은 위젯이 있을 때, Hero위젯을 이용해 부드럽게 변경되게 할 수 있다  

- 공통되는 위젯을 Hero위젯으로 감싸기  
- tag 속성에 같은 값을 넣어주기  
페이지 이동간 flutter가 Hero위젯과 tag를 인식해 자연스럽게 변화시킨다  
## **TickerProvider** class
설정된 시간마다 setState를 호출해, 위젯을 새로 그리도록 한다  
STF위젯에 Ticker관련 클래스를 mixin 하고 사용한다  
- 하나의 애니메이션: `SingleTickerProviderStateMixin`  
- 여러개의 애니메이션: `TickerProviderStateMixin`  
### 1. Animation Controller  
- 시작, 종료, 시간, 반복, 등을 관리한다  
- duration으로 설정된 시간동안 값이 0 ~ 1로 변경됨  
- 위젯이 종료될 때 컨트롤러를 해제 시켜줘야함, 안그러면 메모리 해제가 되지않고, 리소스를 낭비하게 된다  
### 2. Animation
- 애니메이션 자체의 정보로서 Curves, Tween클래스를 이용해 `어떻게` 변화시킬지 정의한다  
- Tween클래스에는 색상, 숫자 등 여러 종류가 있으며 [여기](https://api.flutter.dev/flutter/animation/Tween-class.html)에서 확인해 볼 수 있다.  
- `begin`과 `end`속성을 이용해  필요한 정보를 입력한다. animate메소드 안에 controller를 인자로 넣어 둘을 연결시킨다  
### 3. Animation value
- controller는 기본적으로 0-1의 값을 가지며, 전체 소요시간은 `duration` 값으로 정의한다  
- Tween class를 사용하는 경우 `begin`과 `end` 속성을 이용해 시작과 끝값을 정의할 수 있다  
- 완료되는 경우 관련된 상태값이 리턴되며, `addStatusListener()` 를 이용해 감지할 수 있다  
## Example  

```dart
// 컨트롤러 변수 선언
AnimationController controller;  

// Curved class를 사용하기 위해 animation 선언
Animation animation;
@override
void initState() {
	super.initState();

	controller = AnimationController(
		duration: Duration(second: 1),
		vsync: this,
		upperBound: 100 // 기본값은 0-1이지만 upperBound속성을 이용해 최대값을 수정할 수 있다, Curved class를 사용하는 경우 없애야함
	)
	
	// 좀더 동적인 애니메이션을 표현하기 위해 Curved class를 사용한다
	animation = CurvedAnimation(parent: controller curve: Curves.decelerate)
	controller.forward(); // 증가
	controller.reverse(from: 1.0); // 감소, from속성을 통해 시작값 설정 가능
	controller.addListener(() {
		print(controller.value) // 0에서 1까지 점진적으로 증가
		print(animation.value) // 0에서 1까지 역동적으로(Curves 종류에 따라) 증가
		setState(() {}) // UI를 재렌더링 하기 위해 호출
	})
	controller.addStatusListener((status) {
		// forward()가 완료되었을때의 status는 AnimationStatus.completed
		// reverse()가 완료되었을때의 status는 AnumationStatus.dismissed
		if(status == AnimationStatus.completed) {
			controller.reverse(from: 1.0);
		} else if(status == AnimationStatus.dismiss) {
			controller.forward();
		}
	})

	// repeat 메소드를 통해 무한반복할 수 있다.
	// reverse 속성을 이용해 0~1~0~1 과같이 이어지는 값을 얻을 수 있다 
	AnimationController(duration: const Duration(seconds: 1), vsync: this)
          ..repeat(max: 1, reverse: true);


	// 컨트롤러값을 이용해 투명도 조정 가능 
	backgroundColor: Colors.red.withOpacity(controller.value)

	// 컨트롤러 값에 따라 화면을 변화시키기 위해 addListener 콜백함수 내에 setState를 호출해야 한다
	// addListener는 ..를 이용해 컨트롤러 생성과 함께 실행 시킬수 있다  
	..addListener(() {
            setState(() => {});
          });

	
	controller.value.toInt() // 를 통해 1에서 100까지 1씩 증가되는 로딩 프로그레스바를 표현할 수도 있다

	// 위젯이 종료될 때 컨트롤러를 해제해줘야 메모리에서 해제된다
	@override
	void dispose() {
		controller.dispose();
		super.dispose();
	}
	// animation에는 Curved 대신 Tween클래스를 할당 할 수도 있다. 사용방법은 비슷하지만 특정 값을 변경시킬때 유용할 듯 하다
	// 색깔 속성을 위한 Tween클래스
	animation = ColorTween(begin: Colors.red, end: Colors.blue).animate(controller);

	// 아래와 같이 사용될 수 있다
	backgroundColor: animation.value

}
```
# prepackaged flutter animations
1. flutter_sequence_animation: ^3.0.1  
연속되는 애니메이션을 편리하게 이어줌  
[https://pub.dev/packages/flutter_sequence_animation/versions/4.0.0-nullsafety](https://pub.dev/packages/flutter_sequence_animation/versions/4.0.0-nullsafety)
2. rubber: ^1.0.1  
탄성적인 느낌을 주는 애니메이션  
[https://pub.dev/packages/rubber](https://pub.dev/packages/rubber)
3. sprung: ^3.0.0  
Curved class를 사용하기 쉽게 만든 라이브러리  
[https://pub.dev/packages/sprung](https://pub.dev/packages/sprung)
4. animated_text_kit: ^4.2.1  
다양한 text 애니메이션   
[https://pub.dev/packages/animated_text_kit](https://pub.dev/packages/animated_text_kit)


## Ref
- [https://docs.flutter.dev/development/ui/animations/tutorial](https://docs.flutter.dev/development/ui/animations/tutorial)  
- [https://iosroid.tistory.com/82](https://iosroid.tistory.com/82)  
- [https://beomseok95.tistory.com/320](https://beomseok95.tistory.com/320)  