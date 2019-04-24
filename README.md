# TL;DR

This resource will help you successfully deliver a mobile (native or hybrid) application. While its recommended to give the document a full read - hunt and peck what you find useful.

If you're stuck send up a bat-signal on the `#gomobile` channel in [RocketChat](https://reggie.pathfinder.gov.bc.ca/?intention=LOGIN#error=login_required)

# Introduction

Someone in the BC Government wants you to build a mobile application (either native or hybrid), and to do this, you need to wrap your head around the workflow and best practices: build, test, deploy. This guide will help you get up to speed while being as non-prescriptive as possible.

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
- Language - Swift, Kotlin, Objective-C, bla
- Look & Feel - Fonts, Colour Pallet, bla.
- Bundle ID - Don't go rogue; let us help.

**Language**

The rule of thumb here is choose a language that is well supported and easy to maintain while making it easy for the next developer to follow in your footsteps can support. For iOS roll with Swift (latest) and for Android go with Kotlin. If you're supporting a legacy application in, for example, Objective-C look talk to your product owner and see if can write new features in a more modern language.

**Look & Feel**

Your design team (and maybe that is just you) should be aware of the Digital Services' [Design System](https://developer.gov.bc.ca/Design-System/About). While it is Web focused many resources such as color pallet, fonts, accessibility, and more are very much applicable to mobile.

ProTip: The Government of British Columbia uses the [Noto Sans](https://fonts.google.com/specimen/Noto+Sans) font for digital service deliver. Don't use fonts that require a license like *Myriad Pro*

### Tek. Stack




### Build System
- Build locally
- Working on build system
- Can use on-line systems but they can *not* be given any credentials like signing keys.

### Help
- Where to go for help.
- PR
- Code review



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
