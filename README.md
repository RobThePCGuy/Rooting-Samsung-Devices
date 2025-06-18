# A Comprehensive Guide to Rooting Samsung Galaxy Devices

This guide provides a detailed, step-by-step process for rooting modern Samsung devices using Magisk and Odin. It is intended for users who have some experience with flashing custom firmware.

**This is a high-risk procedure.** Please read the entire guide carefully before starting.

## Table of Contents

  - [Disclaimer](/README.md#disclaimer)
  - [What is Rooting?](/README.md#what-is-rooting)
  - [Prerequisites](/README.md#prerequisites)
      - [Hardware & Setup](/README.md#hardware--setup)
      - [Required Software](/README.md#required-software)
  - [Step-by-Step Guide](/README.md#step-by-step-guide)
      - [Step 1: Enable OEM Unlocking](/README.md#step-1-enable-oem-unlocking)
      - [Step 2: Download the Official Firmware](/README.md#step-2-download-the-official-firmware)
      - [Step 3: Unlock the Bootloader](/README.md#step-3-unlock-the-bootloader)
      - [Step 4: Create the Patched AP File](/README.md#step-4-create-the-patched-ap-file)
      - [Step 5: Flash the Patched Firmware with Odin](/README.md#step-5-flash-the-patched-firmware-with-odin)
      - [Step 6: Factory Reset from Recovery](/README.md#step-6-factory-reset-from-recovery)
      - [Step 7: Finalize the Magisk Installation](/README.md#step-7-finalize-the-magisk-installation)
  - [Troubleshooting & FAQ](/README.md#troubleshooting--faq)
  - [Acknowledgements](/README.md#acknowledgements)

-----

## Disclaimer

> **IMPORTANT:** Rooting your device carries inherent risks. This process will **void your warranty**, trip the Knox security fuse permanently, and may prevent certain security-sensitive apps (like banking apps) from functioning correctly. By following this guide, you acknowledge that you are proceeding at your own risk. **I am not responsible for any data loss, device damage ("bricking"), or any other issues that may arise.** Be responsible for your actions and follow each step with precision.

## What is Rooting?

Rooting is the process of gaining privileged control (known as "root access") over an Android device's operating system.

  - **Pros:** Allows for deep customization, removal of bloatware, installation of specialized apps, and full device backups.
  - **Cons:** Voids warranty, introduces security vulnerabilities if not managed properly, and can lead to device instability.

## Prerequisites

### Hardware & Setup

  - A Windows PC.
  - The Samsung device you intend to root.
  - A high-quality USB data cable.
  - A complete backup of your device's data, as **this process will erase everything**.
  - A stable Wi-Fi internet connection for the initial device setup.

### Required Software

Download and place these tools in a dedicated folder for easy access.

1.  **Magisk:** [Download the latest APK from the official GitHub](https://github.com/topjohnwu/Magisk/releases).
      * *Alternative:* [KitsuneMagisk](https://github.com/1q23lyc45/KitsuneMagisk/releases).
2.  **Odin:** [Patched Odin 3.14.1](https://xdaforums.com/attachments/odin3-v3-14-1_3b_patched-zip.5158507/) (A patched version is often required for custom binaries).
3.  **Samsung USB Drivers:** [Download from Samsung's Developer Portal](https://developer.samsung.com/galaxy/others/android-usb-driver-for-windows).
4.  **Firmware Downloader:** [SamloaderKotlin Bifrost](https://github.com/zacharee/SamloaderKotlin/releases).

## Step-by-Step Guide

### Step 1: Enable OEM Unlocking

1.  Navigate to **Settings** > **About phone/tablet** > **Software information**.
2.  Tap on **Build number** seven (7) times consecutively until you see the "Developer mode has been turned on" message.
3.  Go back to the main **Settings** menu and enter the new **Developer options**.
4.  Find and toggle on **OEM unlocking**.
    > **Note:** If this option is missing, your device may not be unlockable (e.g., some US carrier models), or you might need to wait several days after activating the device. Ensure your software is up to date.

### Step 2: Download the Official Firmware

Samsung's servers now require device-specific information to download firmware. `SamloaderKotlin Bifrost` helps with this.

1.  Extract the `Odin3-*.zip` and `bifrost-*.zip` archives.
2.  Run `Bifrost.exe` from the `/bin` folder of its extracted directory.
3.  Enter your device's **Model** number (e.g., `SM-X910`).
4.  Select the appropriate **Region** code (e.g., `XAR`). This should match the `Service provider software version` on your device's **Software information** screen.
5.  Enter your device's **Serial Number** or **IMEI**.
6.  Click **Check for Updates** and then **Download**.
7.  Save the firmware zip file in your Odin folder.

### Step 3: Unlock the Bootloader

> **WARNING:** This step will perform a factory reset and erase all data on your device.

1.  Power off your device completely.
2.  Press and hold both the **Volume Up** and **Volume Down** buttons simultaneously.
3.  While holding the buttons, connect the device to your PC with the USB cable.
4.  Continue holding the buttons until a light blue "Warning" screen appears. This is **Download Mode**.
5.  On this screen, long-press the **Volume Up** button to unlock the bootloader.
6.  You will be asked for confirmation. Press **Volume Up** again to confirm.
7.  The device will reboot and automatically initiate a factory reset.
8.  Once it boots to the "Welcome!" screen, complete the initial setup. **You must connect to Wi-Fi.**
9.  After setup, re-enable **Developer options** and verify that **OEM unlocking** is grayed out and enabled. This confirms the bootloader is unlocked.

### Step 4: Create the Patched AP File

1.  Once the firmware download is complete, extract the firmware `.zip` file. You will see several files starting with `AP`, `BL`, `CP`, and `CSC`.
2.  Connect your device to your PC.
3.  Copy two files to your device's internal storage (e.g., the `Download` folder):
      * The firmware file that starts with `AP_...` (it's the largest one).
      * The `Magisk.apk` file.
4.  On your device, open a file manager, locate `Magisk.apk`, and install it (you may need to grant permissions).
5.  Open the Magisk app.
6.  In the top card, tap **Install**.
7.  Choose the **Select and Patch a File** option.
8.  Navigate to and select the `AP_...` file you copied earlier.
9.  Magisk will patch the file. This may take a few minutes.
10. Once complete, a new file named `magisk_patched-[version]_[random_chars].tar` will be in your device's `Download` folder.
11. Copy this `magisk_patched-*.tar` file back to the Odin folder on your PC.

### Step 5: Flash the Patched Firmware with Odin

1.  Reboot your device into **Download Mode** using the same method as in Step 3 (Power off -> Hold Vol Up + Vol Down -> Connect USB).
2.  When the warning screen appears, press **Volume Up** once to enter Download Mode.
3.  On your PC, run `Odin3.exe` as an administrator.
4.  In Odin's **Options** tab, ensure **Auto Reboot** is **UNCHECKED**.
5.  Load the firmware files into their respective slots:
      * Click **BL** and select the `BL_...` file.
      * Click **AP** and select the `magisk_patched-*.tar` file.
      * Click **CP** and select the `CP_...` file.
      * Click **CSC** and select the `CSC_...` file.
    > **Important:** **DO NOT** use the `HOME_CSC_...` file. Using the regular `CSC` file is necessary to wipe the device correctly for this process.
6.  Once the files are loaded and your device is detected (the `ID:COM` box will be blue), click **Start**.

### Step 6: Factory Reset from Recovery

The device will not reboot automatically. We must do it manually to enter recovery.

1.  Wait for Odin to display a green **PASS** message.
2.  Unplug the device. Press and hold the **Power** + **Volume Down** buttons to force a reboot.
3.  The moment the screen turns black, **immediately** switch to holding **Power** + **Volume Up**.
4.  Continue holding until the Android Recovery screen appears. (If you miss the timing, the device may bootloop and enter recovery on its own after a few attempts).
5.  In recovery, use the volume buttons to navigate and the power button to select. Choose **Wipe data/factory reset** and confirm.
6.  Once the wipe is complete, select **Reboot system now**.

### Step 7: Finalize the Magisk Installation

1.  The device will reboot to the "Welcome!" screen. Complete the initial setup again, including connecting to Wi-Fi.
2.  Once on the home screen, copy the `Magisk.apk` to your device one last time and install it.
3.  Open the Magisk app. It will show a pop-up stating "Additional Setup Required."
4.  Tap **OK**. The app will perform its final steps, and the device will automatically reboot one last time.

After the reboot, open Magisk. If everything is green, congratulations! Your device is now successfully rooted.

-----

## Troubleshooting & FAQ

  * **Odin doesn't detect my device.**
      * Ensure the official Samsung USB drivers are installed correctly. Try reinstalling them.
      * Use a different USB port (preferably a USB 2.0 port on the back of your PC).
      * Try a different, high-quality USB cable.
  * **My device is stuck in a bootloop.**
      * You likely need to re-flash the stock firmware. Download the original firmware again and flash all original `AP`, `BL`, `CP`, and `CSC` files in Odin (with `Auto Reboot` checked this time) to restore your device. Then, attempt the guide again, paying close attention to every step.
  * **SafetyNet fails / My banking app doesn't work.**
      * This is an expected consequence of rooting. In Magisk settings, enable `Zygisk` and configure the `DenyList` to hide root from specific apps. This may not work for all apps.
  * **The "OEM Unlocking" option is missing.**
      * This usually means your device has a locked bootloader that cannot be unlocked (common for devices sold by US carriers like Verizon or AT&T). There is no workaround for this.

## Acknowledgements

This guide would not be possible without the incredible work of the following developers and communities:

  * **topjohnwu** for creating Magisk.
  * **The XDA-Developers community** for tirelessly testing and sharing knowledge.
  * The developers of Odin, SamloaderKotlin, and other essential tools.
