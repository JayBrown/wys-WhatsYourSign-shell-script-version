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
* still needs testing, especially for executable deep scan (any misses?)
* should have a one-line result at the top, similar to WhatsYourSign appex

## Screengrabs

#### Application signed with Developer ID

![grab1](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app.jpg)

#### Malware application with revoked certificate (KeRanger)
*Notice the bogey RTF file, which is actually an executable part of the ransomware scheme.*

![grab2](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-malware.jpg)

#### Malware application with fake codesigning certificate (OSX.CreativeUpdater)
*Compare the main executable code signature (fake) with the other signature (genuine by Mozilla).*
*This malware is distributed as an app bundle within an app bundle.*

![grab13](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-malware2.jpg)

#### Application with cracked executables using proprietary code signatures

![grab7](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-cracked.jpg)

#### Application with entitlements (Apple System)

![grab3](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-entitlements.jpg)

#### Application with entitlements (Mac App Store)

![grab10](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-mas.jpg)

#### Codesigned disk image (DMG)

![grab4](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-dmg.jpg)

#### Disk image (DMG) signed with a fake code signature for malware distribution

![grab12](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-dmgfake.jpg)

#### Signed installer package

![grab5](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-pkg.jpg)

#### Codesigned binary command line interface

![grab6](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-binary.jpg)

#### Unsigned application

![grab8](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-unsigned.jpg)

#### Adhoc-signed application

![grab9](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-adhoc.jpg)

#### Signed xip archive

![grab11](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-xip.jpg)
