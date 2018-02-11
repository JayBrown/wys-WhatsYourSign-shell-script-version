![wys-platform-macos](https://img.shields.io/badge/platform-macOS-lightgrey.svg)
![wys-code-shell](https://img.shields.io/badge/code-shell-yellow.svg)
[![wys-license](http://img.shields.io/badge/license-MIT+-blue.svg)](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/LICENSE)

# wys – WhatsYourSign (shell script version) <img src="https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/jb-img.png" height="20px"/>

**Shell script version of Patrick Wardle's awesome [WhatsYourSign](https://github.com/objective-see/WhatsYourSign)**

Works with bundles (e.g. applications, extensions etc.), binaries/executables, disk images (DMG), packages (e.g. pkg), and archives (xip & probably xar).

In addition to the default WhatsYourSign functionality, **wys** also:

* prints the file size (B, MB, MiB; only for single files),
* compares a hash (checksum) stored in the clipboard with the hash calculated for the local file (only for single files),
* verifies codesigning and installer package signing certificates against the current revocation list using `security`—
  * *note*: I'm assuming that it helps to set OCSP and CRL to "Best attempt" in **Keychain Access** > Preferences > Certificates—,
* compares the CFBundleIdentifier with the identifier in the code signature,
* creates a local database of any scanned CFBundleIdentifier and codesigning SKID, and compares successive scan data with the saved data,
* prints `spctl` assessment (packages: `install`; other: `execute`),
* prints the codesigning timestamp or signing time (depending on the signature),
* prints the signing timestamp and creator from a package's TOC, and
* deep-scans a bundle, similar to **RB AppChecker Lite**, to find
  * executable files that are unsigned, or
  * that are codesigned differently from the main executable.

## Installation
**Note:** If you are using the macOS Finder, it's best to ignore **wys** and use Patrick's software, unless you need the additional functionality. The **wys** version is only meant as a quick hack for users who have disabled the Finder. Since the original **WhatsYourSign** is an `appex` (Finder extension), it will not work in other file managers.

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

### Usage in default macOS Finder
You can add the **wys** shell script to an **Automator** service/workflow, which will then be available in the "Services" contextual submenu; you can also assign a keyboard shortcut for it in System Preferences.

## Beta status
* still needs general testing, incl. SKID compare, maybe some tweaking for the deep bundle scan
* needs testing for sparsebundles
* find way to compare signing time with other timestamps
* might need a one-line result at the top, similar to WhatsYourSign appex (?)

## Screengrabs

#### Checksum for installer package verified from clipboard

![grab18](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-verify.jpg)

#### Warning of SKID mismatch and certificate revocation (KeRanger)

![grab19](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-skidrevoke.jpg)

#### Application signed with Developer ID

![grab1](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app.jpg)

#### Malware application (KeRanger) with revoked certificate and SKID mismatch
*Notice the SKID mismatch, i.e. the SKID from the code signature used by the attacker differs from the original certificate by the Transmission developer.*

*Notice the bogey RTF file, which is actually an executable part of the ransomware scheme.*

![grab2](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-malware.jpg)

#### Malware application (OSX.CreativeUpdater) with fake codesigning certificate and SKID mismatch
*Compare the main executable code signature (added by attacker) with the other signature (original by Mozilla), i.e. this is a legit app bundle within a malware app bundle to fool the user.*

*Notice the bogey `script` file, which starts the download of the cryptominer malware.*

*Please note that the security assessment using `spctl` can still accept a codesigning certificate, while the more up-to-date verification with `security` already shows it as revoked.*

![grab13](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-malware2.jpg)

#### Application with entitlements (Apple System)

*Notice that there is no CRL (certificate revocation list) for Apple System signatures (leaf certificate: "Software Signing"), so let's hope none of Apple's private codesigning keys ever get leaked.*

![grab3](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-entitlements.jpg)

#### Application with entitlements (Mac App Store)

![grab10](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-mas.jpg)

#### Application with valid but expired codesigning certificate

![grab20](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-expired.jpg)

#### Application with untrusted third-party code signature and missing SKID

![grab17](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-3rdparty.jpg)

#### Adhoc-signed application with missing SKID

![grab9](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-adhoc.jpg)

#### Unsigned application

![grab8](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-unsigned.jpg)

#### Kernel extension

![grab16](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-kext.jpg)

#### Codesigned command line interface with initial SKID scan

![grab6](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-binary.jpg)

#### Codesigned disk image (DMG)

![grab4](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-dmg.jpg)

#### Malware disk image (DMG) with hash mismatch and signed with a fake code signature

![grab12](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-dmgfake.jpg)

#### Signed installer package

![grab5](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-pkg.jpg)

#### xip archive with verified hash and signed with Developer ID

![grab11](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-xip.jpg)

#### xip archive signed with locally trusted key

![grab14](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-xip-user.jpg)

#### Application with cracked executables using proprietary code signatures
*Notice that the main code signature is unchanged: the SKID comparison shows a match.*

![grab7](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-cracked.jpg)

#### Auxiliary list with unsigned executable files
*Note that some developers erroneously set the executable bits on files that do not need it; this really messes things up, and *wys* scans will take longer in these cases.*

![grab15](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/grab_wys-app-cracked-aux.jpg)
