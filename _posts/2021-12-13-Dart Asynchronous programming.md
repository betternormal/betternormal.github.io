---
layout: post
title: Dart Asynchronous programming
author: "praconfi"
tags: Flutter
---
> 서버요청이나 외부 API를 이용해 외부 데이터를 가져오는 경우 응답까지 기다리는 시간이 소요된다.  
이때 cpu리소스를 낭비하게 될 수 있는데, asynchronous programming을 하면 기다리는 동안 다른 작업을 처리하면서 cpu를 효율적으로 사용할 수 있게 된다.  
비동기(asynchronous)란 동기 처리가 끝난 후에 실행되며, 외부에서 데이터를 가져오는경우와 반응형 프로그래밍을 할 때 쓰인다.  
flutter에서는 두가지 방법으로 비동기 프로그래밍을 구현하는데 Future와 Stream을 이용한다.  
`Future`는 일회성 응답에 사용된다 ex) http요청, 앨범에서 이미지 가져오기, 파일 가져오기 등…  
`Stream` 은 계속해서 데이터의 변화를 감지하고 그에 맞는 처리를 할 때 사용된다 ex) 위치업데이트, 음악재생 등…

# Future

```dart
// Future class를 이용해 미래에 받아올 값이라고 정의한다
// Future 만나게 되면 기다리지 않고 다음줄을 실행하게 된다
Future<String> name = Future.value('ben');
Future<int> age = Future.value(30);
```

## async, await

- Future value를 리턴하는 함수는 async함수이다
- await를 써도 cpu는 놀지 않는다, 다른 작업을 찾아서 한다

```dart
void main() {
  addNumbers(1, 2);
  addNumbers(2, 3);
}

void addNumbers(int num1, num2) async {
  print("계산 시작: $num1 + $num2");

  // server simulate
  await Future.delayed(Duration(seconds: 2), () {
    print("계산완료: $num1 + $num2 = ${num1 + num2}");
  });

  print("함수 완료: $num1 + $num2");
}

// 계산 시작: 1 + 2
// 계산 시작: 2 + 3
// 계산완료: 1 + 2 = 3
// 함수 완료: 1 + 2
// 계산완료: 2 + 3 = 5
// 함수 완료: 2 + 3
```

## async await [order]

- async 함수들의 호출순서를 보장하고싶다면 상위스코프에서 async await를 해주면 된다

```dart
void main() async {
  await addNumbers(1, 2);
  await addNumbers(2, 3);
}

// Future를 return하는 함수만 await키워드를 사용할 수 있다
// Future함수에서 Future가 아닌 값을 반환해도 Future로 감싸서 리턴한다
Future<void> addNumbers(int num1, num2) async {
  print("계산 시작: $num1 + $num2");

  // server simulate
  await Future.delayed(Duration(seconds: 2), () {
    print("계산완료: $num1 + $num2 = ${num1 + num2}");
  });

  print("함수 완료: $num1 + $num2");
}

// 계산 시작: 1 + 2
// 계산완료: 1 + 2 = 3
// 함수 완료: 1 + 2
// 계산 시작: 2 + 3
// 계산완료: 2 + 3 = 5
// 함수 완료: 2 + 3
```

## FutureBuilder

- dart는 비동기적으로 진행되기 때문에 API호출 후 바로 ui를 그리게 된다.
- API에서 받아온 데이터를 렌더해야 하는 경우 오지 않은값을 렌더해야하기 때문에 문제가 생길수 있는데, 이를 FutureBuilder위젯으로 처리할 수 있다
- API응답이 오기전 화면을 따로 지정할 수 있다

```dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  Future<dynamic> getAPI() async {
    String url = "URL";

    try {
      Response response = await http.get(apiAddr);
    } catch (e) {}

    return reuslt;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
          child: FutureBuilder(
              future: getAPI(),
              builder: (context, AsyncSnapshot<Weather> snapshot) {
                if (snapshot.hasData == false) {
                  return CircularProgressIndicator();
                }
                return Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    snapshot.data.code == 800
                        ? Icon(Icons.wb_sunny)
                        : snapshot.data.code / 100 == 8 ||
                                snapshot.data.code / 100 == 2
                            ? Icon(Icons.wb_cloudy)
                            : snapshot.data.code / 100 == 3 ||
                                    snapshot.data.code / 100 == 5
                                ? Icon(Icons.beach_access)
                                : snapshot.data.code / 100 == 6
                                    ? Icon(Icons.ac_unit)
                                    : Icon(Icons.cloud_circle)
                  ],
                );
              })),
    );
  }
}
```

# Stream

- 연속적으로 값을 받고 처리하려면 Future 함수를 여러번 실행시켜야 한다. 이를 보완하기 위해 Stream은 지속적으로 값을 받고, Stream을 닫으면 종료된다
- Stream은 다트 기본제공이 아니기에 패키지를 사용한다
- 스트림값을 바로 functional프로그래밍으로 제어할 수 있다

## StreamController

```dart
import 'dart:async';

void main() async {
  
  final controller = StreamController();
  final stream = controller.stream.asBroadcastStream();

  final streamListener1 = stream.where((val) => val % 2 == 0).listen((val) {
    print("Listener 1 : $val");
  });
  
  final streamListener2 = stream.where((val) => val % 2 == 1).listen((val) {
    print("Listener 2 : $val");
  });
  
  controller.sink.add(1);
  controller.sink.add(2);
  controller.sink.add(3);
  controller.sink.add(4);
  controller.sink.add(5);
}

// Listener 2 : 1
// Listener 1 : 2
// Listener 2 : 3
// Listener 1 : 4
// Listener 2 : 5
```

## async*, yield, await [order]

```dart
import 'dart:async';

void main() {
  calculate(2).listen((val) {
    print("calculate(2) : $val");
  });

  calculate(4).listen((val) {
    print("calculate(4) : $val");
  });
}

Stream<int> calculate(int num) async* {
  for (int i = 0; i < 5; i++) {
    yield i * num;
    await Future.delayed(Duration(seconds: 1));
  }
}

// calculate(2) : 0
// calculate(4) : 0
// calculate(2) : 2
// calculate(4) : 4
// calculate(2) : 4
// calculate(4) : 8
// calculate(2) : 6
// calculate(4) : 12
// calculate(2) : 8
// calculate(4) : 16
```

## Stream async*, await [order]

```dart
import 'dart:async';

void main() {
  playAllStreams().listen((val) {
    print(val);
  });
}

Stream<int> playAllStreams() async* {
  yield* calculate(1);
  yield* calculate(1000);
}

Stream<int> calculate(int num) async* {
  for (int i = 0; i < 5; i++) {
    yield i * num;
    await Future.delayed(Duration(seconds: 1));
  }
}

// 0
// 1
// 2
// 3
// 4
// 0
// 1000
// 2000
// 3000
// 4000
```

## Firestore Stream 변화감지

```dart
CollectionReference reference = Firestore.instance.collection('planets');
reference.snapshots().listen((querySnapshot) {
  querySnapshot.documentChanges.forEach((change) {
    // Do something with change
  });
});
```

## StreamBuilder

- Stream값의 변화를 감지하고 build하는 위젯

```dart
StreamBuilder<QuerySnapshot>(
  stream: Firestore.instance.collection('books').snapshots(),
  builder: (BuildContext context, AsyncSnapshot<QuerySnapshot> snapshot) {
    if (!snapshot.hasData) return new Text('Loading...');
    return new ListView(
      children: snapshot.data.documents.map((DocumentSnapshot document) {
        return new ListTile(
          title: new Text(document['title']),
          subtitle: new Text(document['author']),
        );
      }).toList(),
    );
  },
);
```