Terrarium - Live QML Editor and Viewer
=========

![Doge](http://www.terrariumapp.com/images/doge.png)

Terrarium is a cross platform QML Playground: the view renders lively as you type in the editor, makes prototyping and experimenting with [QtQuick](http://qt.digia.com/qtquick/) a lot more fun!  

It monitors changes in its `TextEdit`, and triggers the view to reload source from the local http server. If you're looking for a file system watcher implementation, please refer to [QML LiveReload](https://github.com/penk/qml-livereload). 

### More details on http://terrariumapp.com

## Download

* [iOS](https://itunes.apple.com/us/app/terrarium/id891232736?ls=1&mt=8)
* [Android](https://play.google.com/store/apps/details?id=com.terrariumapp.penk.Terrarium)
* [Mac OSX](http://goo.gl/EqEGvT)
* [Ubuntu Linux](https://launchpad.net/~penk/+archive/touch/+files/terrarium_1.2.1_amd64.deb)
* [Ubuntu Touch](http://goo.gl/jyoVwm)

## Build Instructions

    git clone https://github.com/penk/terrarium-app.git
    cd terrarium-app && git submodule init && git submodule update 
    qmake && make 

## Platform Specific Instructions

### For Mac OSX/iOS

To add icons to iOS build, first generate and open `Terrarium.xcodeproj`, switch AppIcon to use [Assets Catalog](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/Recipe.html), then replace `Terrarium/Images.xcassets/` directory with `platform/ios/Images.xcassets`. 

As for Mac OSX, refer to `macdeployqt` command in `terrarium-app.pro` file. 

__NOTE:__

Remember to add `CFBundleInfoDictionaryVersion` into your `Info.plist` if it's not auto generated by qmake:

    <key>CFBundleInfoDictionaryVersion</key>
    <string>6.0</string>

Otherwise you'll get **Invalid Bundle Structure** error when submit to App Store, as [described here] (http://stackoverflow.com/questions/24194582/invalid-binary-error). 

### For Ubuntu Desktop/Phone

If you're using Qt packages from apt archive instead of [qt-project.org](http://download.qt-project.org/) releases, here's the dependencies: 

    sudo apt-get install qt5-qmake qt5-default qtbase5-dev qtdeclarative5-dev build-essential

All `debian/` package information can be found under `platform/ubuntu/` directory, copy it to current path and build the package by:

    cp -r ubuntu/debian . 
    dpkg-buildpackage -b 

If you're building click package, execute following command on device (for native compile):

    cp platform/ubuntu/* . 
    click build . 

And install it

    click install ./com.ubuntu.developer.penk.terrarium_0.4_armhf.click
    click register --user=phablet com.ubuntu.developer.penk.terrarium 0.4

### For Android 

First generate your keystore by `keytool`, then:

    ~/Qt5/5.3/android_armv7/bin/qmake
    make 
    make install INSTALL_ROOT=../android-terrarium

Copy `platform/android/AndroidManifest.xml` and `platform/android/res` to `../android-terrarium`, build and sign apk by: 

    ~/Qt5/5.3/android_armv7/bin/androiddeployqt --input \
        android-libTerrarium.so-deployment-settings.json \
        --output ../android-terrarium --release --sign ../TerrariumApp.keystore TerrariumApp

## Screenshots 

* [Android 4.4.2](http://i.imgur.com/771i80V.png)
* [iOS 7.1](http://i.imgur.com/NezPpL9.png)
* [Mac OSX 10.9](http://i.imgur.com/iEoTDLa.png)
* [Ubuntu Touch](http://i.imgur.com/NPlxNx0.png)
* [Ubuntu 14.04](http://i.imgur.com/lrMH7OY.png)

## LICENSE 

Copyright © 2014 Ping-Hsun (penk) Chen <penkia@gmail.com>  
The source code is, unless otherwise specified, distributed under the terms of the MIT License. 

## CREDITS

* [DocumentHandler](https://github.com/khertan/ownNotes) by Benoît HERVIER
* [QMLHighligher](https://gitorious.org/aalperts-automatons/bragi) by Alan Alpert 
* [QHttpServer](https://github.com/rschroll/qhttpserver) by Robert Schroll
* [Font Awesome](http://fontawesome.io) by Dave Gandy 

