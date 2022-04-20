import 'package:flutter/material.dart';
//툴을 이용한 오버라이드
void main() => runApp(MyApp());
//중간고사 코드하고 코드설명문서
//시험방식 온라인 줌사용
//09:30 ~ 12:00
//문서는 코드설명,결과화면 캡쳐
//과제제출후에 줌 로그아웃
//오픈구글링
class MyApp extends StatelessWidget{
  static const String _title ='Widget Example';
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title:_title,
      home: WidgetApp(),
    );
  }
}

class WidgetApp extends StatefulWidget{
  @override
  _WidgetExampleState createState() => _WidgetExampleState();
}

class _WidgetExampleState extends State<WidgetApp>{
  String sum = '';
  TextEditingController value1 = TextEditingController();
  TextEditingController value2 = TextEditingController();

  List _buttonList = ['ADD', 'SUB', 'MUL', 'DIV'];
  List<DropdownMenuItem<String>> _dropDownMenuItems = new List.empty(growable:true);
  String? _buttonText;
  IconData calIcon = Icons.add;

  @override
  void initState() {
    super.initState();
    for (var item in _buttonList) {
      _dropDownMenuItems.add(DropdownMenuItem(value: item, child: Text(item)));
    }
    _buttonText = _dropDownMenuItems[0].value;
  }
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Widget Example')
      ),
      body: Container(
        child: Center(
          child: Column(
            children: <Widget> [
              Padding(
                padding: EdgeInsets.all(15),
                child: Text('RESULT: $sum', style: TextStyle(fontSize: 20)),
              ),
              Padding(
                padding: EdgeInsets.only(left: 20,right: 20),
                child: TextField(keyboardType: TextInputType.number, controller: value1),
              ),
              Padding(
                padding: EdgeInsets.only(left: 20, right: 20),
                child: TextField(keyboardType: TextInputType.number, controller: value2),
              ),
              Padding(
                padding: EdgeInsets.all(15),
                child: ElevatedButton(
                  child: Row(
                    children: <Widget>[
                      Icon(calIcon),
                      Text(_buttonText!)
                      ],
                  ),
                  style: ButtonStyle(backgroundColor: MaterialStateProperty.all(Colors.amber)),
                  onPressed: () {
                    setState((){
                      var value1Int = double.parse(value1.value.text);
                      var value2Int = double.parse(value2.value.text);
                      var result;

                      if (_buttonText == 'ADD'){
                        result = value1Int + value2Int;

                      } else if (_buttonText == 'SUB') {
                        result = value1Int - value2Int;
                      } else if (_buttonText == 'MUL') {
                        result = value1Int * value2Int;
                      } else {
                        result = value1Int / value2Int;
                      }
                      sum = '$result';
                    });
                  })
                ),
              Padding(
                padding: EdgeInsets.all(15),
                child: DropdownButton(items: _dropDownMenuItems, onChanged: (String? value){
                  setState((){
                    _buttonText = value;
                    if(value == 'ADD'){
                      calIcon = Icons.add;
                    } else if (value == 'SUB'){
                      calIcon = Icons.abc;
                    } else if (value == 'MUL'){
                      calIcon = Icons.back_hand;
                    } else {
                      calIcon = Icons.g_translate;
                    }
                  });
                }, value: _buttonText)
                )
            ],
          )
        ),
      )
    );
  }
}
