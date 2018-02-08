![wys-platform-macos](https://img.shields.io/badge/platform-macOS-lightgrey.svg)
![wys-code-shell](https://img.shields.io/badge/code-shell-yellow.svg)
[![wys-license](http://img.shields.io/badge/license-MIT+-blue.svg)](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/license.md)

# wys – WhatsYourSign (shell script version) <img src="https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/jb-img.png" height="20px"/>

**Shell script version of Patrick Wardle's awesome [WhatsYourSign](https://github.com/objective-see/WhatsYourSign)**

Works with bundles (e.g. applications, extensions etc.), binaries/executables, disk images (DMG), packages (e.g. pkg), and archives (xar, xip).

In addition to the default WhatsYourSign functionality, **wys** also performs a deep scan of a bundle, similar to **RB AppChecker Lite**, to find executable files that are unsigned, or that are codesigned differently from the main executable.

## Installation
**Note:** If you are using the macOS Finder, it's best to ignore **wys** and use Patrick's software. The **wys** version is only meant as a quick hack for users who have disabled the Finder. Since the original **WhatsYourSign** is an `appex` (Finder extension), it will not work in other file managers.

### Example: Nimble Commander
* Navigate: NC > Preferences > Tools
* Tool title, e.g.: What's Your Sign?
* Application: `/path/to/wys`
* Parameters: `%P`
* Startup Mode: Detached
* Navigate: NC > Preferences > Hotkeys > All > Tools: What's Your Sign?
* Keyboard shortcut, e.g.: CMD-SHIFT-S
* Navigate: NC > Preferences > Hotkeys > Conflicts
* Change keyboard shortcut to resolve any potential conflicts

## Beta status
* still needs testing, especially for executable deep scan

## Screengrabs

#### Application

![grab1](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app.jpg)

#### Malware application with revoked certificate

![grab2](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-malware.jpg)

#### Application with entitlements

![grab3](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-entitlements.jpg)

#### Disk image (DMG)

![grab4](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-dmg.jpg)

#### Installer package

![grab5](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-pkg.jpg)

#### Binary

![grab6](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-binary.jpg)
