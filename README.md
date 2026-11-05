# Secure-Pipes
This repository comes with no warranties, no instructions, and no support. I merely posted the code 
because I don't have any time to work on this project anymore. I hope someone can find the time to update, improve, manage, etc. 

This was my first macOS coding project, so please excuse "everything." I never claimed to be the world's best or even a good programmer. 

Note this last compliled successfully under macOS Big Sur. 

## Local network access

Secure Pipes connects to SSH servers directly, including servers on a private LAN. Its `Info.plist` declares `NSLocalNetworkUsageDescription` so macOS can explain and request Local Network access. If a LAN connection fails while the same SSH command works in Terminal, check **System Settings → Privacy & Security → Local Network** and allow Secure Pipes. This is separate from SSH authentication.

For SOCKS proxy connections, the configured local port must also be free. For example, if `ssh -D 1234 ...` is already running, Secure Pipes cannot also listen on `localhost:1234`; stop the other tunnel or choose another local port. Secure Pipes sets OpenSSH's `ExitOnForwardFailure` for SOCKS connections so a listener bind failure terminates the SSH process instead of leaving an SSH session that looks like a working proxy.

## Notifications

The **Use Notification Center for connection status updates** preference enables connection alerts. Secure Pipes uses macOS User Notifications and requests alert permission when notifications are enabled; if permission was denied, allow them under **System Settings → Notifications → Secure Pipes**. The app must be code-signed with a stable Apple Development identity for macOS to honor its notification permission; an ad-hoc-signed build may be rejected even when an older Secure Pipes entry is enabled. Clicking a connection-failure notification opens the connection's error details. Canceling a connection that never reached the connected state does not send a misleading "disconnected" notification.

## Building

Build the `Secure Pipes` scheme in `Secure Pipes.xcodeproj`. The app target currently has a macOS 26.0 deployment target. The SocketRocket macOS target uses 12.0 because current Xcode versions no longer support building macOS 11 deployment targets.

```sh
xcodebuild -project "Secure Pipes.xcodeproj" -scheme "Secure Pipes" -configuration Release -destination 'platform=macOS' build
```
