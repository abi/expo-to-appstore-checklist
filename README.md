# Expo-to-App-Store Checklist

TODO


* add directions about adding bundleIdentifer in dev console before going to itunes connect
* make a note about SKU
* Explain how to use TestFlight
* When updating, you need to manually up the version in app.json, otherwise Apple won't let you upload two apps to the store


## PREQUESISITES

Register for the [Apple Developer Program](https://developer.apple.com/) with your Apple ID (the name associated with this Apple ID will be the app developer that shows up on iTunes). 

Write down safely:

* Apple username
* Apple password
* Apple Team ID https://developer.apple.com/account/#/membership

Note: Ensure that you don't have 2-factor authentication for your Apple ID.  --> see [this issue](https://github.com/expo/expo/issues/160)

* decide on a bundleIdentifier.  --> see [this stackoverflow question](http://stackoverflow.com/questions/11347470/what-does-bundle-identifier-mean-in-the-ios-project)
and SKU

### Gather Icons

#### App Store
* 1024px × 1024px

Expo will add icons in various sizes for your bundle so that it appropriately appears on different devices, and different contexts (like,  

### App Screenshots

You can generate these using the Simulator and Command+S to take a screenshot. You must use Window > Scale > 100% (Command+1)

* REQUIRED one iPad Pro screenshot (if, your app supports iPad).
* REQUIRED one iPhone 7 Plus screenshot.

These are the highest resolutions for iPad and iPhone.

### Expo Icons

These icons will be used in expo and are added to your exp.json file:

* 48x48 png grayscale with transparency (push notifications)
* 512x512 png file with transparency (home screen and within the Exponent app)

The 48X48 should be used for push notifications, setup like so:

```
  "notification": {
    "icon": "./assets/pathToFile.png", // Must be a .png.
  }
```

and the 512x512 is on a top-level json property called icon:

```
 "icon": "./assets/pathToFile.png", // Must be a .png.
```

### Configure Splash/Loading Screen

```
  "loading": {
    "icon": "./assets/pathToFile.png", // Must be a .png.
    "backgroundColor": "#34495e",
  }
```

# STEP 1

### Go to project directory and publish

* go into your app directory
* go into the exp.json file of your project, then add a slug like "myslug" (The  full slug will be automatically generated, so just put the very last word of the slug such as "myslug" which will be output as exp.host/@notbrent/myslug:)
```
  "slug": "rnplay"
```
* make sure your terminal is in the root directory of your app directory, then run `exp start`
* that will show a QR code, etc. and you'll see "[exp] Dependency graph loaded.". This means you're done, hit ctrl + C to stop packager


# STEP 2

### Decide on a iOS config
This is set in the exp.json file.

```
  "ios": {
    "bundleIdentifier": "identifier",
    "buildNumber": "1.0.0",
  }
```

# STEP 3

### Define a Scheme
The scheme is used for things like deep-linking. It is defined in your exp.json file.

```
  "scheme": "myrnapp"
```


# STEP 4


* build your app by doing this command from teh project root: ```exp build:status```
```
We need your Apple ID/password to manage certificates and provisioning profiles from your Apple Developer account.
? What's your Apple ID?
```

Put in your credentials for your apple developer account. [Make sure 2factor auth is turend off](https://github.com/expo/expo/issues/160)

```
? Do you already have a distribution certificate you'd like us to use,
or do you want us to manage your certificates for you? true
```

hit 1 for yes

```
? Do you already have a push notification certificate you'd like us to use,
or do you want us to manage your push certificates for you? true
```

hit 1 for yes

Then it will start to build your ipa file

when it is done, you'll see this message and the packager/process will exit/end:

```
[exp] Building...
[exp] Build successfully started, it may take a few minutes to complete. Run "exp build:status" to monitor it.
```


### Waiting for IPA file to download...

* run `exp build:status` to check on status. keep doing this until eventually it will return the URL
* copy paste that URL into your browser, it should automatically download the ipa file
* this file is what you will upload to the apple store


### General TODOs

Decide on app description, keywords, title and categories:

https://developer.apple.com/app-store/product-page/

### iTunes Connect

* Go to iTunes Connect.
* Go to My Apps.
* Click the plus button to create a "New iOS App".
* Select iOS Checkbox.
* Name field for your New App is permanent after submission. Pick what you want carefully.
* Select English for "Primary Language".
* Select your Bundle ID.
* SKU is a unique ID (you pick it). e.g. NameOfApp0.1
* Click Create


### iOS App 1.0 Prepare for Submission

* Choose File > Your iPhone screenshot from the prerequisite section.
* Click iPad button above screenshot preview.
* Choose File > Your iPad screenshot from the prerequisite section.
* Click Save (top right)
* Description is required.
* Keywords are required.
* Support URL is required (your website or github).
* Ignore "Build" for now and scroll down to "General App Information".

### General App Information section

* App Icon > Choose File > Your 1024x1024px icon from prerequisite section. MAKE SURE YOU UPLOAD JPG NOT PNG FOR THIS ICON
* Click edit next to "Rating". Fill out questionnaire. Be careful, it's easier to get approved if you don't select "Made For Kids". Click Done.
* Copyright (your business name) required.
* Address information is required.

* now, if you have not yet, download Apple's [Application Loader 3.0](https://itunesconnect.apple.com/apploader/ApplicationLoader_3.0.dmg)
* after downloading, open the app and sign in with your apple username and password
* choose "deliver app" from the options then click "next"
* a file picker will open, find you ipa file that you built earlier (via your terminal, in my case the ipa is no in my downloads)

Is your app designed to use cryptography or does it contain or incorporate cryptography? (Select Yes even if your app is only utilizing the encryption available in iOS or macOS.)

Note: When submitting to the iTunes Store, you’ll be asked whether your app uses the advertising identifier (IDFA). Because Expo depends on Segment Analytics, the answer is yes, and you’ll need to check a couple boxes on the Apple submission form. See Segment’s Guide for which specific boxes to fill in.

https://segment.com/docs/sources/mobile/ios/quickstart/#step-5-submitting-to-the-app-store

Congratulations! You have submitted your app for review.

App is now "Waiting For Review".
The next stages are:
"Preparing for Review"
"Going in Review"
"Accepted" or "Rejected"
You will receive an email for your app's approval, but it is good to check it yourself in iTunes Connect.


BASED ON: https://github.com/alex-wap/app-store
