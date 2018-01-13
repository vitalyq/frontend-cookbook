# Set up Browsers for Testing
## OS / Browser List

- Windows 10, Internet Explorer 11
- Windows 10, Edge (latest)
- Windows 10, Chrome (latest)
- Windows 10, Firefox (latest)
- Windows 7, Internet Explorer 10, VirtualBox
- Android, Chrome (latest), Emulator
- Android 5, Chrome 37, Emulator
- Android 4.4, Chrome 30, Emulator
- macOS, Safari (latest)
- iOS, Safari (latest), Xcode + Simulator

#### Extended Support

- Windows 7, Internet Explorer 9, VirtualBox
- Windows 7, Internet Explorer 8, VirtualBox
- Android 4.1, Stock Browser, Emulator
- Android 4, Stock Browser, Emulator
- Android 4, Chrome 42, Emulator (apk)
- Android, UC Browser (latest), BrowserStack or Device
- Android, UC Browser 11.4, Emulator (apk)
- Android, Mi Browser 9, BrowserStack or Device
- Android, Samsung Internet 5, BrowserStack or Device
- macOS 10.10 Yosemite, Safari 8, VirtualBox
- iOS 8, Safari 8, Xcode + Simulator

#### References

[It's March 2016 - what browsers and operating systems should we be supporting?](http://www.wiliam.com.au/wiliam-blog/its-march-2016-what-browsers-and-operating-systems-should-we-be-supporting)  
[Browser Support for 2016](http://blog.todaysmeet.com/browser-support-update-for-2016/)  
[Test on the right mobile devices](https://www.browserstack.com/test-on-the-right-mobile-devices)  
[Strategies for carrying out testing, MDN](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies)

## Set up the Emulators
#### Test IE and Edge with VirtualBox

1. Install VirtualBox
2. [Download](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/) .ova file with desired OS/Browser combination
3. Double-click the file and import the virtual machine

#### Test on Android Emulator with Android Studio

- Create and run virtual devices from [AVD Manager](https://developer.android.com/studio/run/managing-avds.html)
- Choose `480 x 800: mdpi` devices for better performance
- Choose x86 images with Google APIs
- To download Android 4.0.3 image
    1. Open **Tools > Android > SDK Manager**
    2. In the SDK Platforms tab select Show Package Details
    3. Find Android 4.0.3 (IceCreamSandwich) section
    4. Check Google APIs Intel x86 Atom System Image and click Apply
- Chrome 42 doesn't work on x86 Android 4.0.3 image, install it on Android 4.4 from [apk](https://www.apkmirror.com/apk/google-inc/chrome/chrome-42-0-2311-111-release/chrome-42-0-2311-111-x86-android-apk-download/)
- Home button is not functional on Android 4.1 image, use Android 4.2 instead
- UC Browser from Google Play doesn't work on emulator, install it from [apk](https://www.apkmirror.com/apk/ucweb-inc/uc-browser/uc-browser-11-4-5-1005-release/uc-browser-11-4-5-1005-2-android-apk-download/)
- Some browsers don't have x86 builds available and should be tested with a real device

## Supplement: Android Browsers List

| Version number | Code name             | Usage  | Browsers                                                                        |
|----------------|-----------------------|--------|---------------------------------------------------------------------------------|
| 2, 3           |                       | ~0%    |                                                                                 |
| 4 - 4.0.4      | Ice Cream Sandwich    | ~0%    | Android Browser (no updates), Chrome 42 (no updates)                            |
| 4.1 - 4.3.1    | Jelly Bean            | ~0.3%  | Android Browser (no updates), Chrome (latest)                                   |
| 4.4 - 4.4.4    | KitKat                | ~1.09% | WebView (Chrome 30, updatable by device manufacturer), Chrome (latest)          |
| 5, 6           | Lollipop, Marshmallow |        | WebView (Chrome 37, updatable through Google Play), Chrome (latest)             |
| 7              | Nougat                |        | WebView is provided by Chrome APK, provider can be changed in Developer Options |

Android Browser versions varies across Android versions, including patch versions.

#### References

[Android Browser versions](https://decadecity.net/blog/2013/11/21/android-browser-versions)  
[Android Dashboards](https://developer.android.com/about/dashboards/index.html)
