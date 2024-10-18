```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CheckboxExample(),
    );
  }
}

class CheckboxExample extends StatefulWidget {
  @override
  _CheckboxExampleState createState() => _CheckboxExampleState();
}

class _CheckboxExampleState extends State<CheckboxExample> {
  bool football = true;
  bool tennis = false;
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('stateful widget')),
        body: Container(
          padding: const EdgeInsets.all(10),
          child: Column(
            children: [
              CheckboxListTile(value: football, onChanged: (val) {
                setState(() {
                  football = val!;
                });
              }, title: Text('football'),),
              CheckboxListTile(value: tennis, onChanged: (val) { // try use Switch
                setState(() {
                  tennis = val!;
                });
              }, title: Text('tennis'),),
            ],
          ),
        ),
      ),
    );
  }
}
```