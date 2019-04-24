# TL;DR

This resource will help you successfully deliver a mobile (native or hybrid) application. While its recommended to give the document a full read - hunt and peck what you find useful.

If you're receiving a binary (IPA or APK) from a 3rd party for Enterprise deployment check out the `Signing` section to learn about how an IPA can be re-signed with our Enterprise certificates for AirWatch deployments.

If you're stuck send up a bat-signal on the `#gomobile` channel in [RocketChat](https://reggie.pathfinder.gov.bc.ca/?intention=LOGIN#error=login_required)


# Introduction

Someone in the Government of British Columbia  (BCGov) wants you to build a mobile application (either native or hybrid), and to do this, you need to wrap your head around the workflow and best practices: build, test, deploy. This guide will help you get up to speed while being as non-prescriptive as possible.

## Build

Here we'll go over a few tools, processes, and considerations that that will make you life easier.

```
 _______________________________
/ We know what we're building...\
\ Now what?                     /
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

### Design (visual or otherwise)

A few key considerations right out of the gate are:
- Language - Swift, Kotlin, Objective-C, bla; and
- Look & Feel - Fonts, Colour Pallet, bla; and
- Bundle ID - Don't go rogue; let us help.

**Language**

The rule of thumb here is choose a language that is well supported and easy to maintain while making it easy for the next developer to follow in your footsteps can support. For iOS roll with Swift (latest) and for Android go with Kotlin. If you're supporting a legacy application in, for example, Objective-C look talk to your product owner and see if can write new features in a more modern language.

**Look & Feel**

Your design team (and maybe that is just you) should be aware of the Digital Services' [Design System](https://developer.gov.bc.ca/Design-System/About). While it is Web focused many resources such as color pallet, fonts, accessibility, and more are very much applicable to mobile.

* ProTip: The BCGov uses the [Noto Sans](https://fonts.google.com/specimen/Noto+Sans) font for digital service deliver. Don't use fonts that require a license like *Myriad Pro*

### Code Quality

A few key considerations right out of the gate are:
- LINTing - Code quality and maintainability; and
- Code Review - Don't code in a cave.

**LINTing**

Some languages like JavaScript, for example, have huge cultural momentum behind code quality tools a.k.a LINTers while other languages like Java, Swift and Objective-C its not the case. It is **highly** recommended to use a LINTer in your project; they ensure you're code has a similar look and feel to other BCGov projects.

For **iOS** use [SwiftLint](https://github.com/realm/SwiftLint); you can find a sample config file in the `iOS` subfolder of this repository. It is recommended to add SwiftLint as a `Pod` as follow and copy the config YAML to the root of your project named as `.swiftlint.yml`; hiding the file keeps clutter down for these administrative files.

```console
 pod 'SwiftLint'
 ```

 and then call the file as needed with the following command:

 ```console
 Pods/SwiftLint/swiftlint autocorrect
 ```

 For **Android** ...

 TBD

**Code Review**

Often the project worked on at the BCGov are small consisting of one developer; if this is your situation there isn't much you can do for code reviews.

* ProTip: Ask in the `#gomobile` RocketChat channel and see if another developer can do code reviews for you.

### Build System

**Android**

It is recommended you leverage the OpenShift environment for automating your builds. You can run *gradle* in a Linux / Maven / Gradel container and run all your necessary tests and builds. For a sample project, check out [SecureImage for Android](https://github.com/bcgov/secure-image-android); this project will build just fine in OpenShift.

**iOS**

Unlike Android, iOS applications must be build with `Xcode` which only runs on macOS machines. We are in the process of setting up a common build system for iOS projects but for the time being you'll be doing builds on your local machine.

**Hybrid**

When building a hybrid system like **React Native** you'll be writing your business logic in JavaScript but you'll still need the Android SDK and iOS SDK to compile to a native binary. This means you're iOS dependency of `Xcode` on `macOS` will be your pain point and as such you'll likely be building on your local system.

* ProTip: For **iOS, Android and Hybrid** make sure you check out the `Signing` section below for useful tips on deploying your application(s).

### Help

If you're stuck send up a bat-signal on the `#gomobile` channel in [RocketChat](https://reggie.pathfinder.gov.bc.ca/?intention=LOGIN#error=login_required)


## Test

- No culture of unit testing;
- Recommended to do some sort of testing.
- Use of LINT recommended; samples rules included.
- 

## Deploy

Code Signing

- Crypto export
- Enterprise
AirWatch
Ministry Delegate

- Public

Google Play
Apple iTunes Store
Key management
Automated Deployment
App Managers





---




### How to Contribute

If you would like to contribute, please see our [CONTRIBUTING](CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

### License

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

```
Copyright 2019 Province of British Columbia

This work is licensed under the Creative Commons Attribution 4.0 International License.
To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.
```
