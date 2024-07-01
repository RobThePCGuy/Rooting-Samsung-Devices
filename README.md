# Rooting Samsung Devices

## Words of Caution
This guide assumes you have some experience with rooting and flashing firmware. Proceed with caution, and only attempt this on your own personal devices. Remember, rooting can void warranties and potentially brick your device. I am not responsible for any damages or losses that may occur. Be responsible for your actions, and follow each step carefully.

## Prerequisites
- **Windows PC**
- **Recent backup of your tablet**, as all existing data will be erased.
- **Internet access via Wi-Fi**, necessary for OEM unlocking.

### Software Requirements
1. [Magisk](https://github.com/topjohnwu/Magisk/releases) or [Kitsune Mask](https://github.com/HuskyDG/magisk-files/releases) (a Fork of Magisk)
2. [Patched Odin 3.14.1](https://xdaforums.com/attachments/odin3-v3-14-1_3b_patched-zip.5158507/)
3. [Samsung USB Driver](https://developer.samsung.com/galaxy/others/android-usb-driver-for-windows)
4. [SamloaderKotlin Bifrost](https://github.com/zacharee/SamloaderKotlin/releases)

## Step-by-Step Guide

### Step 1: OEM Unlock
1. Go to **Settings** > **About**.
2. Tap **Software Information**.
3. Tap **Build Number** seven times or until you see an acknowledgment that you have enabled Developer Options.
4. Go back to **Settings** and find **Developer Options**.
5. Locate **OEM Unlock** and enable it. If it is not there, either your device does not support this method or you need to update to the latest software and factory reset the device.

### Step 2: Download Decrypted Firmware
Samsung now requires a matching IMEI or serial number to be sent with firmware requests.
1. Unzip the `Odin3-*.zip` and `bifrost-*.zip`.
2. Run the extracted `Bifrost.exe` inside the bin folder.
3. Input the Model (e.g., SM-X610).
4. Select the Region from the dropdown (match it to your Software Information page, e.g., XAR).
5. Enter your serial number or IMEI into the field.
6. Click 'Check for Updates' to find the latest firmware files.
7. Once it locates the firmware, save it into the Odin folder you extracted earlier.

### Step 3: Unlock the Bootloader
While the firmware downloads, let's unlock the bootloader.

1. If attached, remove the USB cable from the device.
2. Power off the device using the traditional method.
3. Once powered off, press and hold both the **Volume Up** and **Volume Down** buttons while connecting a USB cable from the tablet to a PC.
4. Continue holding the two buttons until download mode appears.
5. To unlock the bootloader, press and hold the **Volume Up** button until the screen transitions.
6. It will ask you to confirm your choice by pressing **Volume Up**.
7. After you agree, the device will reboot and automatically initiate the factory reset.
8. After the reset and you're back at the 'Welcome!' screen, configure a basic setup (Wi-Fi connection required).
9. Re-enable **Developer Options** and make sure you see that **OEM Unlock** is enabled (should be grayed out).

### Step 4: Patch AP
When the download and decryption are completed, you'll have a new folder containing your firmware files specific to your device.

**Sometimes you may need to extract the zip file in order to create the flashable firmware files.**

1. Copy the firmware file that starts with 'AP_' and the APK file for Magisk downloaded from the required files section to the device via USB.
2. Once finished, open the Files app and select 'Application Files' and tap on `app-release.apk` or whatever the APK file is named.
3. Give the appropriate install permissions to install.
4. Open the newly installed app.
5. At the top, select 'Install'.
6. Then, press the radial button for 'Select and Patch a File'.
7. This will open the file browser; find the AP_ file and tap it.
It will take a few minutes to patch the AP file.
8. Once completed, copy the 'magisk_patched-` file from the Download directory of the device back to your PC so we can flash it in place of the original.

### Step 5: Install Patched Firmware
1. Run Odin and do the following:
   - Switch tabs on the left to 'Options' and untoggle the 'Auto Reboot' option.
   - Press BL and select the **BL_** file.
   - Press AP and select the **magisk_patched-** file.
   - Press CSC and select the **CSC_** file.
     - **Do not use Home_CSC** because that will not erase all the user data, which is imperative.

2. Unplug the USB from the device and power it down.
3. After a few seconds, press and hold the **Volume Up** and **Volume Down** buttons while reconnecting the USB cable from the PC to the device.
4. Continue holding the two buttons until download mode appears.
5. Press Volume Up to confirm you want to enter download mode.
6. Back on the PC, press Start to flash the device.

### Step 6: Factory Reset After Flashing
After completing the flash, we do not want the device to auto-reboot.
1. Once Odin says PASS in green, you can unplug the USB and press and hold **Power** and **Volume Down** to reboot the device.
2. When the screen blanks out, continue holding Power but switch from holding **Volume Down** to holding **Volume Up**. If done right, it'll reboot into recovery mode.
   - If not, the device will reboot a few times and boot itself into recovery automatically.
3. Select **Wipe data/factory reset**. The device will reboot on its own and take you to the Welcome! screen once finished.

### Step 7: Finalize the Root
1. Complete the initial setup. Remember, you must connect to Wi-Fi to see if **OEM Unlock** is still enabled.
2. Plug the device back into your PC and copy the `magisk.apk` app again to it.
3. Install Magisk using the method we described above.
   - This time, when we open the app, a popup will state 'Additional Setup Required'. Click OK, and the device will reboot once again.
4. After the reboot, you are now the proud owner of an unlocked bootloader that has been rooted with Magisk. Congrats!
