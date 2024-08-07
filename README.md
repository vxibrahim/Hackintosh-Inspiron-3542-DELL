> :warning: This project is still in development, I am not responsible for any damage to your system.

> :warning: PLEASE READ THE GUIDE SECTION BEFORE ATTEMPTING TO USE MY EFI

# Hackintosh Inspiron 3542 DELL
EFI + GUIDE for my Dell Inspiron 15 3542 currently running MacOS monterey. Dortania's open-core guide was used to make this hackintosh. Its still a work in-progress.

![Monterey Screenshot](https://9to5mac.com/wp-content/uploads/sites/6/2022/01/install-macos-monterey-beta.jpg?quality=82&strip=all)

# INDEX
- **Hardware Info**
- What's working?
- Current issues
- **Guide**
- Tips & Advice
- Updates & Roadmap
- Acknowledgments

## Hardware Info
|Hardware|Specifications|
|----|----|
|MacOS|macOS Monterey 12|
|CPU|Intel Core i3-4005u @ 1.7Ghz|
|Graphics|Intel HD Graphics 4400 1536 MB|
|RAM|4GB DDR3L 1600MHz|
|Hard-drive|160GB WDC HDD|
|WLAN|Dell Wireless 1705|
|Ethernet|Realtek 8100|
|Touchpad|I2C Synaptics DELL|
|Keyboard|Standard PS/2 Keyboard|
|Audio|Realtek ALC225|
|Chipset|Intel 8-series|
|SMBIOS|MacbookPro 11,5| 

## What's working?

- iServices (iCloud, iMessage, Photos, etc)
- Laptop keyboard & touchpad
- GPU acceleration
- GPU vram fixed (1536mb)
- Ethernet
- USB 3.0 port

## Current issues

- WLAN not working due to dropped support for Dell Wireless 1705 after macOS 10.12
- Bluetooth not working (no BT card)
- Excessively long boot-up time
- Keyboard sometimes not working after sleep
- 2/3 USB ports not working (Not mapped yet)

# Guide 

> Before you start, please verify you are using the Inspiron 15 3542 with the exact same specifications as mine, which are listed in the Hardware Info section above. 

> :warning: If the specs don't match theres a 99% chance that the hackintosh won't work properly in that case you are on your own, you are welcome to use my EFI and modify it to your needs and I wish you goodluck.

Lets start! THIS GUIDE IS ORIENTED FROM A WINDOWS USER PERSPECTIVE PLEASE KEEP IT IN MIND.

Skip to 3 if you have already configured ur USB and recovery folder.

**WHAT YOU WILL NEED BEFORE USING MY EFI**
- Access to a working Windows, Mac or Linux machine with internet to configure your efi.
- Access to a 4gb or larger USB drive.
- Access to ethernet connection as DW1705 WLAN card is not supported.
- Basic knowledge on how to use your computer, github and googling simple issues.
- [Python](https://www.python.org/downloads/) installed
- [ProperTree](https://github.com/corpnewt/ProperTree) to edit your config.plist file
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to add proper configuration for your Hackintosh
- [OpencorePKG](https://github.com/acidanthera/OpenCorePkg/releases) to create your USB.
- [Rufus](https://rufus.ie/en/) if you have a USB which is 16gb or larger.
- [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html#prerequisites) to assist you with making of hackintosh.

**1. Creating the usb installer**

To create your usb installer

   - If you have a 4GB or <16gb USB, open File Explorer and format the USB with FAT32 partition
   - If you have a 16gb or larger USB, download and install [Rufus](https://rufus.ie/en/) and format your USB using it.
        - Set Boot selection as Not bootable
        - Set Partition scheme to GPT
        - Set File system as FAT32 or LargeFAT32
   - Once formatted, head into the USB drive and delete autorun files.
   - [If you want a even more detailed guide on setting up the USB or are on Mac or Linux, open this.](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)

**2. Grabbing OpencorePKG and setting up USB**

- Head into the [OpencorePKG github](https://github.com/acidanthera/OpenCorePkg/releases) and download the latest RELEASE.zip.
- Unzip the release, go into utilities/macrecovery and click next to the current folder path and type cmd to open a Command Prompt in the current directory.
- Once CMD is opened and execute this command 
`python3 macrecovery.py -b Mac-FFE5EF870D7BA81A -m 00000000000000000 download`
- Files will download in your macrecovery folder, you need to copy the following files depending on which ones you have
    - BaseSystem.chunklist *OR* RecoveryImage.chunklist
    - BaseSystem.dmg *OR* RecoveryImage.dmg
- Open your USB drive and make a folder named `com.apple.recovery.boot` and place those 2 files in it

The first part is done! Now leave this folder alone and continue with the rest of the guide. If you want more detail refer to [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html#prerequisites)

**3. Configuring my EFI folder and CONFIG.PLIST file**

Now this comes the part where you use my EFI folder. Follow this step-by-step now.

- First grab my EFI folder from this repository and place it in your USB along with `com.apple.recovery.boot` folder.
- Download [ProperTree](https://github.com/corpnewt/ProperTree), head into the folder and open ProperTree.bat if on Windows or ProperTree.command on macOS.
- Press CMD/Ctrl+O, navigate into EFI/OC folder in your USB drive and open `config.plist`
- Press CMD/Ctrl+Shift+R and select your OC folder to take a clean snapshot
    - For troubleshooting later on you can CMD/Ctrl+R to add onto your config file and keep your previous entries.
- After the snapshot is  taken, save the file.
- Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and open it, choose **Generate SMBIOS** option.
- Enter `Macbookpro 11,5` and hit enter. Copy the Serial, Board serial, SmUUID and AppleROM values.
- Head back into the `config.plist`, scroll down to PlatformINFO > Generic
    - Press on **MLB** and replace its value with your **Board Serial** value
    - Press on **ROM** and replace its value with your **AppleRom** value
    - Press on **SystemProductName** and replace its value with `Macbookpro11,5`
    - Press on **SystemSerialNumber** and replace its value with your **Serial** value
    - Press on **SystemUUID** and replace its value with your **SmUUID** value
- Save the config.plist file and exit

**4. Boot into the USB**

The hard part is done! Now plug your USB in and install the macOS. This is as far as this guide will go. From here refer to these parts of Dortania Guide to assist you.

|Guide Part|Link|
|----|----|
|Installation Guide|https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work |
|General Troubleshooting|https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/troubleshooting.html#table-of-contents|
|POST INSTALL|https://dortania.github.io/OpenCore-Post-Install/|

I'll give a few outlines on what to do when you've booted into the set-up screen.

- Plug your ethernet cable in your laptop, as its mandatory to install MacOS. Select Safari from menu and open any website to verify if its running.
- Exit Safari and select disk utility. In the view menu, choose show all devices. Highlight the drive that you want to install macOS to. Click erase, change the name as you want, (Mac SSD, etc.) use APFS format, with GUID partition scheme. Wait until the process finishes. You can close disk utility now, and select install macOS. The process is now the same as you would do on a Mac.
- After the first reboot, OC will start the installer on your internal disk, you should see a black screen with an Apple logo, and a progress bar, it can take up to 30 minutes.
- After the setup, your computer will reboot again, and you should see the welcome setup. Finish it and now you have a working macOS, although we have to do some work, to make the OS bootable without the USB disk.

Outline of booting without USB (my way) [POST INSTALL]
- Make sure ur USB is plugged in, open it and copy the EFI folder from it and place it on your desktop
- Open up terminal and enter `diskutil list`
- Locate your EFI partion disk identifier and remember it
- Enter `sudo diskutil mount **disk identifier**`
- After EFI is mounted, open your Finder, open your EFI partition and delete everything inside it
- Take your EFI folder from desktop and place in the EFI partition and you're done.


## Tips & Advice

*COMING SOON*

## Updates & Roadmap

*COMING SOON*

## Project status
✔️ UNDER DEVELOPMENT

## Acknowledgements
 - [Dortania's open-core guide](https://dortania.github.io/OpenCore-Install-Guide/)
 - [Hackintosh Discord where I went for help](https://discord.gg/u8V7N5C)
