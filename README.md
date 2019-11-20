# Adapty

[![Version](https://img.shields.io/cocoapods/v/Adapty.svg?style=flat)](https://cocoapods.org/pods/Adapty)
[![License](https://img.shields.io/cocoapods/l/Adapty.svg?style=flat)](https://cocoapods.org/pods/Adapty)
[![Platform](https://img.shields.io/cocoapods/p/Adapty.svg?style=flat)](https://cocoapods.org/pods/Adapty)

![Adapty: Win back churned subscribers in your iOS app](https://raw.githubusercontent.com/adaptyteam/AdaptySDK-iOS/master/adapty.png)

Adapty helps you track business metrics, and lets you run ad campaigns targeted at churned users faster, written in Swift. https://adapty.io/

## Requirements

- iOS 12.0+
- Xcode 10.2+
- Swift 5+

## Installation

### CocoaPods

1. Create a Podfile if you don't have one: `pod init`
2. Add Adapty to your Podfile: `pod 'Adapty', '~> 0.1.0'`
3. Save the file and run: `pod install`. This creates an `.xcworkspace` file for your app. Use this file for all future development on your application.

## Usage

### Configure your app and create profile first

#### Step 1: Configure your app

In your AppDelegate class:

```Swift
import Adapty
```

And add the following to `application(_:didFinishLaunchingWithOptions:)`:

```Swift
Adapty.activate("YOUR_APP_KEY")
```

#### Step 2: Register your user

```Swift
Adapty.shared.createProfile(customerUserId: "<id-in-your-system>",
                            email: "example@email.com",
                            phoneNumber: "+1-###-###-####",
                            facebookUserId: "###############",
                            firstName: "Test",
                            lastName: "Test",
                            gender: "",
                            birthday: Date) { (error) in
                                if error == nil {
                                    // successful registration
                                }
}
```

All properties are optional.  
For **`gender`** possible values are: **`m`**, **`f`**, but you can also pass custom string value.

### Update your user

Later you might want to update your user.

```Swift
Adapty.shared.updateProfile(customerUserId: "<id-in-your-system>",
                            email: "example@email.com",
                            phoneNumber: "+1-###-###-####",
                            facebookUserId: "###############",
                            firstName: "Test",
                            lastName: "Test",
                            gender: "",
                            birthday: Date) { (error) in
                                if error == nil {
                                    // successful update
                                }
}
```

All properties are optional.

### AdjustSDK integration

To integrate with AdjustSDK, just pass it's attribution to Adapty.

```Swift
Adapty.shared.updateAdjustAttribution(trackerToken: "", // the tracker token of the current attribution.
                                      trackerName: "", // the tracker name of the current attribution.
                                      network: "", // the network grouping level of the current attribution.
                                      campaign: "", // the campaign grouping level of the current attribution.
                                      adgroup: "", // the ad group grouping level of the current attribution.
                                      creative: "", // the creative grouping level of the current attribution.
                                      clickLabel: "", // the click label of the current attribution.
                                      adid: "") // the unique device identifier provided by attribution.
{ (error) in
    if error == nil {
        // successful update
    }
}
```

All properties are optional.

### Validate your receipt

```Swift
Adapty.shared.validateReceipt("<receiptEncoded>") { (response, error) in
    // response is a Dictionary, containing all info about receipt from AppStore
}
```

**`receiptEncoded`** is required and can't be empty.

## License

Adapty is available under the GNU license. [See LICENSE](https://github.com/adaptyteam/AdaptySDK-iOS/blob/master/LICENSE) for details.