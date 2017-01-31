# Test Browser Compatibility
## OS / Browser List

- Windows 10, Internet Explorer 11
- Windows 10, Edge (latest)
- Windows 10, Chrome (latest)
- Windows 10, Firefox (latest)
- Windows 7, Internet Explorer 10, VirtualBox
- Android, Chrome (latest), Genymotion
- Android 5, Chrome 37, Genymotion
- Android 4.4, Chrome 30, Genymotion
- macOS, Safari (latest), VirtualBox
- iOS, Safari (latest), VirtualBox + Xcode + Simulator

#### Extended Support

- Windows 7, Internet Explorer 9, VirtualBox
- Windows 7, Internet Explorer 8, VirtualBox
- Android 4.1, Stock Browser, Genymotion
- Android 4, Stock Browser, BrowserStack or Device
- Android 4, Chrome 42, BrowserStack or Device
- macOS 10.10 Yosemite, Safari 8, VirtualBox
- iOS 8, Safari 8, VirtualBox + Xcode + Simulator

#### References

[It's March 2016 - what browsers and operating systems should we be supporting?](http://www.wiliam.com.au/wiliam-blog/its-march-2016-what-browsers-and-operating-systems-should-we-be-supporting)  
[Browser Support for 2016](http://blog.todaysmeet.com/browser-support-update-for-2016/)  
[Test on the right mobile devices](https://www.browserstack.com/test-on-the-right-mobile-devices)  
[Strategies for carrying out testing, MDN](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Testing_strategies)

## Set up the Emulators
#### Test IE and Edge with VirtualBox

1. Install VirtualBox
2. [Download](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/) .ova file with desired OS/Browser combination
3. Double click the file and import the virtual machine

#### Test on Android with Genymotion

- Set device screen to `480x800 - 120dpi` to speed up the emulator
- Set `Use virtual keyboard for text input` check box
- Install Google Chrome on Genymotion
    1. Download [Google Apps package](http://opengapps.org/)
    2. Drag & drop downloaded zip file to Genymotion and restart
    3. Open Google Play, add google account and install Chrome

## Supplement: Android Browsers List

| Version number | Code name             | Usage  | Browsers                                                                        |
|----------------|-----------------------|--------|---------------------------------------------------------------------------------|
| 2, 3           |                       | ~0%    |                                                                                 |
| 4 - 4.0.4      | Ice Cream Sandwich    | ~0.05% | Android Browser (no updates), Chrome 42 (no updates)                            |
| 4.1 - 4.3.1    | Jelly Bean            | ~0.67% | Android Browser (no updates), Chrome (latest)                                   |
| 4.4 - 4.4.4    | KitKat                | ~2.06% | WebView (Chrome 30, updatable by device manufacturer), Chrome (latest)          |
| 5, 6           | Lollipop, Marshmallow |        | WebView (Chrome 37, updatable through Google Play), Chrome (latest)             |
| 7              | Nougat                |        | WebView is provided by Chrome APK, provider can be changed in Developer Options |

Android Browser versions varies across Android versions, including patch versions.

#### References

[Android Browser versions](https://decadecity.net/blog/2013/11/21/android-browser-versions)  
[Android Dashboards](https://developer.android.com/about/dashboards/index.html)
