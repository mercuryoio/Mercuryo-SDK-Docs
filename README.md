# Mobile SDK

![Mercuryo Logo](documentation/img/logo.png "Mercuryo Logo")

Mercuryo is a Multicurrency Crypto Wallet allowing users to buy, sell, store and pay with cryptocurrency whenever they want. Besides client-facing web and mobile apps or widgets Mercuryo provides the platform for developers to create their own services on top of our API. This SDK is created to ease the process of integration of top-notch crypto experince to your mobile applications.

SDK is written on Koltin Multiplatform with goal to provide same shared code to both iOS and Android libraries. Despite not being a ubiquitous approach this allows us to enable all features on all platforms simultaneously. From iOS or Android developer’s standpoint integration looks similar to how you usually do it: add pod from CocoaPods for iOS or dependency in Gradle followed by calling methods as described below.

## Requirements

- Android 5.0+
- iOS 13.0+

## Installation

## Android
### Gradle

Add it in your root build.gradle at the end of repositories:

```Kotlin
allprojects {
    repositories {
        ...
        maven { url 'https://dl.bintray.com/andrey-timofeev/mercuryo/' }
    }
}
```

Add dependency:

```Kotlin
dependencies {
    implementation 'com.github.adaptyteam:AdaptySDK-Android:0.3.1'
}
```

##iOS
###CocoaPods
Add the Mercuryo-SDK pod into your Podfile and run pod install.
```ruby
    target :YourTargetName do
      pod 'Mercuryo-SDK'
    end
```

### Manual Installation
1. [Download archive](https://github.com/mercuryoio/iOS-SDK/archive/main.zip) and extract the zip.
2. Drag `MercuryoSDK.xcframework` into your project.
<img src="https://raw.githubusercontent.com/mercuryoio/iOS-SDK/main/images/copy_into_project.png" width="281" height="278">
3. Select "Copy items if needed" and click Finish.
<img src="https://raw.githubusercontent.com/mercuryoio/iOS-SDK/main/images/copy_dialog.png" width="438" height="271">
4. Don’t forget to change Embed property for MercuryoSDK.xcframework on “Embed & Sign”. This can be found in the “Frameworks, Libraries, and Embedded Content” section of your target’s “General” tab.
<img src="https://raw.githubusercontent.com/mercuryoio/iOS-SDK/main/images/setup_guide.png" width="661" height="374">


## Usage

– [Quickstart](documentation/getstarted_en.md)
- 🔓 Authentication [EN](documentation/session_en.md) | [RU](documentation/session.md)
- 🗄 Wallets [EN](documentation/wallet_en.md) | [RU](documentation/wallet.md)
- 💰 Operations (buy/sell/withdraw crypto)  [EN](documentation/operations_en.md) | [RU](documentation/operations.md)
- 💳 Cards [EN](documentation/cards_en.md) | [RU](documentation/cards_ru.md)

## Reference

SDK models [EN](documentation/models_en.md) | [RU](documentation/models.md)
