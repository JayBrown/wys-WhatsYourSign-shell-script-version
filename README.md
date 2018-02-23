![wys-platform-macos](https://img.shields.io/badge/platform-macOS-lightgrey.svg)
![wys-code-shell](https://img.shields.io/badge/code-shell-yellow.svg)
[![wys-license](http://img.shields.io/badge/license-MIT+-blue.svg)](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/LICENSE)

# wys – WhatsYourSign (shell script version) <img src="https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/img/jb-img.png" height="20px"/>

**wys is a shell script variant of Patrick Wardle's awesome [WhatsYourSign](https://github.com/objective-see/WhatsYourSign).**

Full functionality including signature verification is available for bundles (e.g. app, kext, framework), binaries/executables, disk images (DMG, sparsebundle, sparseimage), package archives (pkg, xip, xar). Basic functionality, e.g. checksum verification, is available for any and all regular files.

**wys** is actually "WhatsYourSign Extended". In addition to the default functionality, **wys** also

* generally works on mounted volumes, i.e. in `/Volumes` or other user-defined mount points (e.g. `smb` mounts etc.), i.e. you can safely scan a file or application on its mounted DMG volume before copying it,
* prints the file size (B, MB, MiB) for regular files (data size) and directories (size on disk),
* prints the download source domain names, so the user can detect potential temporary redirects,
* verifies DMG checksums and prints disk image information on DMGs, sparsebundles and sparseimages,
* verifies a signed bundle for modified files with `codesign`,
* compares a file hash (checksum) stored in the clipboard with the hash calculated for the local file (regular files only),
* checks the calculated hash (file or executable) against the VirusTotal database for malware detection (optional),
* verifies code signing certificates (CSCs) against the current revocation list using `security` and accounts for potentially spoofed code signatures,
* verifies installer package signing certificates (IPSCs) against the current revocation list using `security` and accounts for potentially spoofed signatures,
* compares the CFBundleIdentifier with the identifier in the code signature,
* creates a local sqlite database of any scanned CFBundleIdentifier and the associated SKID in the CSC, and compares successive scan data with the saved data,
* prints Gatekeeper `spctl` assessment (packages: `install`; other: `execute`) and the associated source information,
* prints a CSC's timestamp or signing time (depending on the signature),
* prints an IPSC's signing timestamp and creator from a package's TOC,
* deep-scans a bundle to find
  * executable files that are unsigned, or
  * that have a different code signature than the main executable, and
* permanently writes the scan results to log files (optional, recommended).

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
* Create a free online account at **[VirusTotal](https://www.virustotal.com)**;
* in your browser navigate: VirusTotal > Account > Profile > API Key;
* copy the key and configure **wys** accordingly (*see below*).

### Notes
* It probably helps to set OCSP and CRL to "Best attempt" in **macOS Keychain Access** > Preferences > Certificates.
* The SKID comparison will occasionally produce false warnings, because a SKID (a certificate's **Subject Key Identifier**) can change for perfectly valid reasons, for example because the developer of a software has
  * renewed an expired certificate,
  * sold his product to another developer, or
  * received a new certificate (e.g. after company rebranding etc.).
* VirusTotal results can also produce false warnings, depending on the antivirus software involved; examples are:
  * **BBEdit:** VEX189B.Webshell (Bkav);
  * false positives like applications with `libswiftDispatch.dylib` marked as MacOS.BitCoinMiner-AS (Avast, AVG).

## Scan options

### Command line operation and configuration
* Move, copy or (best practice) symlink **wys** from the cloned repository into your `$PATH`, e.g. to `/usr/local/bin/wys`, then configure using the CLI options.
* The following command line options and arguments are available:

```
wys [<file(path) 1> ... <file(path) n>]		scan filepath(s) or file(s) from the command line

Options:

--init		initialize wys
--silent	force silent mode for current scans
--status	print wys configuration status

--config [report | silent | vt <key>]		modify wys configuration file
	report		toggle logging
	silent		toggle silent mode
	vt <key>	enter VirusTotal API key

--help		this help page
```

### Alternative configuration (GUI usage)
* Run **wys** at least once to create the default wys configuration file, then
* run the command `open -a TextEdit ~/.wys/config` to open the config file, or open it manually.

#### Enable logging
* In the **wys config file** replace `report=no` with `report=yes` and **save**.
* Logs will be stored in `~/Library/Logs/wys` and will be accessible via Apple's **Console** application.

#### Silent mode
* In the **wys config file** replace `silent=no` with `silent=yes` and **save**.
* **wys** will scan silently in the background and only log the SKIDs and (if logging is enabled) the scan results.

#### VirusTotal API key
In the **wys config file** look for the line that begins with `vtkey=`, paste the API key behind the `=` (equals sign) without whitespace, and **save**.

## Uninstall
To uninstall, you need to remove the following files:

* **wys** itself,
* the wys GitHub directory (if you have cloned it),
* the invisible directory `~/.wys`, which contains the config file, the SKID database, the wys icon, and the `./bin` directory with the `abspath` CLI), and
* `~/Library/Logs/wys`, which contains the log files.

Temporary files in `/tmp` will be automatically removed by **wys** after every scan, and potential detritus will be removed at macOS boot.

## [Screengrabs](https://github.com/JayBrown/wys-WhatsYourSign-shell-script-version/blob/master/screengrabs.md)

## Beta status
* still needs general testing, lots of testing
* timestamp information in Info.plist? (research) … approximate signing/creation time?
* deep scan: parse CodeResources to thoroughly check for modified and unverified/added files (v1.1)

## Thank you
* Patrick Wardle (for the original **WhatsYourSign** and all his other great security tools)
* lososik (feature ideas & testing)
* Daniel Beck (`abspath`)
