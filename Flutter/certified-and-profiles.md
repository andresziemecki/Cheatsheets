# chapter 9:

See [this chapter](https://www.youtube.com/watch?v=VPvVD8t02U8&t=20910s) if you want to release your app

You need to know how to publish your app in the app store and play store

We talk previously that to release an app you need an iOS developer account.

## Certificates and profiles

When you are certified, then apple knows where the app comes from.

Then apple sign the app in their certification to be able to put it in the appstore and then download
by millios of users.

## Profiles

I'm am a developer application which sign with this profile.

There are different flavors from the application:
- development flavors
- production flavor
- etc.


The development profile is able to debug the develipment flavor

The prod is not allow to be debug.

Steps:

1. Sign apple developer program (seems to cost 100usd per year)
3. Create a certificate of iOS developer and save to disk (This create a private key)
4. To create a production certificate you need to follow similar steps but click in appstore and ihoc.
5. Once registered you need to register in which device you are going to test the application.

before trying to push the app to your phone go to your project and
``` bash
flutter clean ios
flutter pub get
# maybe you need to delete Podfile
cd ios 
pod instal --repo-update
```
## Check this medium post
https://medium.com/readytowork-org/step-by-step-guide-on-generating-an-ios-certificate-preparing-for-test-flight-and-releasing-ios-99cd2eb11067

