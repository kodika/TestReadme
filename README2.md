# MutataApp

## Set $MUTATA_ROOT_PATH env var

`cd` to the root of MutataApp
```console
export MUTATA_ROOT_PATH=$PWD
```

## Prepare your Mac

In order to be able to build your Swift for Android on your macOS machine you will need to install some open source programs and libraries.
You can use the `01-PrepareMac.sh` script or run the individual commands. You will need to run each step only once and only if you are missing the specific tool.


### Install Xcode Command Line tools

```console
xcode-select --install
```

### Install [Homebrew](https://brew.sh/)

```console
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install JDK 8
```console
brew search openjdk
brew install openjdk@8
```

### Install tools
```console
brew install coreutils cmake wget
```

### Download Official Android NDK r21e
```console
cd $MUTATA_ROOT_PATH
wget https://dl.google.com/android/repository/android-ndk-r21e-darwin-x86_64.zip
unzip android-ndk-r21e-darwin-x86_64.zip
rm -rf android-ndk-r21e-darwin-x86_64.zip
```



# Prepare your project

## Download Android project
Downloads the a general Android project from https://github.com/kodika/MutataRunnerApp-Android
```console
./12-CreateAndroidProject
```

## Convert your iOS Project
Please Backup/push your code or use a copy of your project before continue.

Set the **MUTATA_IOS_SOURCES_PATH** environment variable 
```console
export MUTATA_IOS_SOURCES_PATH=/path/to/your/ios/sources
```

Run `./15-ConvertIosProject.sh`
It will copy your Sources to `./out` and then will run the `swiftSelectorsRewriter` which will create some files needed to run your IBActions.
Also, will clear the project from @objc, @IBOutlets, @IBActions attributes as they cannot be compiled but are supported.
Finally, it will delete your copied AppIcon.appiconset as you need to create separate Android logo.

## Create Package.swift
In order for Mutata to compile your Swift files, uses Package.swift and Swift Package Manager.
It will also need to append some files to your final Swift Package in order to connect to Java using JNI.

### Set the MUTATA_SWIFT_MODULE_NAME environment variable with the name of your iOS app. Remove all whitespaces or replace them with underscores(_)
```console
export MUTATA_SWIFT_MODULE_NAME="MutataShowcase"
```
Run `./16-CreateSwiftPackageAndMutataFiles`
This will create a new Package.swift at `./out/AndroidProject/app/src/main/swift` which will be used automatically by gradle later to build your Swift code and include it in the Android .apk.
It will also copy 3 files needed to connect your Swift code with Mutata iOS and Android Libraries.

Finally it will create a new Package.swift in your Sources folder, which Mutata's Package.swift will depend on.


## Copy Android res default files

Run `./17-CopyAndroidResFiles.sh`


## Copy your iOS Images and xibs

Run `./18-CopyIosImagesAndXibs.sh

## Install and Run
Mutata uses gradle and adb to build and run your Android projects.

You can run `./20-InstallAndRun.sh` and wait for the app to launch on your device or emulator(TODO).

You can also manually build your debug apk with
```console
cd ./out/AndroidProject
gradle installDebug
```
and then launch it either from the home screen or 
```console
	adb shell am start -n YOUR_APPLICATION_ID/io.kodika.kodikaplayerandroid.MainActivity
```


## Update Mutata License
There are 2 types of Licenses
- Free with expiration code
- Paid without expiration code

Each license can be used only for one application id and versionName/Code

In order to activate your license you will need 
### Automatic License update
Copy your `license.json` in the root folder of MutataApp and run `19-UpdateMutataLicense.sh`

### Manual License update
Open the `AndroidAppDelegate.swift` in `./build/AndroidProject/app/src/main/swift/Sources/SwiftAndroid/AndroidAppDelegate.swift` and insert as the first line of 
```Swift 
public override func application(_ application: UIApplication, willFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]?) -> Bool
``` 
the MutataLicense

For paid 
```Swift
MutataLicense.setLicenseKey("YOUR_LICENSE")
```

For free
```Swift
MutataLicense.setLicenseKey("YOUR_LICENSE","EXPIRES")
```

For example
```Swift
MutataLicense.setLicenseKey("rHBUKbmzWp+tpPhbGPwkz2DgC4dVhEnUI8Yt0WW6c90Tapv54qR+dS1rnz7ooutX9hxkiMExCd7xriSlWQBg==")
MutataLicense.setLicenseKey("rHBUKbmzWp+tpPIBhbGPwkz2DgC4dVhEnUI8Yt0WW6c90Tapv54qR+dS1rnz7ooutX9hxkiMExCd7xriSlWQBg==","1638320461")
```

## Request your Mutata License key



