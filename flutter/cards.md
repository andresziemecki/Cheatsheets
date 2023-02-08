# Cards

We can use [cards widget](https://api.flutter.dev/flutter/material/Card-class.html) to display information much pretier

``` dart
Widget textTemplate(text){
    return Card(
        margin: EdgesInsets.FromLTRB(16.0, 16.0, 16.0, 16.0),
        child: Column(
            crossAxisAlignemt: crossAxisAlignemt.stretch,
            children: <Widget>[Text(text, style: TextSyle(fontSize: 10.0, color: Colors.grey[600]))]
            SizeBox(height: 6.0)
        )
    );
}
```