# Functions as parameters

Given a parent widget, let say that we want to delete a button when we pressed from a list of children's widgets

So we have to pass a delete function from it's parent which deletes this widget when the widget is pressed, so this function will be called and call the setState from the parent so the parent can remove it.

THis is the implementation


## This is the parent

``` dart
class QuoteList extends StatefulWidget {
  @override
  _QuoteListState createState() => _QuoteListState();
}

class _QuoteListState extends State<QuoteList> {

  List<Quote> quotes = [
    Quote(author: 'Oscar Wilde', text: 'Be yourself; everyone else is already taken'),
    Quote(author: 'Oscar Wilde', text: 'I have nothing to declare except my genius'),
    Quote(author: 'Oscar Wilde', text: 'The truth is rarely pure and never simple')
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[200],
      appBar: AppBar(
        title: Text('Awesome Quotes'),
        centerTitle: true,
        backgroundColor: Colors.redAccent,
      ),
      body: Column(
        children: quotes.map((quote) => QuoteCard(
          quote: quote,
          delete: () { // <------ HERE IS THE MAGIC
            setState(() {
              quotes.remove(quote);
            });
          }
        )).toList(),
      ),
    );
  }
}
```

## These are the children class

``` dart
class QuoteCard extends StatelessWidget {

  final Quote quote;
  final Function delete; // <<<-------- AND HERE IS THE MAGIC
  QuoteCard({ this.quote, this.delete });

  @override
  Widget build(BuildContext context) {
    return Card(
        margin: const EdgeInsets.fromLTRB(16.0, 16.0, 16.0, 0),
        child: Padding(
          padding: const EdgeInsets.all(12.0),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Text(
                quote.text,
                style: TextStyle(
                  fontSize: 18.0,
                  color: Colors.grey[600],
                ),
              ),
              SizedBox(height: 6.0),
              Text(
                quote.author,
                style: TextStyle(
                  fontSize: 14.0,
                  color: Colors.grey[800],
                ),
              ),
              SizedBox(height: 8.0),
              FlatButton.icon(
                onPressed: delete, // <<<-------- AND HERE IS THE MAGIC
                label: Text('delete quote'),
                icon: Icon(Icons.delete),
              )
            ],
          ),
        )
    );
  }
}
```