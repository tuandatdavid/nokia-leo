<details markdown="block">
  <summary dir="rtl">View device specification table</summary>
<table align="right" style="font-size:small">
  <thead><tr><th colspan="2">Nokia 6300 4G (nokia-leo)</th></tr></thead>
  <tbody>
    <tr><td>Released</td><td align="right">13 November 2020</td></tr>
    <tr><td>Model</td><td  align="right">TA-1286, TA-1287, TA-1291, TA-1294, TA-1307, TA-1324</td></tr>
  <tr><td colspan="2" align="center"><strong>Specifications</strong></td></tr>
    <tr><td>SoC</td><td align="right">Qualcomm MSM8909 Snapdragon 210<br>(4 x 1.1GHz Cortex-A7)</td></tr>
    <tr><td>RAM</td><td align="right">512MB LPDDR2/3</td></tr>
    <tr><td>GPU</td><td align="right">Adreno 304</td></tr>
    <tr><td>Storage</td><td align="right">4GB eMMC 4.5 (+ up to 32GB microSDHC card)</td></tr>
    <tr><td>Network</td><td>2G GSM, 3G UMTS, 4G LTE Cat4 150/50Mbps<br><em>+ EU (except East Ukraine, Azerbaijan, Georgia), APAC: band 1, 3, 5, 7, 8, 20<br>+ MENA, CN, Nigeria, Tanzania: band 1, 3, 5, 7, 8, 20, 28, 38, 39, 40, 41<br>+ US: band 2, 4, 5, 12, 17, 66, 71<br>+ LATAM: band 2, 3, 4, 5, 7, 28<br>+ ROW: band 1, 3, 5, 7, 8, 20, 38, 40</em><br>VoLTE &amp; VoWiFi support<br>Single or Dual SIM (Nano-SIM, dual-standby)</td></tr>
    <tr><td>Screen</td><td align="right">320 x 240 @ 167 PPI<br>2.4 inches QVGA TFT LCD, 16M colors</td></tr>
    <tr><td>Bluetooth</td><td align="right">4.0, A2DP, LE</td></tr>
    <tr><td>Wi-Fi</td><td align="right">802.11b/g/n, 2.4GHz, Hotspot</td></tr>
    <tr><td>Peripherals</td><td align="right">GPS &amp; GLONASS</td></tr>
    <tr><td>Cameras</td><td align="right">Rear: VGA, LED flash</td></tr>
    <tr><td>Dimensions<br>(HWD)</td><td align="right">131.4 * 53 * 13.7 (mm)<br>5.17 * 2.09 * 0.54 (in)</td></tr>
    <tr><td>Weight</td><td align="right">107.4 g (3.70 oz)</td></tr>
    <tr><td>Ports</td><td>- microUSB charging &amp; USB 2.0 data transferring port<br>- 3.5mm headphone jack</td></tr>
    <tr><td>Battery</td><td align="right">Removable Li-Ion 1500mAh (BL-4XL), 5W wired charging<br>(up to 25 days of 4G standby advertised)</td></tr>
  <tr><td colspan="2" align="center"><strong>KaiOS info</strong></td></tr>
    <tr><td>Version</td><td align="right">KaiOS 2.5.4</td></tr>
    <tr><td>WA VoIP</td><td align="right">Supported</td></tr>
    <tr><td>Build no.</td><td align="right">10.00.17.01, 12.00.17.01, 20.00.17.01, 30.00.17.01</td></tr>
  </tbody>
</table>
</details>

<p align="center">
  <img width="400" src="assets/nokia_6300_4G-emotional-Range.png">
</p>

