# Class

It's a type data.

- Setting properties
- Constructor

``` dart
class Quote{
    String text;
    String author;
    Quote(String text, String author){
        this.text = text;
        this.author  author;
    }

    // With name parameters we can create an object as follows: q = Quote(text: 'some text', author: 'some author');
    // ALso the constructor like that doesnt matter the order
    Quote({String text, String author}){
        this.text= text;
        this.author = author;
    }

    // We can forget about many things and re write this last one as follows:
    Quote({this.text, this.author});
}
```

## import classes

If they are in the same directory:
``` dart
import 'qute.dart'
```

## Print attributes

THe following will not work
``` dart
'$quote.text'
```

Instead do the following
``` dart
'${quote.text}'
```
