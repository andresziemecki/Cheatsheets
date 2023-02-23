# Handling Errors

The Flutter framework catches errors that occur during callbacks triggered by the framework itself, including errors encountered during the build, layout, and paint phases. Errors that don’t occur within Flutter’s callbacks can’t be caught by the framework, but you can handle them by setting up an error handler on the `PlatformDispatcher`.

All errors caught by Flutter are routed to the `FlutterError.onError` handler. By default, this calls `FlutterError.presentError`, which dumps the error to the device logs. When running from an IDE, the inspector overrides this behavior so that errors can also be routed to the IDE’s console, allowing you to inspect the objects mentioned in the message.

Consider calling `FlutterError.presentError` from your custom error handler in order to see the logs in the console as well.

When an error occurs during the build phase, the `ErrorWidget.builder` callback is invoked to build the widget that is used instead of the one that failed. By default, in debug mode this shows an error message in red, and in release mode this shows a gray background.

When errors occur without a Flutter callback on the call stack, they are handled by the `PlatformDispatcher`’s error callback. By default, this only prints errors and does nothing else.

You can customize these behaviors, typically by setting them to values in your `void main()` function.

## Errors caught by Flutter

To make your application quit immediately any time an error is caught by Flutter in release mode, you could use the following handler:

``` dart
import 'dart:io';

import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

void main() {
  FlutterError.onError = (details) {
    FlutterError.presentError(details);
    if (kReleaseMode) exit(1);
  };
  runApp(const MyApp());
}
```

The top-level kReleaseMode constant indicates whether the app was compiled in release mode.

## Define a custom error widget for build phase errors

To define a customized error widget that displays whenever the builder fails to build a widget, use `MaterialApp.builder`.

``` dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      builder: (context, widget) {
        Widget error = const Text('...rendering error...');
        if (widget is Scaffold || widget is Navigator) {
          error = Scaffold(body: Center(child: error));
        }
        ErrorWidget.builder = (errorDetails) => error;
        if (widget != null) return widget;
        throw ('widget is null');
      },
    );
  }
}
```


## Errors not caught by Flutter

Consider an `onPressed` callback that invokes an asynchronous function, such as `MethodChannel.invokeMethod` (or pretty much any plugin). For example:

``` dart
OutlinedButton(
  child: const Text('Click me!'),
  onPressed: () async {
    const channel = MethodChannel('crashy-custom-channel')
    await channel.invokeMethod('blah')
  },
)
```

If `invokeMethod` throws an error, it won’t be forwarded to `FlutterError.onError`. Instead, it’s forwarded to the `PlatformDispatcher`.

To catch such an error, use `PlatformDispatcher.instance.onError`.

``` dart
import 'package:flutter/material.dart';
import 'dart:ui';

void main() {
  MyBackend myBackend = MyBackend();
  PlatformDispatcher.instance.onError = (error, stack) {
    myBackend.sendError(error, stack);
    return true;
  };
  runApp(const MyApp());
}
```

## Handling all types of errors

Say you want to exit application on any exception and to display a custom error widget whenever a widget building fails - you can base your errors handling on next code snippet:

``` dart
import 'package:flutter/material.dart';
import 'dart:ui';

Future<void> main() async {
  await myErrorsHandler.initialize();
  FlutterError.onError = (details) {
    FlutterError.presentError(details);
    myErrorsHandler.onErrorDetails(details);
  };
  PlatformDispatcher.instance.onError = (error, stack) {
    myErrorsHandler.onError(error, stack);
    return true;
  };
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      builder: (context, widget) {
        Widget error = const Text('...rendering error...');
        if (widget is Scaffold || widget is Navigator) {
          error = Scaffold(body: Center(child: error));
        }
        ErrorWidget.builder = (errorDetails) => error;
        if (widget != null) return widget;
        throw ('widget is null');
      },
    );
  }
}
```


# Try, Catch and Result

## Exception Handling in Dart and Flutter: The basics

As an example, here's a simple Dart function that we can use to fetch a location from an IP address:

``` dart
// get the location for a given IP using the http package
Future<Location> getLocationFromIP(String ipAddress) async {
  try {
    final uri = Uri.parse('http://ip-api.com/json/$ipAddress');
    final response = await http.get(uri); 
    switch (response.statusCode) {
      case 200:
        final data = json.decode(response.body);
        return Location.fromMap(data);
      default:
        throw Exception(response.reasonPhrase);
    }
  } on SocketException catch (_) {
    // make it explicit that a SocketException will be thrown if the network connection fails
    rethrow;
  }
}
```

 the signature of our function doesn't make it explicit that it can throw an exception:

 In fact, the only way to find out if the function throws is to read its documentation and implementation.

