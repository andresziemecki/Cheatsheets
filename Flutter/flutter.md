

# Chapter 12: Basic Register User Screen

## Hot reload vs Hot restart

Hot reload: I have made some changes in my code, so show me this changes. For example, when e change a value of a string. 

However, some changes on the code are so big that flutter is not going to resolve the delta from the previous step. 
That's when a hot restart comes in. It restart you application.

## build

Every time we do a hot reload, we are building the application again. In other words, executing all builds method we have in our app.

So, if you don-t want to rebuild part of your code when you do hot reload, you should remove the "MyApp" from the build part and put it outside.

# Stateless vs Statefull

**State**: It's just data. When you do a hot reload, flutter can keep this data that you have modificed when interacting with the app.If you want to deolete it
just press hot restart.

**Stateful** Is something that we can see on the screan and it can contain data upon whos changes we can redraw instelf. THe state of the widget can change in time.

**Stateless** widgets can't contain mutuable variables or peaces of information or it doesn't manage any mutuable information internally. THe state of this widget cannot change over time.

Creation of state widget:

``` dart
class ClassName extends StatelessWidget {
    const ClassName({Key? key}): super(key:key);
    @override
    Widget build(BuildContext context) {
        return Container();
    }
}
```

The stateless widget is going to enable the hot reload for us. So in the future, when we do hot reload it is going to change all the stateless widget we have changed.



The `build` method is the one response to build all the widget in the app.



# Widget Concept

Everything inside of an application is a widget.

- Root Widget: What's sorround in the entire app
    - App Bar Widget: Which is the nav bar, inside of it we have:
        - Text Widget: Which could be the actual title of the app.
    - Container Widget: Inside of the container:
        - Text Widget

And so on.

We can build a widget tree which describe the structure of your app.

