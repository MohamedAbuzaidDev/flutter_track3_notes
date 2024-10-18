# LocalKey

## ValueKey

```dart
tiles = [
      StatefulColorfulBox(key: ValueKey(1),),
      StatefulColorfulBox(key: ValueKey(2),),
    ];
```

## ObjectKey

```dart
tiles = [
      StatefulColorfulBox(key: ObjectKey(Product(id: 1, title: 't-shirt')),),
      StatefulColorfulBox(key: ObjectKey(Product(id: 2, title: 't-shirt')),),
    ];
```

## UniqueKey

```dart
tiles = [
      StatefulColorfulBox(key: UniqueKey(),),
      StatefulColorfulBox(key: UniqueKey(),),
    ];
```

# Ex Local

- main.dart
  
```dart
void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: SwapExample(),
    );
  }
}
```

- key_example.dart

```dart
import 'package:flutter/material.dart';
import 'dart:math';

class SwapExample extends StatefulWidget {
  const SwapExample({super.key});

  @override
  State<SwapExample> createState() => _SwapExampleState();
}

class _SwapExampleState extends State<SwapExample> {
  late List<Widget> tiles;

  @override
  void initState() {
    super.initState();
    tiles = [
      StatefulColorfulBox(key: ValueKey(1),),
      StatefulColorfulBox(key: ValueKey(2),),
    ];
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: swapTiles,
        child: const Icon(Icons.sentiment_very_satisfied),
      ),
      body: SafeArea(
        child: Row(children: tiles,),
      ),
    );
  }

  swapTiles() {
    setState(() {
      tiles.insert(1, tiles.removeAt(0));
    });
  }
}


class StatelessColorfulBox extends StatelessWidget {
  final Color color;
  const StatelessColorfulBox({super.key, required this.color});

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 50,
      height: 50,
      color: color,
    );
  }
}

class StatefulColorfulBox extends StatefulWidget {
  const StatefulColorfulBox({super.key});

  @override
  State<StatefulColorfulBox> createState() => _StatefulColorfulBoxState();
}

class _StatefulColorfulBoxState extends State<StatefulColorfulBox> {
  late Color color;

  @override
  void initState() {
    color = UniqueColor.randomColor();
    super.initState();
  }
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 50,
      height: 50,
      color: color,
    );
  }
}

class UniqueColor {
  static Color randomColor() {
    return Color(Random().nextInt(0xffffffff));
  }
}
```

# Ex Global Key

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: GlobalKeyCounterApp(),
  ));
}

class GlobalKeyCounterApp extends StatelessWidget {
  // Define a GlobalKey to access the state of the Counter widget
  final GlobalKey<CounterWidgetState> counterKey = GlobalKey<CounterWidgetState>();

  GlobalKeyCounterApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('GlobalKey Counter App'),
      ),
      body: Center(
        // Use the GlobalKey to assign to the CounterWidget
        child: CounterWidget(key: counterKey),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Use the GlobalKey to access the counter's state and increment it
          counterKey.currentState?.incrementCounter();
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}

class CounterWidget extends StatefulWidget {
  const CounterWidget({super.key});

  @override
  State<CounterWidget> createState() => CounterWidgetState();
}

class CounterWidgetState extends State<CounterWidget> {
  int _counter = 0;

  // Method to increment the counter
  void incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text(
      'Counter: $_counter',
      style: const TextStyle(fontSize: 32),
    );
  }
}
```