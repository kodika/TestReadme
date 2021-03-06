# Prepare your Mac

In order to be able to compile Swift iOS apps for Android you will need to have:
- Official Swift 5.4.2 Toolchain for Xcode
- Swift Android Toolchain & Gradle Plugin
- Android NDK
- JDK 8
- Precompiled Swift Mutata Libraries
- Precompiled Mutata Android Libraries
- HomeBrew, CMake and other tools


# Automated Install Steps
- Download Official Swift 5.4.2 Toolchain for Xcode from https://swift.org/builds/swift-5.4.2-release/xcode/swift-5.4.2-RELEASE/swift-5.4.2-RELEASE-osx.pkg and install it.
- If you do not have Xcode Command Line tools, run `xcode-select --install`
- Run `./scripts/01-PrepareMac.sh` to install HomeBrew, JDK 8, CMake.
- Run `./scripts/02-DownloadLatestLibs.sh` to download latest Swift Android Toolchain, Mutata Swift and Android Libraries, needed Mutata scripts.
- Run './scripts/03-DownloadNdk.sh' to download the Android NDK r21e from Google.


# Manual Install Steps
Please use the Automated Install Steps with the scripts that we have prepared to ensure that you have the correct tools.

## Official Swift 5.4.2 Toolchain for Xcode
Mutata is using the official [Swift 5.4.2](https://github.com/apple/swift/tree/swift-5.4.2-RELEASE) toolchain for Xcode which you can download from https://swift.org/builds/swift-5.4.2-release/xcode/swift-5.4.2-RELEASE/swift-5.4.2-RELEASE-osx.pkg

## Swift Android Toolchain + Gradle Plugin
In order to make the compilation of Swift and the integration with Gradle easier, readdle has created a [Swift Android Toolchain](https://github.com/readdle/swift-android-toolchain) and a [Gradle Plugin](https://github.com/readdle/swift-android-gradle).

## Android NDK
```console
cd $MUTATA_ROOT_PATH
wget https://dl.google.com/android/repository/android-ndk-r21e-darwin-x86_64.zip
unzip android-ndk-r21e-darwin-x86_64.zip
rm -rf android-ndk-r21e-darwin-x86_64.zip
```

## JDK 8
You will need JDK 8 to be able to compile the Android project.
```console
brew search openjdk
brew install openjdk@8
```

## Mutata Libraries
In order to support the iOS frameworks on Android devices, you will need to have the Mutata libraries which include.

## [Homebrew](https://brew.sh/)
```console
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## CMake and other tools
You will need to have CMake and other open-source tools to use the Mutata tools.
```console
brew install coreutils cmake wget
```
