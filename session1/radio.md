```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: RadioExample(),
    );
  }
}

class RadioExample extends StatefulWidget {
  @override
  _RadioExampleState createState() => _RadioExampleState();
}

class _RadioExampleState extends State<RadioExample> {
  String? gender;
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('stateful widget')),
        body: Container(
          padding: const EdgeInsets.all(10),
          child: Column(
            children: [
              RadioListTile(value: 'male', groupValue: gender, onChanged: (val) { // try use Switch
                setState(() {
                  gender = val;
                });
              }, title: Text('male'),),
              RadioListTile(value: 'female', groupValue: gender, onChanged: (val) { // try use Switch
                setState(() {
                  gender = val;
                });
              }, title: Text('female'),),
            ],
          ),
        ),
      ),
    );
  }
}
```