# Dart

Some dart [documentation](https://dart.dev/guides) and guides.

Is the programming language that power flutter. 
``` bash
flutter create <project name> 
```
creates a flutter project

To run it -> Command shift P -> flutter: Select device. Then you select the device

THe mayority of the code will be in lib/main.dart

To **run** the code in your simulator, you have to press `run` in the `menu`, and then `run without debugging`

# Keywords

Words reserverd for the programming languages. [Here](https://dart.dev/guides/language/language-tour#keywords) are the keywords from Dart.

## Constants

Constants doesn't change during compile time or run time.

``` dart
const age = 27;
```

When press save, it automatic executes dart formater.

## Variables

``` dart
var name = 'Antohny';
name = 'Antohny';
final name = 'Alex'; // It allows you to define the variable later but when it's defined, it will be like a constant, it cannot be changed.
```

We can also have the `dynamic` variable where we can change it type:

``` dart
dynamic name = 'foo';
name = 30;
print(name); // 30
```

## Functions

Function definitions should follow Cammel case

``` dart
String getFullName(String firstName, String lastName){
    return firstName + ' ' + lastName
} 
```
or 
``` dart
String getFullName(String firstName, String lastName) => 
    firstName + ' ' + lastName;
```

Inside build, if you run a print function
``` dart
print(getFullName('foo', 'bar'))
```
If you press command S, you will see the result in your terminal.

It was a hot reload, saving in flutter triggers an action hot reload, which looks for changes in your code and execute this new changes.

## Arrow Functions

``` dart
String getint() => 'hello';
```

### String formating

if we have two string variables we can concatenate them as follows:
``` dart
'$a $b';
```

# Dart control statements and collections

## If else statements

``` dart
if (name == 'foo'){
    ...
} else if(){
    ...
} else {
    ...
}
```

## Operators
``` dart
final variable = --age; // this put age to age-1 and variable = age - 1, both to the same value
"string"*2 results in: "stringstring"
```

# Lists

``` dart
final names = ['asd', 'dfg'];
final foo = names[1];
final length = names.length;
```
We can add like this:
``` dart
our_list.add('item_to_add');
our_list.remove('item_to_remove');
```

We can add an integer to the list if we don't specify the datatype of the list.

``` dart
List our_list = [];
our_list.add('item_to_add');
our_list.add(30);
```
But it's not a good practice to do that. The good practice is to specify the data
``` dart
List<int> out_list = [];
```

## Advance Lists

We can create lists using the `map` operator, which cicles the list of data and for each item is going to perform a function, and return a value of each element.

For example, inside of our class that extends from State

``` dart
List<String> quotes = ['s1', 's2', 's3'];
// some code ...
body: Column(
    children: <Widget>[...],
    // or
    children: quotes.map((quote){
        return  Text(quote);
    }).toList(),
    // or
    children: quotes.map((quote) =>  Text(quote)).toList();
    ),
)
```



## Sets

List of unique things.

``` dart
var names = {'foo', 'bar'}; // if you mix data types strange things happen
names.add('baz');
```

## Maps

``` dart
const person = {'age': 20};
```

# Chapter 5: Sound Null safety in Dart

Dart comes it a [documentation](https://dart.dev/null-safety) of what this actually mean.

If we want to assign a null value to a string, there will be some warnings. So, to do it, we need to add a special character:

``` dart
String? name = null;
```

This tell that it is a string but this string value maybe absent.

Another example, doing this is not possible:

``` dart
int a = 20;
a = null;
```

but this it is possible:
``` dart
int? a = 20;
a = null;
```

If you want to have a List of strings wich can be nulleable and also put some element nulleable, you have to define it like this:
``` dart
List<String?>? names = ['andres', 'august', null];
```

### Cherry picking non-null values
``` dart
const firstNonNull = firstName ?? secondName ?? lastName;
```
`??` operator tells you, if the firstName is null then pick the second part of the term. In the second part there is another cherry pick.
So, if the secondName is null, then pick lastName.

What the next does is, if the name is null, then assign this name to middlename.
``` dart
 name ??= middlename;
```

### How to access properties from null object?

Example:
``` dart
List<String>? names = null;
final numberOfNames = names.length;
```

That will through an error.

A better way of doing that


``` dart
numberOfNames = 0;
fi (names != null){
    numberOfNames = names.length;
}
```
Using question mark with conditional invocations:
``` dart
final numberOfNames = names?.length ?? 0;
```

the above says: If names is not null, takes the value of length, otherwise take the value of zero.
Finally, the `numberOfNames` will appear as integer and not as optional of integers.

The same you could do with the method `add` of the list.

In summary, there are three operators here we should know: (not sure, please check)
``` dart
?? // if the left it's null assign what's in the right
?. // If it's not null, execute the method
??= // assign to the left what is on the right if the left is null 
```

Reference: website similar to this one dart.dev/null-safety/understanding-null-safety

# Chapter 6: Dart Enumerations and Objects

## Enumerations

Enumerations are name list of related items.

``` dart
enum PersonProperties {
    firstName, lastName
}

print(PersonProperties.firstName)
// output: PersonProperties.firstName

// You can access to its properties als:
print(PersonProperties.firstName.name)
// output: firstName

void test(AnymalType animalType){
    switch(anymalType){
        case AnymalType.cat:
            print("It's a cat");
            break;
        case AnymalType.dog:
            print("It's a dog");
            return;    
    }
}

```

## Classes

``` dart
class Person {

    final String name; // after the person has initialize this instance, you cannot change this name because it's a final

    String lastName = "default_value"; // this is how to set devault values
    Person(this.name); // constructor of the class
    // the previous one could be like follows also:
    Person(name){
        this.name = name;
    }

    void run(){
        print("$this.name Running"); // not sure if this works
    }
}
final person Person();
```

## Inheritance and Subclasses

``` dart

class LivingThings{
    void move(){
        print('I am moving');
    }
}

class cat extends LivingThings{
    LivingThing(String thing, int age) : super(thing, age);
}

```

### Abstract classes
Abstract its like a normal class that can't have instances
``` dart
abstract class LivingThing{
    ...
}
```

THe purpose is to other inherit classes to use their functionalities.

### Factory Constructors

Custom Operator: 
``` dart
class ...{ // all classes extends from Object
    @override 
    bool operator ==(covariant Cat other) => other.name == name;

    @override 
    int get hashCode => name.Hashcode; // override the hash function, this is to know if it's unique or not en a set
}

```


# Chapter 7: Advance Dart

## Extentions

Adding logic to existing classes. For example

Given an existing class `Cat` we can create the following:

``` dart
extension Run on Cat{
    void run(){
        print('cat $name is running'); // name: the name of this cat instance
    }
}
```

In toher words, is a functionality you are adding to the existing class that doesn't really belongs to that class itself
But it exist in the source file you are running in.

Another example building it with a gettter (it's like adding another attribute):

``` dart
extension FullName on Person{
    String get fullName => '$firstName $lastName';
}
print(foo.fullName);
```

## Future
Is data that will be return in the future. It's part of asyncronous programming. 

``` dart
Future<int> heavyFutureThatMultipliesByTwo(int a){
    Future.delayed(const Duration(seconds: 3), ()=> a*2)
}
```

Telling a function that is async, can return values that are not compute inmediatly
``` dart
void test() async {
    final result = heavyFutureMultipliesByTwo(10);
    print(result);// this print will print: "Future<int>" instead of 20 as we expected. 
}
```
But if we run with the `await` keyword
``` dart
void test() async {
    final result = await heavyFutureMultipliesByTwo(10);
    print(result);// this print will print: 20 as we expected after 3 seconds. 
}
```

## Streams

An asynchronous pipe of data. Cotinious pipe of information. It either complete, or never completes or it errors up and die.

``` dart
Stream<String> getName(){
    return Stream.value('hello'); // the inly value that it contain is 'hello'
    return Stream.periodic(const Duration(seconds: 1), functions here like: ()=> 'Foo' )
}
void test async(){
    final value = getName();
    print(value); // this will print ControllerStream<String>

    // let's see another way
    await for (final value = getName()){
        print(value);
    }
}
```

So, streams can periodically return values.

## Generators

A functions returns a list of things but internally it calculates this data in a very simple way.

``` dart
Iterable<int> getOneTwoThree() async*{ // calculate this list of thing asyncronously, we cna do that also sync
    yield 1;
    yield 2;
    yield 3;
}

void test() {
    for (final value in getOneTwoThree()){
        print(value)
    }
}
```

Eeevery time you have a value to output, then you would basically, do a yield.
You can also print the entire list just by `print(getOneTwoThree())`

## Generics

You avoid writing the same code over and over again

``` dart
class Pair {
    final String value1;
    final String value2;
    Pair(this.value1, this.value2);
}
```

If we want a pair of strirng we ened to duplicate code. What you can do instead is:

``` dart
class Pair<A,B> {
    final A value1;
    final B value2;
    Pair(this.value1, this.value2);
}
```