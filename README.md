---
description: What the Mobile Starter Kit is and how it works.
title: Mobile Starter Kit Overview
resourceType: Documentation
author: jleach
---

# Mobile Starter Kit Overview

## TL;DR

This resource will help you successfully deliver a mobile (native or hybrid) application. While its recommended to give the document a full read - hunt and peck what you find useful.

If you're receiving a binary (IPA or APK) from a 3rd party for Enterprise deployment check out the `Signing` section to learn about how an IPA can be re-signed with our Enterprise certificates for AirWatch deployments.

If you're stuck send up a bat-signal on the `#devops-mobile-development` channel in [RocketChat](https://chat.pathfinder.gov.bc.ca)

Also, reach us on RocketChat to check your bundle ID or get developers invited to our iTunes or Enterprise account.

# Introduction

Someone in the Government of British Columbia  (BCGov) wants you to build a mobile application (either native or hybrid), and to do this, you need to wrap your head around the workflow and best practices: build, test, deploy. This guide will help you get up to speed while being as non-prescriptive as possible.

# Build

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

## Developers

Reach out to us on RocketChat (details in the tl;dr) to get iOS developers invited to the iTunes (Public or Enterprise); you won't need such invites if you're doing Android only development.

## Design (visual or otherwise)

A few key considerations right out of the gate are:
- Language - Swift, Kotlin, Objective-C, bla; and
- Look & Feel - Fonts, Colour Pallet, bla; and
- Bundle ID - Don't go rogue; let us help.

### Language

The rule of thumb here is choose a language that is well supported and easy to maintain while making it easy for the next developer to follow in your footsteps can support. For iOS roll with Swift (latest) and for Android go with Kotlin. If you're supporting a legacy application in, for example, Objective-C look talk to your product owner and see if can write new features in a more modern language.

### Look & Feel

Your design team (and maybe that is just you) should be aware of the Digital Services' [Design System](https://developer.gov.bc.ca/Design-System/About). While it is Web focused many resources such as color pallet, fonts, accessibility, and more are very much applicable to mobile.