**Table of Contents**
- [Don’t buy a counterfeit](#dont-buy-a-counterfeit)
- [Differences between US and international variants](#differences-between-us-and-international-variants)
- [Tips and tricks](#tips-and-tricks)
- [Known issues](#known-issues)
  - [KaiOS-specific](#kaios-specific)
  - [WhatsApp-specific](#whatsapp-specific)
- [Secret codes](#secret-codes)
- [Special boot modes](#special-boot-modes)
  - [UART debugging testpoint](#uart-debugging-testpoint)
- [Sideloading and debugging third-party applications](#sideloading-and-debugging-third-party-applications)
- [ROOT: Boot partition modifying (non-US only)](#root-boot-partition-modifying-non-us-only)
  - [What we’ll need](#what-well-need)
  - [Part 1: Set up environment for EDL tools](#part-1-set-up-environment-for-edl-tools)
  - [Part 2: Obtaining the boot partition](#part-2-obtaining-the-boot-partition)
    - [Nokia 8000 4G and Nokia 6300 4G with bkerler’s EDL](#nokia-8000-4g-and-nokia-6300-4g-with-bkerlers-edl)
    - [Nokia 2720 Flip and Nokia 800 Tough with andybalholm’s EDL](#nokia-2720-flip-and-nokia-800-tough-with-andybalholms-edl)
  - [Part 3: Modifying the boot partition](#part-3-modifying-the-boot-partition)
    - [Automatic patching with `8k-boot-patcher`](#automatic-patching-with-8k-boot-patcher)
    - [Manual patching with Android Image Kitchen](#manual-patching-with-android-image-kitchen)
  - [Part 4: Flashing the modified boot partition](#part-4-flashing-the-modified-boot-partition)
- [Source code](#source-code)
- [External links](#external-links)

## Don't buy a counterfeit
A lot of fake KaiOS phones, like the Nokia 8110 4G, 2720 Flip and 6300 4G are sold at many tech shops and online platforms for amazingly cheap prices; these are not the real ones, and if you were to buy them you wouldn't be able to get a refund.

Some signs that can indicate a fake KaiOS phone are:
- Price: Brand-new KaiOS phones, even after their lifespan on the shelf, don't cost less than two-thirds of their retail prices.
- Network: All KaiOS phones from HMD/Nokia Mobile have 4G LTE support. KaiOS devices are required to have at least 3G, as 2G is being phased out.
- Packaging: 8110 4G and 2720 Flip comes in semi-clear plastic boxes with flaps on both ends, while the 6300 4G comes in a solid cardboard box. Prints on the box may lack features, poor printing quality, odd grammar or spacing.
- Terrible build quality when comparing side-by-side. [To quote u/cannotelaborate on Reddit](https://www.reddit.com/r/KaiOS/comments/xglkr7/well_darn_it_i_just_received_a_counterfeit_nokia): *Build quality is horrific, the battery and SIM cards barely fit in [their trays]. It takes only like 10 seconds to boot, shows KaiOS logo briefly, then plays the old Nokia chime. Speaker quality is awful. The buttons' faces are low quality and aren't flush with the overall surface, some of them are crooked.*
- Check the country code on the information sticker under the battery. For example, if the CODE is 23BTS70**VN**00, the phone is intended for Vietnam only. You can also dial *#0000# in the OS to see the code.
- User interface: Elements are not aligned or spaced properly. KaiStore and related services should always be present on any KaiOS device.
- Apps: KaiOS does not support Java or MRE apps, and does not have Opera Mini 4.4.
- Storage: Connect the phone to a computer and see if the actual storage is much lower than the advertised one.

Remember, **only buy from trusted, reputable sources**, even if they charge more. That extra bit of price usually guarantees that you're getting a real device.

## Differences between US and international variants
"Buying Western-customized products will always give you the best quality possible" is unwise when it comes to consumer electronics, including mobile phones, and the 6300 4G is no exception. When buying the TA-1324 variant of this phone, you should expect:
- No cellular access: From the dawn of mobile phone technologies, for national security, the US has been using different cellular technologies from the rest of the world with little to no compatibility. On 4G LTE, the US variant receives different bands with little overlaps on international variants' bands, primarily band 7 (see the device specification table above). This means that you will have trouble making or receiving calls and texts on the US variant outside the country without roaming.
- Restricted device settings, notably device and T9 languages, as the phone software has to follow the FCC's regulations. On the US 6300 4G, the only languages available are English (US), español (US), Français (CA) and Português (BR). 
- Tighten device security: US 6300 4G currently cannot be rooted due to different hash signature used for EDL handshake (see [Sideloading and debugging third-party applications](#sideloading-and-debugging-third-party-applications) below).

Don't buy the US variant of 6300 4G unless you know what you're doing. Seek the availability of the phone in the closest place or nearby countries to where you are.

## Tips and tricks
- You can capture a screenshot by pressing both * and # keys at the same time.
- You don’t need a KaiOS account to use your phone or download apps from KaiStore, but you can create one in Settings, Accounts if you want to use Anti-Theft features.
- To stop getting ad notifications from KaiStore, go to Settings, Personalization, Notices, App notices, Store and turn off Allow Notices. Then go to Store, Options, Settings & Account, Show rich content and select Do not show.
  - To block KaiAds altogether, add `ssp.kaiads.com` in your Wi-Fi routers' blacklist or [the system's `hosts` file](https://ivan-hc.github.io/bananahackers/ADBlock.html). Be aware that this might prevent you from installing apps from KaiStore like WhatsApp.
- Speed Dial lets you call a contact quickly by pressing and holding a number key from 2 to 9 on the homescreen. To assign a contact to a number key, press and hold an empty key on the homescreen or go to Contacts, Options, Settings, Set Speed Dial Contacts. You can also change your voicemail number in the same menu.
  - *ICE (In Case of Emergency) Contacts, however, is an useless feature on this phone, since there's basically no way to activate it. On the 2720 Flip, you could hold or double-press the side button to trigger SOS Call.*
- You can use a GIF as your homescreen wallpaper, but it will drain your battery faster.
- If you prefer a different layout than the default 3-by-3 grid view, you can choose Options, List view/Single view and rearrange the items as you like.
- This phone has a hidden screen reader feature that might not work well with some third-party apps that have unlabeled buttons. To turn on the hidden Readout feature, open Browser, go to cyan-2048.github.io/kaios_scripts, use D-Pad to move the cursor and select *Screen Reader*.
- There's also a hidden call recording feature that has been made available on KaiOS 2.5.2 and later. To toggle, connect the phone to a WebIDE session (see [Sideloading and debugging third-party applications](#sideloading-and-debugging-third-party-applications)), then open *Device Settings* in the right sidebar, search for `callrecording.mode` and set it to either `on` (press D-Pad Left to record), `auto` or `off`.
  - Alternatively you can sideload [CrossTweak](https://gitlab.com/suborg/crosstweak) and press 3 to toggle call recording.

## Known issues
- The multiple clips holding the back panel can be stressed and quickly broken. Speaker is decent, but muffled on strong bass. *For tactile responses on keypad presses, turn on Keypad vibration under Settings, Device, Accessibility.*
  - *Note that phone shutting itself down or not receiving any charges often come down to loose or dirty battery connectors or charging port and not software problem. Happened to me once, got the phone checked and repaired for less than $10.*
- **[MAJOR]** Battery can drain heavily (from 5–7 days of 4G standby to 18 hours, or 2 hours in active usage) if you leave Wi-Fi or mobile data on at all time, e.g. to be immediately notified of incoming WhatsApp messages ⇒ workaround: turn them off if you don't plan to use Internet connection, and only turn them on periodically to check for notifications.
- **[MAJOR]** Keypad frequently registering multiple or no keystrokes instead of a single-press, because of keypad design and keypress timeout interval being too short in `keyboard.gaiamobile.org`. [BananaHackers' guide on fixing the keypad speed](https://ivan-hc.github.io/bananahackers/fix-the-keypad-speed.html) may help
- **[MAJOR]** A-GPS failing to lock your current position on 4G LTE, possibly due to interferences with TDD bands ⇒ workaround: change your A-GPS APN settings under *Settings, Mobile network & data, APN settings* or switch to 2G/3G for the phone to retrieve GPS information properly (*Settings, Mobile network & data, Carrier - SIMx, Network type, 3G/2G*). Might be major issue for those in the US where 2G/3G has been shut down.
- **[MAJOR]** B2G takes up large chunk of memory, and RAM optimizations leading to the phone joining Doze deep sleep immediately and aggressive task killing after a few minutes, making opening or exiting apps horribly slow, and notifications—including incoming WhatsApp calls—being delayed.
  - Wi-Fi hotspot feature will stop also transmitting data packets with your other devices when you put the phone into sleep.
  - *This can be mitigated by disabling the Low Memory Killer module on /boot, which we'll mention in [Manual patching with Android Image Kitchen](#manual-patching-with-android-image-kitchen) below.*
- Normally, you can wake up the phone from sleep by either pressing the Power, Volume up or Volume down buttons, regardless of whether keyguard is in place or not. On this phone there are no volume buttons, but some of their functions, such as triggering boot modes or waking the phone up, are mapped to * and # keys respectively. This can be problematic as those keys are located close to the bottom edge of the phone and can be randomly mashed if you store the phone in your front pockets, leading to unintended screenshots.
- If you forgot your lockscreen passcode (not SIM or Anti-Theft ones), you can bypass it by holding down the top Power button, then select *Memory Cleaner* and *Deep Memory Cleaning*.
- *According to reports from GSMArena and Reddit, some call and text entries may not be registered in the log. I've not been able to replicate those during my usage however, could be related to other mentioned issues.*

### KaiOS-specific
- If you're setting up the phone for the first time with no SIM card, pre-installed apps such as WhatsApp, Facebook and Google apps may not appear in the app list or in KaiStore. After popping in a SIM, those apps will show up as normal.
  - *KaiStore will show up in all circumstances, regardless of whether there's a SIM card inserted or not.*
- This phone runs KaiOS 2.5, which itself is based on Gecko 48 from 2016, meaning without optimizations and new web technologies, some websites like Instagram and Uber just fall apart and the overall performance is unbearable.
  - No built-in Widevine DRM decoders, which means the phone is NOT capable of playing DRM-protected content from e.g. Spotify
- **[MAJOR]** Some built-in apps, such as Call logs, Contacts or Music, are written in a way that is performance-intensive and not optimized for the phone, causing slow rendering and system lags if you store a large number of contacts (technically infinite but 100 recommended), call logs (max 40), music files or other items in a list. 
  - *Performance issues has been addressed on later versions, for now you should opt for alternatives such as [arma7x's K-Music](https://github.com/arma7x/kaimusic) in KaiStore if possible.*
- **[MAJOR]** Sending text messages don't automatically convert to MMS in group chats. You'll have to add a message subject or file attachment before sending to manually do so, otherwise your message will be sent separately to each individual in the thread. Receiving works flawlessly. *Group messaging over MMS has been properly implemented as a feature on later versions.*
- **[MAJOR]** Alarms can be delayed, unable to go off or go off unexpectedly if the Clock app is killed. Before going to sleep, make sure to open the Clock app and lock the phone without pressing the End call key or closing the app.
- Predictive typing mode doesn't last between inputs, meaning if you switch between input boxes, it'll return to the normal T9 mode.
- You cannot change message notification tone or alarm tone on the phone outside the defaults provided. This is because both are not managed by the system, but by the Messages and Clock app themselves.
  - To change them, you'll have to use ADB to pull `sms.gaiamobile.org` and `clock.gaiamobile.org` from `/system/b2g/webapps`, extract, edit the audio files and repackage the apps, then push them back under `/data/local/webapps` and edit the `basePath` in `/data/local/webapps/webapps.json` to reflect the change (see [BananaHackers' guide](https://ivan-hc.github.io/bananahackers/clock-alarms.html#h.unmy3yif91xs) for instructions)
- D-Pad shortcuts and app shortcuts in the carousel menu (when you press Left on the home screen) are not customizable. *The former has been addressed on later versions*, but to change them on this phone you'll have to edit `launcher.gaiamobile.org`.
- Built-in email, calendar and contact syncing function with Google account may completely fail at times. Use IMAP and import contacts instead.
  - T9 search in Contacts app is missing. For those missing the feature, there's a port called [FastContact](https://gitlab.com/suborg/fastcontact) by Luxferre that you can sideload to use as an alternative.
  - E-Mail app lacks many crucial enterprise features, such as OAuth2 secure sign-in.
  - Speaking of built-in Calendar app, if you manage to opt for syncing your Google account with the phone, only the calendar *with your email address as its name* will sync.
 
### WhatsApp-specific
- 8MB download/5MB upload limit: This is to avoid 'out of memory' errors with the nature of WhatsApp's end-to-end encryption. All things sent through the app's servers—including photos and videos—are encrypted on device. Decrypt them bit-by-bit would use too much memory for KaiOS devices, having only as much as 512MB of RAM.
- Pairing account with the WhatsApp Web interface or desktop applications is NOT possible. This is because KaiOS cannot hold background processes or handle battery life well enough to sync decryption keys and mirrors messages & calls from the phone.
  - Note that you cannot sign into another device, pair with WhatsApp Web and then sign into WhatsApp on KaiOS. This will cause the decryption keys to be renewed and all other devices to be logged off automatically.

## Secret codes
*Tip: You can save these codes as contacts for quick dialing later. When the phone suggests a saved code, you'll have to press Call to activate the code's function.*

- `*#*#33284#*#*`: Toggle debugging mode, allowing the phone to be accessed with ADB and DevTools. A bug icon will appear in the status bar letting you know debugging mode is on. This can also be turned on under Settings, Device, Developer, Debugger, ADB and DevTools.
- `*#06#`: Display the hidden International Mobile Equipment Identity numbers or IMEI(s) to uniquely identify a specific cell phone on GSM networks. Do not show them to anyone else: they're crucial for calling functions on the phone.
- `*#0606#` (TA-1324 only): Display the Mobile Equipment Identifier numbers or MEID(s) to uniquely identify a specific cell phone on CDMA networks. On international variants the MEIDs would be all zeroes, and thus this secret code doesn't apply.
- `*#0000#`: Display device information, such as firmware version, build date, model number, variant and CUID.
- `*#33#` (call): Check the [Call barring](https://www.communityphone.org/blogs/call-barring) service status from carrier for blocking or whitelisting calls, whether incoming or outgoing, domestic or international. Requires a 4-digit passcode to use. To toggle, go to Settings, Network & Connectivity, Calling, Call barring.
- `*#43#` (call): Check the [Call waiting](https://en.wikipedia.org/wiki/Call_waiting) service status from carrier. To toggle, go to Settings, Network & Connectivity, Calling, Call waiting.
- `*#*#372733#*#*`: Open KaiOS MMI Test, an internal tool to test hardware performance of a KaiOS device through an automatic routine or manually by hand, including LCD backlight, T9 keyboard, camera, LED flash, RTC, speaker, microphone, vibrator, 3.5mm audio jack, SIM trays, Wi-Fi, Bluetooth, NFC, microSD and microUSB slots etc.
  - Throughout the manual speaker test, you'll hear some English and Chinese dialog from a female speaker, which transcribes to: *Hello. Please dial 110 for police, 119 for fire, 120 for ambulance, 122 for traffic accidents, and dial area code before 112 for six full obstacles.* [?]

### Codes that don't work
Most of these codes requires `userdebug` or `eng` versions to work.
- `*#07#`: Check the `ro.sar.enabled` property, if enabled check the current SAR level and display SAR-related health and safety information.
- `*#1219#`: Clear all userspace customizations, presumably for store display.
- `*#091#` (on)/`*#092#` (off): Toggle auto-answering on incoming call. This can be turned on via Device Settings interface in WebIDE.
- `*#2886#`: Should also open KaiOS MMI Test interface.
- `*#8378269#`/`*#*#2637643#*#*`: Open Testbox engineering menu with predecessor Firefox OS design, usually used by OEMs to test various hardware of the phone. This menu can be manually opened using Luxferre's [CrossTweak](https://gitlab.com/luxferre/crosstweak).
- `###2324#`: Open a menu, allowing to toggle Qualcomm diagnostic mode for fixing null/invalid IMEI or baseband via QPST.
- `*#*#212018#*#*`: Toggle privileged access (including rooted ADB shell) to the phone.
- `*#7223#`: Display internal firmware build and boot image versions.
- `*#*#0574#*#*`: Open LogManager utility which allows you to fully enable ADB and DevTools on Spreadtrum devices.
- `*#573564#`: Open T2M Log (jrdlog), a brief LogManager interface.
- `*#1314#`: Switch the `auto.send.crash.sms` property, whose purpose is still unknown.

## Special boot modes
- **Recovery mode**: With the device powered off, hold the top Power button and the * key, or type `adb reboot recovery` when connected to a computer. Allows you to factory reset the device by wiping /data and /cache, view boot and kernel logs, and install patches from `adb sideload` interface or SD card.
- **Fastboot mode**: Only accessible and automatically kick in when both /boot and /recovery is corrupted. Allows you to restore partitions under `fastboot` interface.
- **EDL mode**: With the device powered off, hold the top Power button and both the * and # keys, or type `adb reboot edl` when connected to a computer. Boots into a black screen, allows you to read and write partitions in low-level with proprietary Qualcomm tools. Remove the battery to exit.

<details markdown="block">
  <summary>What the heck is EDL mode?</summary>

---
**Qualcomm Emergency Download mode**, commonly known as EDL mode, is a special engineering interface implemented on devices with Qualcomm chipsets. It lets you do special operations on the phone that only the device manufacturer can do, such as unlocking the bootloader, read and write firmwares on the phone's filesystem or recover from being a dead paperweight. Unlike bootloader or Fastboot mode, system files needed by the EDL mode resides on a separate 'primary bootloader' that aren't affected by software modifications. 

Aleph Security has a deep-dive blog post into exploiting the nature of EDL mode on Qualcomm-chipset devices that you can read [here](https://alephsecurity.com/2018/01/22/qualcomm-edl-1).

Booting into this mode, the phone's screen will briefly show the 'enabled by KaiOS' logo, then turn almost black as if it's off, but in fact it's still listening to commands over Qualcomm's proprietary protocol called Sahara (or Firehose on newer devices). With a [suitable digitally-signed programmer in MBN/ELF file format](https://edl.bananahackers.net) and some instruction-bundled tools, the most popular one being QFIL (Qualcomm Flash Image Loader), one can send commands from a computer to the phone over USB.

---
</details>

You can also **force reboot** the phone by holding the top Power button and the # key at any time.

EDL programmer for the international version of this phone (not TA-1324) can be found on BananaHackers' [EDL archive site](https://edl.bananahackers.net/loaders/8k.mbn) with hardware ID 0x009600e100420029 (a copy is available here). The US version of this phone has been signed with a different PK_HASH and needs a different firehose loader which we currently don't have in archive.

### UART debugging testpoint
As discovered by atipls on Discord, on the mainboard of the 6300 4G, there are 3 UART testing points: RX, TX and GND just above the SIM2 slot. Shorting TX and GND takes you to Fastboot and Linux terminal interface.

![Mainboard of a TA-1307 Nokia 6300 4G, with the red arrow pointing to three gold contacts in the middle of the board, those being the UART testpoints in the order of RX, TX and ground](assets/testpoint.png)

## Sideloading and debugging third-party applications
BananaHackers' definitions put this phone and most other KaiOS 2.5.4 devices in the first category, which means that you can install and debug apps from outside sources, but with a few caveats: apps with 'forbidden' permissions, such as `embed-apps`, `embed-widgets` and `engmode-extension` cannot be sideloaded, and you cannot debug apps that came with the device using WebIDE's Developer Tools (you can, however, see the system's global warnings and errors with `adb logcat`).

For detailed instructions, see [Sideloading and debugging/WebIDE](https://github.com/minhduc-bui1/nokia-leo/wiki/Sideloading-and-debugging).

**Do note that OmniSD, one of the methods used for on-device sideloading, and many Gerda-related apps requires the `navigator.mozApps.mgmt.import` API that has been removed from KaiOS 2.5.2.2, and therefore no longer work on this phone.** However, the Privileged factory reset feature that could be used on KaiOS 2.5.2 and older can now be activated after permanent rooting to gain privileged userspace session (see [Next steps](#next-steps)).

To remove unwanted apps from the phone, you can use [this fork of Luxferre's AppBuster](https://github.com/minhduc-bui1/AppBuster) which lets you disable any apps you don't need and enable them again if you want.

## ROOT: Boot partition modifying (non-US only)
On KaiOS 2.5.4 devices, such as the 6300 4G and 8000 4G, ADB and WebIDE can be used to install most third-party apps. However, apps with special ‘forbidden’ permissions are not allowed, including most BananaHackers apps with `engmode-extension` like Wallace Toolbox, which can be used to gain exclusive access of the phone. You also cannot make changes to the system. On the 2720 Flip and 800 Tough with KaiOS 2.5.2.2, with HMD/Nokia Mobile changing their release branches from `dev-keys` to `release-keys`, the situation is even worse as you cannot sideload at all. 

This is because in order for WhatsApp's VoIP feature to work on these KaiOS versions, a security module called SELinux is now set to be `Enforced` which checks and reverts system modifications on boot. To get total read-write access to the devices, you'll now have to permanently root them by setting SELinux to `Permissive` mode.

The guide below is based on the main guide from BananaHackers website, but has been rewritten to make it easier to follow. The process will take somewhat considerable 30 minutes to an hour, so do this when you have enough time.

> [!IMPORTANT]
> **DISCLAIMER: This process will void your phone's warranty, disable its ability to receive WhatsApp calls and over-the-air updates, but you can undo this if you save a copy of the original boot partition. However, you might also brick your phone if you make a mistake in the process, so proceed at your own risk and with caution! I won't be responsible for any damages done to your phone by following these.**
> 
> Remember, you don't have to root your phone to do things that usually need root access e.g. you can use [this fork of Luxferre's AppBuster](https://github.com/minhduc-bui1/AppBuster) to disable apps from the launcher instead of deleting them with Wallace Toolbox. You can also install [CrossTweak](https://gitlab.com/suborg/crosstweak), a Wallace Toolbox alternative also made by Luxferre that does not need `engmode-extension` and therefore can be easily installed on KaiOS 2.5.4 devices.

### What we'll need
- an international non-US version of Nokia 6300 4G (not TA-1324) or Nokia 8000 4G, Nokia 2720 Flip or Nokia 800 Tough;
- an USB cable capable of data transferring (EDL cables will also do);
- an Internet connection to download the tools needed;
- a somewhat-working firehose programmer MBN file for the [8000 4G and 6300 4G](https://edl.bananahackers.net/loader/8k.mbn), [2720 Flip](https://edl.bananahackers.net/loader/2720.mbn) or [800 Tough](https://edl.bananahackers.net/loader/800t.mbn);
- an [image file of Gerda Recovery](https://cloud.disroot.org/s/3ojAfcF6J2jQrRg/download) ([backup](https://drive.google.com/open?id=1ot9rQDTYON8mZu57YWDy52brEhK3-PGh)) for the Nokia 8110 4G, since the firehose loader above has a reading bug, we'll use this to access ADB from the recovery mode and get the boot partition from there (not needed for 2720 Flip/800 Tough);
- a EDL tools package to read and write system partitions in low-level access (in this guide we'll be using [bkerler's edl.py v3.1](https://github.com/bkerler/edl/releases/tag/3.1) for 8000 4G/6300 4G, [andybalholm's edl](https://github.com/andybalholm/edl) for 2720 Flip/800 Tough)

andybalholm's EDL cannot be used on 8000 4G and 6300 4G due to some structural changes within the GPT partition table, which will result in an error `AttributeError: 'gpt' object has no attribute 'partentries'. Did you mean: 'num_part_entries'?`. **Do note that the command structures used between bkerler's and andybalholm's are different, which we'll mention below.**

*We'll be using open-sourced Python scripts from GitHub for the sake of cross-platform usage (and my obsession of open-source tools), instead of QFIL which is proprietary and only supports Windows.*

- **Windows users also need:**
  - a computer with Python and `pip` installed for the EDL tools to work (Windows: both are packaged on Python's [official website](https://www.python.org/))
  - Qualcomm driver for your PC to detect the phone in EDL mode (included in the EDL tools)
  - [Zadig 2.7](https://github.com/pbatard/libwdi/releases/tag/v1.4.1) to configure `libusb-win32` driver
  - Android Debug Bridge (ADB) installed to read the boot image in Gerda Recovery (see [Development/WebIDE on BananaHackers Wiki](https://wiki.bananahackers.net/en/development/webide))

*@cyan-2048 confirmed to me that Zadig 2.5 bundled within the EDL package doesn't work, so **DO NOT USE** that. I've also specifically chosen version 2.7 as it works best throughout my testing, and the latest 2.8 version of Zadig tool also has troubles detecting the phone's EDL driver.*

- **macOS & Linux users also need:**
  - A package manager, such as [Homebrew](https://brew.sh), to quickly set up Python, ADB, `libusb` and configure the environment for EDL tools (setup guide with Homebrew can be found below)
  - *Python 2.7 bundled with macOS 10.8 to 12 is NOT recommended for following this guide.*

*If you're on Linux, Python and ADB can be quickly set up by installing with your built-in package manager. We won't be covering this here, as each Linux distro has its own way of installing from package manager.*

- **If you're going the automatic boot partition patching and compilation via Docker route (only recommended for 5-6 year old computers):**
  - Git to clone/download the repository of the patcher tool to your computer ([install guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git))
  - Docker Compose to provide the environment for the patcher tool to work (included in Docker Desktop, whose download links can be found [here](https://docs.docker.com/compose/install))
  - (Windows) WSL2 with [Linux kernel update package](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package) installed (to install WSL2, turn on Virtualization in BIOS, then open Command Prompt with administrative rights and type `wsl --install`)
- **If you're going the extracting and manual editing by hand route:**
  - Android Image Kitchen v3.8 ([Windows](https://forum.xda-developers.com/attachments/android-image-kitchen-v3-8-win32-zip.5300919), [macOS/Linux](https://forum.xda-developers.com/attachments/aik-linux-v3-8-all-tar-gz.5300923))
  - (Windows) [Notepad++](https://notepad-plus-plus.org/downloads) to edit the needed files while [preserving line endings](https://www.cs.toronto.edu/~krueger/csc209h/tut/line-endings.html)
  - [Java Runtime Environment](https://www.java.com/en/download) for properly signing the boot image (optional)

For the sake of simplicity, the guide assumes you've moved the Gerda Recovery image and the MBN loader file into the root of EDL tools folder, which you should do for convenience. If you'd like to have those in other folders, change the directory path accordingly.

### Part 1: Set up environment for EDL tools
> This portion of the guide was taken from [Development/EDL tools on BananaHackers Wiki](https://wiki.bananahackers.net/development/edl) so that you don't have to switch tabs. Kudos to Cyan for the guides!

#### Linux
1. Install Python from your operating system's package manager e.g.
```
sudo apt-get install python pip3
```
2. Then, open Terminal and type this to install the dependencies for EDL tools:
```
sudo -H pip3 install pyusb pyserial capstone keystone-engine docopt
``` 
3. Switch your phone to EDL mode and connect it to your computer.
  - From the turned on state, turn on debugging mode on your phone by dialing `*#*#33284#*#*`, connect it to your computer and type `adb reboot edl` in a command-line window.
  - From the turned off state, hold down `*` and `#` at the same time while inserting the USB cable to the phone.

In both cases, the phone's screen should blink with a 'enabled by KaiOS' logo then become blank. This is normal behaviour letting you know you're in EDL mode and you can proceed.

Additionally, if you have issue with device access:

- Open `/etc/modprobe.d/blacklist.conf` in a text editor and append `blacklist qcserial`.
- Copy both `51-edl.rules` and `50-android.rules` in the root of extracted EDL tools folder to `/etc/udev/rules.d`.

#### macOS
1. Follow the instructions to install Homebrew on [its homepage](https://brew.sh). Basically just open Terminal and copy the long streak of code shown on the page, and type your password when prompted.
2. While you're in Terminal, type this into the command-line:
```
brew install python android-platform-tools libusb && pip3 install pyusb pyserial capstone keystone-engine docopt
```
3. Switch your phone to EDL mode and connect it to your computer.
  - From the turned on state, turn on debugging mode on your phone by dialing `*#*#33284#*#*`, connect it to your computer and type `adb reboot edl` in a command-line window.
  - From the turned off state, hold down `*` and `#` at the same time while inserting the USB cable to the phone.

#### Windows
1. Open the Python installer and proceed with installation. Remember to tick the box next to "Add python.exe to PATH". This would make Python able to be called everywhere in the command-line instead of specifically pointing to its folder, which the next part of the guide won't cover on.

![Screenshot of an installation window for Python 3.9 showing two options, 'Install Now' and 'Customize installation', with the checkbox for 'Add Python 3.9 to PATH' being selected](assets/python.png)

2. On Windows 10/11, by default, typing the `python` or `python3` aliases within Command Prompt will call the Microsoft Store version of Python, which we don't have installed. To override this default into calling the local version of Python, head over to Settings > Apps > Apps & features > App execution aliases and toggle off both App Installer (python.exe) and App Installer (python3.exe).

<img alt="Screenshot of the Apps & features page in Windows 10's Settings app, of which the App execution aliases link is located under the Apps & features section" src="assets/settings_alias.png">
<img alt="Screenshot of the App execution alias page, where the toggles for App Installer (python.exe) and App Installer (python3.exe) are both turned off. Description says Apps can declare a name used to run the app from a command prompt. If multiple apps use the same name, choose which one to use" src="assets/alias_off.png">

3. Open Command Prompt with administrator privileges and run this command:
```
pip3 install pyusb pyserial capstone keystone-engine docopt
```
![Screenshot of a console window showing the successful process of collecting and downloading dependencies after typing the above command](assets/pythoooon.png)

4. Open the extracted EDL tools folder, go to the Windows folder under Drivers and run `Qualcomm_Diag_QD_Loader_2016_driver.exe` with administrator rights. Proceed with installation and leave everything as default, restart the computer if it prompts you to do so.

![Screenshot of an installation window for Qualcomm's diagnostic driver, in which two radio buttons are shown labelled 'WWAN-DHCP is not used to get IPAddress' and 'ETHERNET-DHCP is used to get IPAddress' respectively. The first button is selected.](assets/whatever.png)

5. Switch your phone to EDL mode and connect it to your computer.
  - From the turned on state, turn on debugging mode on your phone by dialing `*#*#33284#*#*`, connect it to your computer and type `adb reboot edl` in a command-line window.
  - From the turned off state, hold down `*` and `#` at the same time while inserting the USB cable to the phone.

In both cases, the phone's screen should blink with a 'enabled by KaiOS' logo then become blank. This is normal behaviour letting you know you're in EDL mode and you can proceed.

6. Run the Zadig tool (use the version downloaded above and NOT the one provided by the EDL package) and select *Options, List All Devices*. In the front dropdown menu, select `QHSUSB__BULK` (your device in EDL mode). In the target driver box (which the green arrow is pointing to), click on the up/down arrows until you see `libusb-win32` and click on Replace Driver.

![Screenshot of Zadig program with the Option dropdown menu shown, in which the List All Devices option is highlighted and selected](assets/listall.png)
![Screenshot of Zadig's main interface with the front dropdown list shown listing all devices connected to computer, in which the option for QHSUSB_BULK is highlighted](assets/qhsusb.png)
![Screenshot of Zadig's main interface with the second label box on the Drivers line, which the green arrow points to, showing 'libusb-win32 (v1.2.6.0)'. Two smaller up/down arrows are shown to the right of that box.](assets/arg.png)

7. If you're installing the driver for the first time, an "USB Device Not Recognised" pop-up may appear. Exit EDL mode by removing and re-inserting the battery, then turn on the phone in EDL mode again.

*As I've said above, the latest 2.8 version of Zadig might have some troubles installing the phone's EDL driver. If the driver installation takes too much time and the tool aborts it, exit Zadig, exit and re-enter EDL mode on the phone, then try to install again. If that still doesn't help, try to [download version 2.7](https://github.com/pbatard/libwdi/releases/tag/v1.4.1) instead.*

### Part 2: Obtaining the boot partition
#### Nokia 8000 4G and Nokia 6300 4G with bkerler's EDL
> Beware: due to the firehose loader being malfunctioned, the EDL tool only accepts one command each session, after which you'll have to disconnect the phone and restart the phone in EDL mode. If you try to throw a second command, it'll result in a `bytearray index out of range` error.

1. Turn on the phone in EDL mode.
2. Open the EDL tools folder in a command-line window. Flash the Gerda Recovery image to the recovery partition by typing this command:
```
python edl.py w recovery recovery-8110.img --loader=8k.mbn
```

*If the progress bar stops at 99% and you get this error `'usb.core.USBError: [Errno None] b'libusb0-dll:err [_usb_reap_async] timeout error\n'` or `usb.core.USBError: [Errno 60] Command timed out`, this is because the phone doesn't send any indicator information back to the EDL tool when in fact the image has been successfully written. Don't mind the error and proceed with the next step.*

3. When finished, disconnect the phone from your computer and exit EDL mode by removing and re-inserting the battery. 

4. Then, hold down the top Power button and `*` to turn on the phone in recovery mode. Connect the phone to your computer again.

> [!WARNING]
> Be careful not to boot into normal operation mode at this point! As stated above, while SELinux is still in `Enforced` mode, it'll try to revert all system modifications on startup, in this case, the custom recovery image we've just flashed will be overwritten by the stock one. If you accidentally start into normal mode (with the Nokia logo), you'll have to start over from step 1.

Don't worry if this boots into a white screen, you can still use ADB right after boot. This is because the display driver for the Nokia 8110 4G included in the recovery image are not compatible with the display of 8000 4G/6300 4G.

Check if ADB can recognise the phone by typing `adb devices` into the command-line.

5. Navigate the command-line to the `platform-tools` folder (if needed) and pull the boot image from the phone by typing this command:
```
adb pull /dev/block/bootdevice/by-name/boot boot.img
```
You should now see `/dev/block/bootdevice/by-name/boot: 1 file pulled, 0 skipped.` and have a copy of the boot partition with the size of 32.0MB (32,768KB). Fetched boot image will be saved to the current directory.

6. Reboot the phone into normal operation by typing `adb reboot` into the command-line, or remove and re-insert the battery. Our custom Gerda Recovery partition will now be overwritten by the default one.

You can disconnect the phone from your computer for now.

#### Nokia 2720 Flip and Nokia 800 Tough with andybalholm's EDL
Unlike the 6300 4G and 8000 4G, our phones' EDL loader properly works with both reading and writing, so the steps are more straightforward.

1. Switch your phone to EDL mode and connect it to your computer.
  - From the turned on state, turn on debugging mode on your phone by dialing `*#*#33284#*#*`, connect it to your computer and type `adb reboot edl` in a command-line window.
  - From the turned off state, hold down both side volume keys (2720 Flip) or both D-Pad Up and Down keys (800 Tough) at the same time while inserting the USB cable to the phone.

In both cases, the phone's screen should blink with a 'Powered by KaiOS' logo then become blank. This is normal behaviour letting you know you're in EDL mode and you can proceed.

2. Open the EDL tools folder in a command-line window. Extract the boot partition of the phone by typing one of these commands depend on which file you have:
```
python edl.py -r boot boot.img -loader 2720.mbn
```
```
python edl.py -r boot boot.img -loader 800t.mbn
```
3. When finished, reboot the phone into normal operation by typing one of these into the command-line, or remove and re-insert the battery:
```
python edl.py -reset -loader 2720.mbn
```
```
python edl.py -reset -loader 800t.mbn
```

You can disconnect the phone from your computer for now.

> [!WARNING]
> **Copy and keep the original boot partition somewhere safe in case you need to restore to the original state for over-the-air updates or re-enabling WhatsApp calls.**

### Part 3: Modifying the boot partition
#### Automatic patching with `8k-boot-patcher`
1. Follow [Docker's tutorial](https://docs.docker.com/compose/install/#scenario-one-install-docker-desktop) on installing Docker Desktop. Once set up, open the program, click Accept on this box and let the Docker Engine start before exiting.

![Screenshot of a window titled as 'Docker Subscription Service Agreement' which declares that you will have to accept Docker's Subscription Service Agreements, Data Processing Agreement and Data Privacy Policy in order to use the program, and the free scope of it is limited to personal and small business uses. The window also lists the options to view the full agreements, accept them or reject and close the program.](assets/docker_abomination.png)

2. Clone/download the boot patcher toolkit by typing this into a command-line window. This will download the toolkit and have Docker set it up. Do not omit the dot/period at the end of this command, this tells Docker where our downloaded toolkit are located on the system.
```
git clone https://gitlab.com/suborg/8k-boot-patcher.git && cd 8k-boot-patcher && docker build -t 8kbootpatcher .
```

![Screenshot of a macOS Terminal window showing some logs in purple text after typing the command above](assets/docker_build.png)

3. Copy the `boot.img` file we've just pulled from our phone to the desktop and do not change its name. Type this into the command-line to run the modifying process:
```
docker run --rm -it -v ~/Desktop:/image 8kbootpatcher
```

![Screenshot of a macOS Terminal window listing a list of processed files after typing the command above](assets/docker_patch.png)

That's it! On your desktop there will be two new image files, the modified `boot.img` and the original `boot-orig.img`. You can now head to [part 4](#part-4-flashing-the-modified-boot-partition).

![Screenshot of boot.img and boot-orig.img files as shown on desktop](assets/after_patch.png)

#### Manual patching with Android Image Kitchen
1. Extract the Android Image Kitchen tools and copy the boot image we've just obtained over to the root of the extracted folder.

![Screenshot of a list of folders and files contained in the extracted Android Image Kitchen folder](assets/aik.png)

2. Open the folder in a command-line window and type `unpackimg boot.img`. This will split the image file and unpack the ramdisk to their subdirectories.

![Screenshot of a Windows Command Prompt window showing some logs of the boot partition extracting process after typing the command above](assets/unpack.png)

> [!WARNING]
> **Be sure to edit the files correctly, else the phone won't boot!**

3. Let the editing begin! First, open `ramdisk/default.prop` using Notepad++ and change:
  - line 7: `ro.secure=1` -> `ro.secure=0`
  - line 8: `security.perf_harden=1` -> `security.perf_harden=0`
  - line 10: `ro.debuggable=0` -> `ro.debuggable=1`

<img width="493" src="assets/default_prop.png" alt="Screenshot of the original content of the default.prop file">
<img width="493" src="assets/default_prop_edited.png" alt="Screenshot of the modified content of the default.prop file">

4. Open `ramdisk/init.qcom.early_boot.sh` in Notepad++ and add `setenforce 0` as a new line at the end of the file.

![Screenshot of the modified content of the init.qcom.early_boot.sh file](assets/setenforce.png)

5. Go back to the root Android Image Kitchen folder and open `split_img/boot.img-cmdline` in Notepad++. Without adding a new line, scroll to the end of the first line and append `androidboot.selinux=permissive enforcing=0`.

![Screenshot of the modified content of the boot.img-cmdline file](assets/append.png)

6. Open `ramdisk/init.rc` (NOT `ramdisk/init`) and delete line 393 `setprop selinux.reload_policy 1` or mark a comment as shown. This will ultimately prevent SELinux from overwriting the policy changes we made above.

![Screenshot of the modified content of the init.rc file, with line 393 marked as comment. This has the same effects as deleting the line altogether.](assets/reload_policy.png)

7. (Optional) If you wish to disable the Low Memory Killer function, now's a good time to do so! In the same `ramdisk/init.rc` file, after line 420, make a new line and add:
```
write /sys/module/lowmemorykiller/parameters/enable_lmk 0
```
Indent the new line to match up with other lines as shown.

![Screenshot of the modified content of the init.rc file, with line 421 added to disable the Low Memory Killer module](assets/disable_lmk.png)

8. And that's a wrap! Open the root Android Image Kitchen folder in a command-line window and type `repackimg` to package our modified boot partition.

![Screenshot of a Windows Command Prompt window showing some logs of the boot partition repacking process after typing the above command, but has a signing error at the end](assets/repack_unsigned.png)

*If you happen to encounter an error during the signing process, that's likely because the process uses `java` to power the `boot-signer.jar` sequence and you don't have it installed. The image will still be packaged and ready for flashing, but if you're a perfectionist, you can install JRE and try again.*

![Screenshot of a Windows Command Prompt window showing some logs of the fully successful boot partition process](assets/repackimg_signed.png)

If the newly packaged image is barely over 1/3 the size of the original image, it's a normal behaviour and you can proceed.

### Part 4: Flashing the modified boot partition
1. Turn on your phone in EDL mode and connect it to your computer.

2. Move the newly created `boot.img`, `unsigned-new.img` or `image-new.img` to the EDL tools folder and open a command-line window within it. From here type either of these commands depending on which image file you have:
```
python edl.py w boot boot.img --loader=8k.mbn
```
```
python edl.py w boot unsigned-new.img --loader=8k.mbn
```
```
python edl.py w boot image-new.img --loader=8k.mbn
```
For Nokia 2720 Flip and Nokia 800 Tough with andybalholm's EDL:
```
python edl.py -w boot boot.img -loader 2720.mbn
```
```
python edl.py -w boot boot.img -loader 800t.mbn
```
*Again, if the progress bar stops at 99% and you get a timeout error, this is because the phone doesn't send any indicator information back to the EDL tool when in fact the image has been successfully written. Don't mind the error and go on with the next step.*

3. Restart the phone to normal operation mode by typing `python edl.py reset`. And we're done!

*If you still have the original boot partition and wish to revert all the messes and damages, connect the phone to your computer in EDL mode, move the image file to the EDL tools folder, open a command-line window within it and type these one-line at a time:*
```
python edl.py w boot boot.img --loader=8k.mbn
python edl.py reset
```

![Demostration of a command-line window showing the results after typing the first command above](assets/edl_bootog.png)

#### Next steps
- Now that you've rooted your phone, to install applications with 'forbidden' permissions, connect it to a WebIDE session, then open Device Preferences by the right pane, search for `devTools.apps.forbiddenPermissions`, clear its value, then either restart the phone or hold the top Power button and choose Memory Cleaner > Deep Clean Memory to restart B2G.

![Screenshot of a WebIDE window in which the location of Device Preferences is highlighted in the right pane and the value of devTools.apps.forbiddenPermissions has been emptied](assets/devpref.png)

- If you wish to retain privileged permissions after restoring the phone to its unrooted state, before doing so, back up all data, sideload Luxferre's [CrossTweak](https://gitlab.com/suborg/crosstweak) then press # to perform a privileged factory reset — this will wipe all data of the phone and let you set up with a privileged session. This session will last until an OTA update overrides or you choose to factory reset normally yourself.
- After rooting, you can spoof SELinux's Enforced status for WhatsApp VoIP by typing these commands one-by-one into the rooted ADB shell. This will last until a restart.
```
echo -n 1 > /data/enforce
mount -o bind /data/enforce /sys/fs/selinux/enforce
```

## Source code
HMD Global/Nokia Mobile has published the device's source code for its Linux 4.9 kernel, B2G and certain third-party libraries used in this phone, which can be downloaded directly from [here](https://nokiaphones-opensource.azureedge.net/download/phones/Nokia_6300_4G_20.00.17.01_OSS.tar.gz).

Note that the source code released does not contain proprietary parts from other parties like Qualcomm.

## External links
- [Nokia 6300 4G product page](https://www.nokia.com/phones/en_int/nokia-6300-4g) on Nokia Mobile's website
- [Discussion: Nokia 6300 4G and Nokia 8000 4G](https://4pda.to/forum/index.php?showtopic=1009510) on 4PDA Forum (Russian)
- [Nokia 8000 4G and Nokia 6300 4G general discussion thread](https://groups.google.com/g/bananahackers/c/jxEC3RVMYvI) on BananaHackers Google Groups
- [Nokia 8000 4G rooting research thread](https://groups.google.com/g/bananahackers/c/8lCqP15zHXg) on BananaHackers Google Groups
- [Nokia 6300 4G (nokia-leo)](https://wiki.postmarketos.org/wiki/Nokia_6300_4G_(nokia-leo)) on postmarketOS Wiki
- [Affe Null's Bananian project repository](https://git.abscue.de/bananian/bananian), a Debian port for KaiOS devices