



# Chapter 11: Firebase Setup

## FlutterFire initialization

Resolve a lot of configurations problems.

The installation and procedure are in the following [URL](https://flutter.firebase.dev/docs.overview)

To install it and use it:

``` bash
dart pub global activate flutterfire_cli # using the cli
```
If you see where the flutter fire is:
``` bash
which flutterfire
# some path as output
```
If then trying flutterfire config and your terminal doesn't find where it is, you need to tell to the terminal where it is installed chaning your path

``` bash
export PATH="$PATH":"$HOME/.pub-cache/bin"
source .zshrc
```

## Firebase Cli

A cli is to help us to interact with firebase from our terminal.

We need to go [here](https://firebase.google.com/docs/cli#install-cli-mac-linux) and follow the steps to install it 

It will ask you to execute a command like this:
``` bash
curl -sL https://firebase.tools | bash
```

When you want to integrate your flutter project with firebase you need to 
create a firebase project on the firebase console. 

In orther to understand where the firebase need to create the project you need to tell it to log it with an account (which probably will have multiple accounts).

``` bash
firebase login

flutterfire configure

-> create an ew project or select an existing one
-> choose android or ios now
-> which ios bundle id: com.<company>.<app_name>
```

As a result you wil see an identifier associated with an iOS app and android app.

We can make sure that these identifiers are correct.
Copy then and search in your entire project.

You will see that they are in `firebase_options.dart` configured.

Be care with who are you going to share this api keys ids.

Go to firebase.com and check that both apps (android and iOS) are running in the same project.
