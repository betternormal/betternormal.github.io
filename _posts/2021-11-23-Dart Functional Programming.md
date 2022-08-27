---
layout: post
title: "Dart functional programming"
author: "praconfi"
tags: Flutter
---

함수형 프로그래밍은 형변환과 내장함수를 이용해 새로운 형태의 값을 만들어낸다

결과값을 이어받아 chaining할 수 있고, 결과적으로 코드가 간결해진다

# Type casting

```dart
// List <-> Map <-> Set 

// List에서 형변환
List<String> blackPink = ['a', 'b', 'c', 'd',]; 
final Map blackPinkMap = blackPink.asMap(); // {0: a, 1: b, 2: c, 3: d}
final Set blackPinkSet = blackPink.toSet(); // {a, b, c, d}

// Map에서 형변환
final Map blackPinkAsMap = blackPink.asMap();
List<dynamic> keys = blackPinkAsMap.keys.toList(); // [0, 1, 2, 3]
List<dynamic> values = blackPinkAsMap.values.toList(); // [a, b, c, d]

// Set에서 형변환
Set blackPinkFronSet = Set.from(blackPink); // {a, b, c, d}
List balckSet = blackPinkFronSet.toList(); // [a, b, c, d]
```

# map()

list의 메소드

모든 멤버변수의 형태를 변경한 후, `새로운 리스트`를 반환한다

map()으로 생성된 리스트는 멤버변수가 동일해도 다른 주소값을 가진 리스트이다

### iterable

반복이 가능한 집단(list, array)

.toList()메소드를 이용해 list로 변환

```dart
List<String> blackPink = ['a', 'b', 'c', 'd',] 

blackPink.map((item){
	return 'this it $item' 
});

// with arrow function
final blackPink2 = blackPink.map((item) => '블랙핑크$item')
```

## mapping Map

```dart
Map<String, String> harryPotter = {
  'harry potter': '해리포터',
  'ron': '론',
  'hermione': '헤르미온느'
};

// 맵을 매핑하면 key, value를 같이받는다
final result = harryPotter.map(
    (key, value) => MapEntry('harry potter character $key', '해리포터 캐릭터 $value'));

void main() {
  // key
  print(harryPotter.keys.map((item) => 'key is $item').toList());
	// value
  print(harryPotter.values.map((item) => 'value is $item').toList());
}
```

## Mapping Set

```dart
Set blackPinkSet = {"로제",'지수','제니','리사'};

final newSet = blackPinkSet.map((item) => 'this is $item').toSet();
```

## where()

필터하는 목적

```dart
List<Map<String, String>> people = [
  {
    'name': '제니',
    'group': '블랙핑크',
  },
  {
    'name': '로제',
    'group': '블랙핑크',
  },
  {
    'name': 'RM',
    'group': 'BTS',
  }
];

final result = people.where((item) => item['group'] == 'BTS').toList();
```

## reduce()

최초에만 prev와 next에 첫번째값 두번째값이 들어간다

이후부터 콜백함수의 return값이 다음 반복의 prev가된다

reduce는 멤버변수들과 같은 타입의 결과만 반환할 수 있다

이러한 문제는 fold()로 해결할 수 있다

```dart
List<int> numbers = [1, 2, 3, 4, 5];

int resultInt = numbers.reduce((prev, next) {
  return prev + next;
});

// arrow function
numbers.reduce((prev, next) => prev + next);
```

## fold()

reduce()와 같은역할, 초기값을 정하면서 반환값의 데이터 타입을 정할 수 있다

첫번째 파라메터가 prev로 들어가고 next에 첫번째 멤버변수가 들어간다

```dart
List<int> numbers = [1, 2, 3, 4, 5];

// Generic으로 리턴타입을 명시
numbers.fold<int>(0, (prev, next) => prev + next);

List<String> words = ['안녕', '하세요'];

words.fold<String>('', (prev, next) => prev + next); // 안녕하세요
words.fold<int>(0, (prev, next) => prev + next.length); // 5

```

## …cascade operator

리스트를 합치는 경우

멤버변수가 풀어져서 들어가게 된다

새로운 리스트를 만들게 된다

```dart
List<int> even = [2, 4, 6];
List<int> odd = [1, 3, 5];
List newArr = [...even, ...odd]; 

// [...even] 과 even은 다르다
```