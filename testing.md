# Test Browser Compatibility
## Android Browsers List

| Version number | Code name             | Usage  | Browsers                                                                        |
|----------------|-----------------------|--------|---------------------------------------------------------------------------------|
| 2, 3           |                       | ~0%    |                                                                                 |
| 4 - 4.0.4      | Ice Cream Sandwich    | ~0.05% | Android Browser, Chrome 42 (no updates)                                         |
| 4.1 - 4.3.1    | Jelly Bean            | ~0.67% | Android Browser, Chrome (latest)                                                |
| 4.4 - 4.4.4    | KitKat                | ~2.06% | WebView (Chrome 30, updatable by device manufacturer), Chrome (latest)          |
| 5, 6           | Lollipop, Marshmallow |        | WebView (Chrome 37, updatable through Google Play), Chrome (latest)             |
| 7              | Nougat                |        | WebView is provided by Chrome APK, provider can be changed in Developer Options |

Android Browser versions varies across Android versions, including patch versions.

[Android Browser versions](https://decadecity.net/blog/2013/11/21/android-browser-versions)  
[Android Dashboards](https://developer.android.com/about/dashboards/index.html)

## Set up the Emulators
#### Test IE and Edge with Vagrant

1. Install VirtualBox and Vagrant
2. [Download](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/) .box file with desired OS/Browser combination
3. Copy .box to a separate folder, i.e. `win7-ie10`
4. `vagrant init "IE10 - Win7.box"` - substitute box name
5. Update `Vagrantfile`
    ```
    ### Replace these lines:
    # config.vm.provider "virtualbox" do |vb|
    #   # Display the VirtualBox GUI when booting the machine
    #   vb.gui = true
    #
    #   # Customize the amount of memory on the VM:
    #   vb.memory = "1024"
    # end

    ### With these:
    config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--vram", "48"]
    end
    ```
6. `vagrant up`

#### Test on Android with Genymotion

Install Google Chrome on Genymotion:

1. Download [Google Apps package](http://opengapps.org/)
2. Drag & drop downloaded zip file to Genymotion and restart
3. Open Google Play, add google account and install Chrome
