# Releasing Procedure

This document will show how to release an app from scratch

## Creating the app

Create a flutter application with its organization name, the org name is used for Apple Store and Play Store to identify the app. More information [here](https://stackoverflow.com/questions/73117713/what-is-the-purpose-of-organization-name-when-we-create-a-new-flutter-project).

### How to choose the organization name

If company website is www.mywebsite.com you should have your bundle id as com.mywebsite.app (.app is optional but it's a good practice to add app).

### Command to create the app

```
flutter create --org ai.flyland --project-name app --template=app --platforms ios,android app
```

## iOS App Setup

You need an iOS developer account.

App store connect is your portal to manage your applications and uploading to the appstore.

The app will be signed with your certificate. The certificate you get is your identity as a developer, so whenever you publish an app to the app store, the certificate tells to apple that the app comes from us.

Each flavor can be signed with different profiles, for example the development profile and production profile.

From the certificates and profiles you have to make sure about two things:

1. The application is signed with the production certificate.
2. The application is signed with the production profile which is hook with the certificate.

The App ID is the identifier that apple and you know which application are you talking about and its capabilities.

Certificates KeyChain: You are creating a digital signal on your computer then you request your certifcate
and hook the certificate with the private key creating a chain.

### Steps

1. Go to https://developer.apple.com/account
2. Go to Certificates and create a new one -> iOS App Development (stop here)
3. Go to the keychain access app in your notebook 
4. Menu -> Certificate assistance -> Request a Certificate from a certificate authority
5. You have to put your company email there -> Save the file generated.
This create a private key in the keychain access, but you can't check which one because it doesnt have the date
6. Go back to 2 and upload this certificate you have downloaded.
7. Continue -> Download the certificate (ios_development.cer file) and double click on it
8. Once double click will create the certificate in your keychain and login keychain that is linked with your private key. You will see those two are hooks together.
9. The same thing you have to do for the production certificate.

your certificate will be in `~/library/MobileDevice`

### APP ID

After the certificates, we need an App ID as well.

1. Go to identifiers here https://developer.apple.com/account/resources/identifiers/list
2. Press the + button next to the Identifiers title
3. Choose App ID -> App
4. Fill Description and add the Bundle ID -> ai.flyland.app -> Register

### Get the identifier of your phone to be able to run your app in your device

Register your device with apple so apple knows which device test your application 

Those devices are stored in Devices section https://developer.apple.com/account/resources/devices

1. Register your device into that devices tab before you create you profile
2. Connect your device into your mac
3. Go to finder and tap your device
4. Click iPhone 13 Pro and copy that UUID
5. Go into devices section and add that UUID with a name to your account.

You can achieve the same using xcode.

### Create Development Profile

1. Click generate new profile
2. iOS App Development
3. Choose an APP ID (The app ID you have created)
4. Select the certificate that is this profile connected to
5. Select the devices you want
6. Give a name like |Something Dev| 
7. Download it
8. Do the same with a Distribution Profile (App store one) where you cant debug your application
9. Put hose files in the Provisioning Profiles Folder 

### Xcode

To assign the correct profiles into the app

1. Go to the ios folder of your app
2. right click and reveal in finder
3. double click on Runner.xcworkspace
Make sure that your signin of your application is done correctly
4. Click Runner top left
5. On your Targets, choose your target
6. Go to signing and capabilities -> Remove automatic signing from release and debug
7. Add dev for debug and prof for release
8. Go to build setting and make sure the development team is selected by typing in filter development team and filling all the things by choosing the team name
9. If the xcode doesnt find the developemt profile, go to keychain and see if the xcode has created one for you
10. Delete that one and restar xcode and check again
11. Press the play botton to make sure that xcode can run the code into your app

If you see any errors, run the following
```
flutter clean ios
```
which clean all it dependencies

then 
```
flutter pub get
```
then go to ios repo
```
pod install --repo-update
```

if the error keeps showing: Go to `Podfile` and change the platform version to a bigger one

### cocopoads
cocopoads is the dependencies manager application in the ios applications
```
sudo gem install cocoapods
```







