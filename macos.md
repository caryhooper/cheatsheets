# MacOS

## Certificate Operations
security list-keychains

## iOS
#### Extract IPA entitlements
/usr/libexec/PlistBuddy -x -c 'Print :Entitlements' provision.plist 

## Homebrew
#### Hard reset for homebrew
brew update-reset
#### Update homebrew
brew update
#### Install a package
brew install cmake
brew install libusbmuxd