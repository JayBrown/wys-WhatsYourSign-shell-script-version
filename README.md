![wys-platform-macos](https://img.shields.io/badge/platform-macOS-lightgrey.svg)
![wys-code-shell](https://img.shields.io/badge/code-shell-yellow.svg)
[![wys-license](http://img.shields.io/badge/license-MIT+-blue.svg)](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/LICENSE)

# wys – WhatsYourSign (shell script version) <img src="https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/jb-img.png" height="20px"/>

**wys is a shell script variant of Patrick Wardle's awesome [WhatsYourSign](https://github.com/objective-see/WhatsYourSign).**

It works with bundles (e.g. applications, extensions etc.), binaries/executables, disk images (DMG, sparsebundle), packages (e.g. pkg), and archives (xip & probably xar).

**wys** is actually "WhatsYourSign Extended". In addition to the default functionality, **wys** also

* generally works on mounted volumes, i.e. in `/Volumes` or other user-defined mount points (e.g. `smb` mounts etc.), i.e. you can safely scan a file or application on its mounted DMG volume before copying it,
* prints the file size (B, MB, MiB; regular files only, e.g. DMGs or zip archives),
* prints the download source domain names, so the user can detect potential temporary redirects,
* compares a hash (checksum) stored in the clipboard with the hash calculated for the local file (regular files only),
* checks the calculated hash against the VirusTotal database for malware detection,
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

**Note:** the SKID comparison will occasionally produce false negatives, because a SKID (a certificate's **Subject Key Identifier**) can change for perfectly valid reasons, for example because the developer of a software has

* renewed an expired certificate,
* sold his product to another developer, or
* received a new certificate (e.g. after company rebranding etc.).

## Installation
If you are using the macOS Finder, it's best to ignore **wys** and use Patrick's software, unless you need the extended functionality. The **wys** version is only meant as a quick hack for users who have disabled the Finder. Since the original **WhatsYourSign** is an `appex` (Finder extension), it will not work in other file managers.

### Example: Nimble Commander
* navigate: NC > Preferences > Tools
* set **Tool title**, e.g.: What's Your Sign?
* set **Application**: `/path/to/wys`
* set **Parameters**: `%P`
* set **Startup Mode**: Detached
* navigate: NC > Preferences > Hotkeys > All > Tools: What's Your Sign?
* define keyboard shortcut, e.g.: CMD-SHIFT-S
* navigate: NC > Preferences > Hotkeys > Conflicts
* if necessary, change keyboard shortcut to resolve any potential conflicts

### Usage in default macOS Finder
You can add the **wys** shell script to an **Automator** service/workflow, which will then be available in the **Services** contextual submenu; you can also assign a keyboard shortcut for it in **System Preferences**.

### VirusTotal API key
* run **wys** at least once to create the config file
* create a free online account at **[VirusTotal](https://www.virustotal.com)**
* in your browser navigate: VirusTotal > Account > Profile > API Key
* copy the API Key (*see below*: "YourVirusTotalAPIKey")
* launch iTerm or Terminal etc. and run the following command:
* `echo "vtkey=YourVirusTotalAPIKey" >> ~/.config/wys/wys.cfg`

## Uninstall
To uninstall, you need to remove the following files:

* **wys** itself
* wys GitHub directory (if you have cloned it)
* `~/.config/wys` (contains the configuration file for the VirusTotal API key)
* `~/.cache/wys` (contains the SKID database, the wys icon, and the `./bin` directory with the `abspath` CLI)

Temporary files in `/tmp` will be automatically removed by **wys** after every scan, and potential detritus will be removed at macOS boot.

## Beta status
* still needs general testing, lots of testing
* timestamp information in Info.plist? (research)
* deep scan: parse CodeResources to check for modified, missing or added files (probably)
* might need a one-line result at the top, similar to WhatsYourSign appex (probably not)

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
