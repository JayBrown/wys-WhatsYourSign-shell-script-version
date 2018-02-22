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