There are a lot of prebuild widget that we can get from the app:
- Text Widget: Style, textAlign, overflow, maxLines, etc.
- Button widget: Color, elevation, disableColor (how to see when the button it's disabled), enabled, etc.
- Row Widget:   
- Column Widget
- Image Widget

Each of these widgets are fully customizables and we can pass different properties to this widget to have the desire display on the screen.

At the end, Widget in flutter are classes, each one has its own programatic class which define each behaivor and also how it looks on the screen.

Dart is the language to set all this things.

## Diving into the code of the create flutter app

The first widget you will see will contain the app, which is the MyApp's widget that extends from stateless widget.

## MaterialApp Widget

Allow s to create a blank cart with google material design features inside the application. It's like a wrapper to the rest of our widgets.

In the same, I can specify the `home` property and a `Text('hey ninjas!')`

``` dart
void main() => runApp(MaterialApp(
    home: Text('hey ninjas!'),
)); // MaterialApp
```

### Scafold Widget

It's the basic building structure of an application to present of a user. It has an `appBar` proerty and a `body` proerty.

It will allow us to implement a basic layout. Like an appbar on the top, some actions botton. All widget comes with the flutter sdk.

try this:

``` dart
void main() => runApp(MaterialApp(
    home: Scaffold( // scafold is also a stateful widget.
        appBar: AppBar( // if you see the documentation app bar is a statefull widget.
            title: Text('Title - all text properties needs a text widget'), // Text is a stateLESS widget compared with the other ones.
            centerTitle: true, // to center the title wrote above
        ),
        // next property
        body: Center(
            child: Text('Hello Ninjas'),// what content will be in the screen
        ), // centralize everything inside of it
        floatingActionButton: FloatingActionButton(
            child: Text('click'),
        ) // button in the bot right corner
        
    ),
));
```

You can see more properties in [scaffold documentation](https://api.flutter.dev/flutter/material/Scaffold-class.html).

Observe that all widgets start with capital letter. 

### Login Button

``` dart
body: Center( // THe center centers horizontally and vertically.
                TextButton(onPressed: () async {}, // in firebase the button press is an async task  
                    child: const Text('Register')), // buttons can display any widget inside, that' why the child property.
            ),
```

To create ext field and separated each other in the same column, we will need the column widget:

``` dart
import 'package:firebase_auth/firebase_auth.dart';

body: Column( children: [
                TextButton(onPressed: () async {
                    final email = _email.text;
                    final password = _password_.text;
                    final userCredential = await FIrebaseAuth.createUserWithEmailAndPassowrd(email: email, password: password); // if you not put the wait, you will get the future instance instead of the work that it's doing
                }, 
                    child: const Text('Register')), 
                TextField(controller: _email,
                            enableSuggestion: false,
                            autocorrect: false,
                            keyBoardType: TextInputType.emailAddress, 
                            
                            decoration: InputDecoration(hintText: 'enter your email')),
                TextField(password: _passowrd,
                            obsecureText: ture, // this is to hide passowrd
                            ),
                ]
            ),
```

To pass information between a TextField to buttons, we need a `TextController`. It's kind of a proxy object and the textField pass this information all the tame is changed to the button that can read that informaiton. To accomplish this, remember you need have wrapped your widget in a statefull wdiget homepage.

``` dart
// inside the class HomePageState extends State<HomePage>

late final TextEditingController _email; // late tells your program that this variable doesn't have a value right now but I promise it will have in the future.
late final TextEditingController _password;

@override 
void initState(){
    _email = TextEditingController();
    _password = TextEditingController();
    super.initState()
}


@override 
void dispose(){
    _email = dispose();
    _password = dispose();
    super.dispose()
}
``` 

To make this work with firebase, we need to go to firebase_options.dart, grap the code that says:
``` dart
import `firebase_option.dart`;
await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
);
```

and put this in the main.dart and put it before the `FirebaseAuth`

If it fails because unreachable host, you need to connect wifi from the virtual phone. 

### Handling configuration not found.

You have to set up Authentication in Firebase. In sign in methodgo to email and passowrd address and allow/enable this. 

### initialize firebaseApp just once

remove the intialization wherever it is and add it after the main title:

``` dart
void main (){
    WidgetsFlutterBinding.ensureInitialized();
    runApp(...)
}
```

source flutter architectural overview to see more documentation about it.

## Future Builder

Sometimes we don;t want to finish the building of a widget before and `await` function will terminate.

To solve this problem we need to use `FutureBuilder`

SO you can wrap the `Column` widget with FutureBuilder

``` dart
FutureBuilder(
    future: Firebase.InitializeApp()
    builder: (context, snapshot) { // this snapshot is the state of the future we set before
        switch (snapshot.connectionState){
            case connectionState.done:
                return Column(...);
            default:
                return Text('Loading...');
        }
        return Column()
    }
)
```

## Sign in methods:

In direbase flutter dev there are many sign in methods, apple, google, etc. 

# Colours and Fonts

## Colors

In some widgest you will se there is the property `backgroundColor`. The color must be a material design color obtained from the material design palette.

The wayy to assign it is: `Colors.red`. You can hold the mouse in red and press `Control+Q` and you will se much more red options. `Colors.red[600]`.

To the floatingActionButton, we must add the `onPressed` which we have to assign a function `() {}`.

We can also add background color to the floatingActionButton. `backgroundColor: Colors.red[600]`.

### Text propertis

``` dart
Text('message')
Text(
    'message',
    style: TextStyle(
        fontSize: 20,
        fontWeight: FontWeight.bold,
        letterSpacing: 2.0,
        color: Colors.grey[600],
    ),
)
```


## Choosing a custom font

1. font.google.com and choose anyone.
2. Press + icon.
3. In top right click download.
4. Save the file, extract.
5. drag the font into a new folder `fonts`
6. Go to `pubpspect.yml` file.
7. scroll and find the fonts comments and uncomment and align
8. Family is a name **we** give to the font family and add the path in the `asset` attribute (delete the rest).

You will have a notification that new dependencies have been changed.

Now you to your `style` properties and add the next:
``` dart
fontFamily: '<familyName>',
```

# Cards

``` dart
Card(
    margin: EdgeInserts.fromLTRB(16,16,16,0),
    child: Padding(
        padding: const edgeInsets.all(12.0),
        child: Column(
            crossAxisAlignemtn: crossAxisAlignemtn.stretch,
            children: <Widget>[
                Text(someText, 
                    style: TextStyle(
                        fontSize: 18.0, 
                        color: Color.grey([600])), 
                        
                    ),
                SizeBox(height:6),
                Text(someOtherText, 
                    style: TextStyle(
                        fontSize: 14.0, 
                        color: Color.grey([800])), 
                        
                    ),
            ]
        ),
    )

)
```

Remember that when alignment a card you have the main axis that goes down and the cross axis that goes horizontal

# Tips
- If the hot reload doesn't work, try "hot restart" (just press restart)

# JSON Serialization



## Shortcuts

- press stl in vscode to create  Stateful or Stateless widget.
- press control dot in any widget you have written and you can wrapp it in another widget from the menu displayed or remove the current widhget.
- control space with get help to fill something

# References

- Documentation of flutter_map [here](https://docs.fleaflet.dev/)
- 