And if we have a large codebase, it can be even harder to figure out which functions might throw and which don't.

To handle the exception we need to wrap it in a try catch block

``` dart
try {
  final location = await getLocationFromIP('122.1.4.122');
  print(location);
} catch (e) {
  // TODO: handle exception, for example by showing an alert to the user
}
```

## Improved Exception Handling with the Result type

What we really want is a way to make it explicit that the function can return a result that can be either success or an error.

Here's how we can convert our previous example to use it:

``` dart
// 1. change the return type
Future<Result<Exception, Location>> getLocationFromIP(String ipAddress) async {
  try {
    final uri = Uri.parse('http://ip-api.com/json/$ipAddress');
    final response = await http.get(uri);
    switch (response.statusCode) {
      case 200:
        final data = json.decode(response.body);
        // 2. return Success with the desired value
        return Success(Location.fromMap(data));
      default:
        // 3. return Error with the desired exception
        return Error(Exception(response.reasonPhrase));
    }
  } catch (e) { // catch all exceptions (not just SocketException)
    // 4. return Error here too
    return Error(e);
  }
}
```

Now our function signature tells us exactly what the function does:

- return an Exception if something went wrong
- return a success value with the resulting Location object if everything went well

As a result, we can update our calling code like so:

``` dart
final result = await getLocationFromIP('122.1.4.122');
```

And if we want to handle the result, we can use `pattern matching` with the `when` method:

``` dart
result.when(
  (exception) => print(exception), // TODO: Handle exception
  (location) => print(location), // TODO: Do something with location
);
```

This forces us to handle the error case explicitly, as omitting it would be a compiler error.

So, by using the `Result` type with pattern matching, we can leverage the Dart type system to our advantage and make sure we always handle errors.


## When the Result type doesn't work well

Here is an example of a method that calls several other `async` methods internally:

``` dart
Future<void> placeOrder() async {
  try {
    final uid = authRepository.currentUser!.uid;
    // first await call
    final cart = await cartRepository.fetchCart(uid);
    final order = Order.fromCart(userId: uid, cart: cart);
    // second await call
    await ordersRepository.addOrder(uid, order);
    // third await call
    await cartRepository.setCart(uid, const Cart());
  } catch (e) {
    // TODO: Handle exceptions from any of the methods above
  }
}
```

If any of the methods above throws an exception, we can catch it in one place and handle it as needed.

But suppose we converted each of the methods above to return a `Future<Result>`.

In this case, the `placeOrder()` method would look like this:

``` dart
Future<Result<Exception, void>> placeOrder() async {
  final uid = authRepository.currentUser!.uid;
    // first await call
  final result = await cartRepository.fetchCart(uid);
  if (result.isSuccess()) {
    final order = Order.fromCart(userId: uid, cart: result.getSuccess());
    // second await call
    final result = await ordersRepository.addOrder(uid, order);
    if (result.isSuccess()) {
      // third call (await not needed if we return the result)
      return cartRepository.setCart(uid, const Cart());
    } else {
      return result.getError()!;
    }
  } else {
    return result.getError()!;
  }
}
```

This code is much harder to read because we have to unwrap each `Result` object manually and write a lot of control flow logic to handle all the success/error cases.

In comparison, using try/catch makes it much easier to call multiple async methods sequentially (as long as the methods themselves throw exceptions rather than returning a Result).

## Can we use Result with multiple async calls?

So when considering if you should convert a method to return a `Future<Result>`, you could ask yourself if you're likely to call it in isolation or alongside other async functions.

But it's hard to decide this for every method you declare. And even if a method is called in isolation today, it may no longer be in the future.

What we really want is a way to capture the result of an asynchronous computation made of multiple async calls that could throw, and wrap it inside a `Future<Result>`.

# Futures and error handling

**The Dart language has native asynchrony support, making asynchronous Dart code much easier to read and write. However, some code—especially older code—might still use Future methods such as `then()`, `catchError()`, and `whenComplete()`.**

 **Warning: You don’t need this page if your code uses the language’s asynchrony support: `async`, `await`, and error handling using `try-catch`.**

 [link](https://dart.dev/guides/libraries/futures-error-handling)