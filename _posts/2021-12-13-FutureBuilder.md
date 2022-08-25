---
layout: post
title: FutureBuilder
author: "praconfi"
tags: Flutter
---

dart는 비동기적으로 진행되기 때문에 API호출 후 바로 ui를 그리게 된다.  
API에서 받아온 데이터를 렌더해야 하는 경우 오지 않은값을 렌더해야하기 때문에 문제가 생길수 있는데, 이를 FutureBuilder위젯으로 처리할 수 있다  
API응답이 오기전 화면을 따로 지정할 수 있다
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
      
    } catch (e) {

    }

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