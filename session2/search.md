```dart
import 'package:flutter/material.dart';
void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build (BuildContext context) {
    return const MaterialApp(
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState(); 
}

class _HomePageState extends State<HomePage> {

  @override
  Widget build (BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text('search delegate'),
          actions: [
            IconButton(onPressed: (){
              showSearch(context: context, delegate: ProductsSearch());
            }, icon: Icon(Icons.search))
          ],
        ),
      );
  }
}

class ProductsSearch extends SearchDelegate {
  List<String> users = [
    'mohamed',
    'ahmed',
    'hosam',
    'yasser',
    'mostafa',
    'mona',
    'asmaa',
  ];

  @override
  List<Widget>? buildActions(BuildContext context) {
    return [
      IconButton(onPressed: () {
        query = '';
      }, icon: Icon(Icons.close))
    ];
  }

  @override
  Widget? buildLeading(BuildContext context) {
    return IconButton(onPressed: () {
      close(context, null);
    }, icon: Icon(Icons.arrow_back));
  }

  @override
  Widget buildResults(BuildContext context) {
    return Text('welcome $query', style: const TextStyle(fontSize: 22, fontWeight: FontWeight.bold),);
  }

  @override
  Widget buildSuggestions(BuildContext context) {
    return query.isEmpty? customSuggest(users) : customSuggest(users.where((element) => element.startsWith(query)).toList());
  }

  Widget customSuggest(List<String> items) {
    return ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) => InkWell(
          onTap: () {
            query = items[index];
            showResults(context);
          },
          child: Card(
          child: Padding(
            padding: const EdgeInsets.all(15),
            child: Text(items[index], style: const TextStyle(
              fontSize: 22,
              fontWeight: FontWeight.bold
            ),),
          ),
        ),
        ),
      );
  }

}
```