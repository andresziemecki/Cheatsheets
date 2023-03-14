# Routing
One of the attributes of `MaterialApp` widget is:

``` dart
routes: {
    `/`: (context) =>  Loading(),// the context tells where are you in the tree
    ... // other routes
    }

```

the home default route is '/', but we can change it with the initialRoute.

To change between webpage we use `Navigator`

The appBar widget from Scaffold automatically place an arrow in the back part to return to the previous page.

## Pushing and Pping screens

Our app is a stack of screens.

```dart
Navigator.pushName('route')
```

When pressing the back button it pops the current page. So it deletes everything it is in the current page

Becareful on pushing pages that we have already in the stack.