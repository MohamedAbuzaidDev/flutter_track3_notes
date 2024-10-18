```dart
class _MyAppState extends State<MyApp> {
  String txt = 'off';
  bool status = false;
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('stateful widget')),
        body: Container(
          padding: const EdgeInsets.all(10),
          child: Column(
            children: [
              SwitchListTile(value: status, onChanged: (val) { // try use Switch
                setState(() {
                  status = val;
                  txt = val? 'on': 'off';
                });
              }, title: const Text('toggle text'),),
              Text(txt),
            ],
          ),
        ),
      ),
    );
  }
}
```