# Secure-Pipes
This repository comes with no warranties, no instructions, and no support. I merely posted the code 
because I don't have any time to work on this project anymore. I hope someone can find the time to update, improve, manage, etc. 

This was my first macOS coding project, so please excuse "everything." I never claimed to be the world's best or even a good programmer. 

Note this last compliled successfully under macOS Big Sur. 

## Building

Build the `Secure Pipes` scheme in `Secure Pipes.xcodeproj`. The app target currently has a macOS 26.0 deployment target. The SocketRocket macOS target uses 12.0 because current Xcode versions no longer support building macOS 11 deployment targets.

```sh
xcodebuild -project "Secure Pipes.xcodeproj" -scheme "Secure Pipes" -configuration Release -destination 'platform=macOS' build
```
