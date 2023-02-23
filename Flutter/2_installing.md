

# Installing Flutter

[Get started](https://docs.flutter.dev/get-started/install)
``` bash
sudo snap install flutter --classic
flutter sdk-path
```
- SDK means software development kit

`flutter doctor` command it looks your installation and checks if it's in a good health. If something is missing, you can fix it.

Use VS Code to program the app, and install the extentions: 

- flutter
- dart
- bloc
- rainbow bracket

# Chapter 8: Project SetUp

Reverse domain identifier

``` bash
flutter create --org xxx.domain appname
```
If your website is `foobar.com` and you app is `bazz` 
your reverse name will `com.foobar.bazz`.

**Is important to fill this before because when publishing will be a problem**

[Here is more information](https://www.youtube.com/watch?v=VPvVD8t02U8&t=18040s)

To upgrade flutter:

``` bash
flutter upgrade
```

## structure application

`ios` folder that contain the native necessary for flutter to run iOS simulator.

`android` the same reason as the `ios` folder. 

`test` where you create your test. 

`web` folder, because now flutter support web applications in flutter.

`analysis_options.yaml` analysis is a way to flutter to look at the code that you are writing and correct you.

`pubspec.yaml` read the comments to understand what they mean. This file is kind of a control file, dependencies, version, name, etc.

    Observation: In this file you are not going to see the com.yourcompany , this is going to be somewhere that uses when the flutter up deploys. 

    The version number you will see inside this file, with 3 digits, separated by dot. The left number is the mayor number and then the middle the minor number and the right is the bumble or something like that.
    You app will "birth" with 1.0.0, if you add some improvement, will be in the minor version (the middle one). 

    Then you have the environment version, and you will have the sdk (software development kit). Is the sdk require in order to run this application. 

    `dependencies`: Here, as you guess, goes the dependencies.

    There is a default dep `cubertino_icons`, 

In this website pub.dev you can search on dependencies and their documentation.

    `dev_dependencies`: dependencies that run only during the development.

We can add `firebase` as dependencies here now

## Installing Dependencies

In https://publ.dev/packages is the list of official packages form flutter, each one has it's installation instruction.

After the installation, we can see the dependencies in `pubspect.yaml` file in the `dependencies` key.

To bring firebase dependencies just type the following
```bash
flutter pub add firebase_core
flutter pub add firebase_auth
flutter pub add cloud_firestore
flutter pub add firebase_analytics
```