**Pro Tip**
The BCGov uses the [Noto Sans](https://fonts.google.com/specimen/Noto+Sans) font for digital service deliver. Don't use fonts that require a license like *Myriad Pro*

## Code Quality

A few key considerations right out of the gate are:
- LINTing - Code quality and maintainability; and
- Code Review - Don't code in a cave.

### LINTing

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

For **Android** development use the build in mechanics and best practices of Android Studio [Improve your code with lint checks](https://developer.android.com/studio/write/lint).

### Code Review

Often the project worked on at the BCGov are small consisting of one developer; if this is your situation there isn't much you can do for code reviews.

**Pro Tip**
Ask in the `#gomobile` RocketChat channel and see if another developer can do code reviews for you.

## Build System

### Android

It is recommended you leverage the OpenShift environment for automating your builds. You can run *gradle* in a Linux / Maven / Gradel container and run all your necessary tests and builds. For a sample project, check out [SecureImage for Android](https://github.com/bcgov/secure-image-android); this project will build just fine in OpenShift.

### iOS

Unlike Android, iOS applications must be build with `Xcode` which only runs on macOS machines. We are in the process of setting up a common build system for iOS projects but for the time being you'll be doing builds on your local machine.

### Hybrid

When building a hybrid system like **React Native** you'll be writing your business logic in JavaScript but you'll still need the Android SDK and iOS SDK to compile to a native binary. This means you're iOS dependency of `Xcode` on `macOS` will be your pain point and as such you'll likely be building on your local system.

**Pro Tip**
For **iOS, Android and Hybrid** make sure you check out the `Signing` section below for useful tips on deploying your application(s).

## Help

If you're stuck send up a bat-signal on the `#gomobile` channel in [RocketChat](https://reggie.pathfinder.gov.bc.ca/?intention=LOGIN#error=login_required)


# Test

Lets have that awkward conversation about testing.

```
 _______________________________
/ I don't test my code but when \
\ I do - I do it in production. /
 -------------------------------
  \
   \  /  \~~~/  \         
     (    ..     )----,      
      \__     __/      \     
        )|  /)         |\    
         | /\  /___\   / ^   
          "-|__|   |__| 
```

While some platforms / languages have a strong test culture this isn't the case for native mobile applications like iOS and (to a lesser extent) Android, especially in the private sector. In the the BCGov we're setting the bar heigh by expecting developers to write automated tests for their code. While Google can explain all the benefits of automated tests in our Enterprise environment the quick-win is maintainability; You can refactor you code and be confident you're not breaking things and new, less experienced developers, can take over your project with a safety net in place.

**Pro Tip**
If you're getting pressure to cut corners and drop automated tests push back and explain that in an Enterprise environment where applications can be very long lived automated tests are expected. Also, see LINTing above.

# Deploy

Polishing your app and shipping it feels like the 20% of the work that takes 80% of the effort. Be cool, you're almost there.

```
 ____________________________________
/ I've built my app. I'm ready to go. \
\ What next?                          /
 ------------------------------------
     \
      \
       ___
      (o o)
     (  V  )
    /--m-m-
```

Here's the TD;DR on distribution: For iOS you're going you're going to want to have the IPA signed with one of our two BCGov certificates. The first certificate is for public iTunes App Store distributions and the second is for our AirWatch Enterprise App Store. There are conditions where you can avoid signing for our Enterprise App Store, for example, if they're provided by a 3rd-party and users are expecting to trust the 3rd party's certificate.

## Code Signing

If you're building an app that complies to run natively on iOS or Android then you'll need to sign your app for production deployment. For Android this means using a `unique` key for your application while for iOS it means producing an IPA signed with either our iTunes App Store or Enterprise certificates.

To sign your compiled binary visit our [Code Signing Service](https://signing-web-devhub-prod.pathfinder.gov.bc.ca/).

**Pro Tip**
While Google Play makes signing a simple do-it-yourself process its discouraged for a few reasons: If your team looses the signing key then the Google Play version can *not* be updated. Your team will need to remove the app from sale and create a different instance; this will be a really poor experience for your users.

## Exporting Encryption

If you're going to make your app publicly available, either through Google Play or the iTunes App Store and it uses encryption that is **over 63 bytes** then you'll likely need to deal with U.S cryptography export restrictions. Here is some useful reading on the subject:

* [Export Compliance Summary - Google](https://support.google.com/googleplay/android-developer/answer/113770?hl=en)

* [Complying with Encryption Export Regulations - Apple](https://developer.apple.com/documentation/security/complying_with_encryption_export_regulations)

* [Encryption and export license for an App Store or Google Play app](https://stackoverflow.com/questions/30297727/encryption-and-export-license-for-an-app-store-or-google-play-app)

* [Cryptography Export Regulations](https://medium.com/@cossacklabs/apple-export-regulations-on-crypto-6306380682e1)

**Pro Tip**
Even if you're making your app available in the Canada Region of Google Play or iTunes Store you still need to comply with U.S. export restrictions. This is because both Apple and Google are U.S companies and the app will reside on servers in the U.S. and thus is being `exported` to users in Canada.

## Deployment

You have a few options available to distribute your application to your users:

### Enterprise

For enterprise deployments we have a private app store called **AirWatch** that is only available to BCGov employees using work phones; this services is commonly referred to as a managed device or MDMS.

Each ministry has a `delegate` who has access to AirWatch and can deploy applications their for your. Please contact the MDMS team to discuss who you AirWatch delegate is.

### Public 

If you're application is going to be made widely available then your options are the official app stores:

- Google Play
- Apple iTunes Store

A BCGov employee for your team will be setup as an applicaiton administrator in one or both of the public stores. This will allow you to upload version, track usage, and other administrative tasks.

Reach out to the administrators in the RocketChat `#gomobile` channel to get setup.

## Management

Each team is empowered to manage there own application. While some help is required such as: setting up a bundle ID; inviting developers to our developer accounts; signing for public distribution; no team will take ownership of your app.

If you've chosen to manage your own signing key for an Android app keep it safe, don't let it walk out the door, and back it up.

---

# How to Contribute

If you would like to contribute, please see our [CONTRIBUTING](CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

# License

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

```
Copyright 2019 Province of British Columbia

This work is licensed under the Creative Commons Attribution 4.0 International License.
To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.
```
