![wys-platform-macos](https://img.shields.io/badge/platform-macOS-lightgrey.svg)
![wys-code-shell](https://img.shields.io/badge/code-shell-yellow.svg)
[![wys-license](http://img.shields.io/badge/license-MIT+-blue.svg)](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/license.md)

# wys – WhatsYourSign (shell script version) <img src="https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/jb-img.png" height="20px"/>

**Shell script version of Patrick Wardle's awesome [WhatsYourSign](https://github.com/objective-see/WhatsYourSign)**

## Installation
**Note:** If you are using the macOS Finder, it's best to ignore **wys** and use Patrick's software. The **wys** version is only meant as a quick hack for users who have disabled the Finder. Since the original **WhatsYourSign** is an `appex` (Finder extension), it will not work in other file managers.

### Example: Nimble Commander
* Navigate: NC > Preferences > Tools
* Tool title, e.g.: What's Your Sign?
* Application: `/path/to/wys.sh`
* Parameters: `%P`
* Startup Mode: Detached
* Navigate: NC > Preferences > Hotkeys > All > Tools: What's Your Sign?
* Keyboard shortcut, e.g.: CMD-SHIFT-S
* Navigate: NC > Preferences > Hotkeys > Conflicts
* Change keyboard shortcut to resolve any potential conflicts

## Beta status
Still needs support for pkg/mpkg and xip. Already works on application bundles, DMGs, binaries etc.

## Screengrabs

![grab1](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app.jpg)
