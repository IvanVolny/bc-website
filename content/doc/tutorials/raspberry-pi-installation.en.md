---
title: Raspberry Pi Installation
---

{{% note "warning" %}}If you already have Raspberry Pi with the original Raspbian distribution, go to the section [**Setup on Original Raspbian**]({{< relref "#setup-on-original-raspbian" >}}).{{% /note %}}

This document will guide you through installing Raspberry Pi. The tutorial is tested for Raspberry Pi 3 (Model B) but should also work for older Raspberry Pi 2.

{{% note "info" %}}Raspberry Pi is a small, affordable, single-board computer that is able to run Linux operating system. BigClown uses this system to process sensor information, actuator control, decision logic for automation, data storage, or serve as a gateway to connect cloud services.{{% /note %}}

In the following procedure, we will install the **BigClown Raspbian** Linux distribution. Raspbian is the official and most widely distributed Linux distribution for Raspberry Pi. BigClown maintains a modified version of this distribution that facilitates some steps and includes pre-installed packages that are key to BigClown.

## Requirements

* Raspberry Pi 3 (Model B)

* MicroSD card with a minimum capacity of 4 GB

* MicroSD Card Reader (+ optional SD Card Adapter)

* Ethernet cable

* Workstation or laptop

* Router (or LAN switch) with the DHCP server set up

* One of the following operating systems:

    * Windows 7, 8.x, 10 (32-bit or 64-bit)

    * macOS (tested on version 10.12.x)

    * Ubuntu (tested on version 16.04 LTS)

## SD Card Preparation

In the following steps, we will prepare a MicroSD card for Raspberry Pi. Go to one of the supported platforms:

* [**Instructions for Windows**]({{< relref "#instructions-for-windows" >}})

* [**Instructions for macOS**]({{< relref "#instructions-for-macos" >}})

* [**Instructions for Ubuntu**]({{< relref "#instructions-for-ubuntu" >}})

## Instructions for Windows

1. Insert the MicroSD card into the card reader.

2. Download the current version of the **BigClown Raspbian** image:

    {{% download "Download from GitHub" "https://github.com/bigclownlabs/bc-raspbian/releases" %}}

3. Unzip the downloaded image.

    {{% note "info" %}}You can use the [**7-Zip**](http://www.7-zip.org) tool for this step.{{% /note %}}

4. Write the downloaded image `bc-raspbian-VER-armhf-rpi.img` to the MicroSD card (replace `VER` with the actual version of the downloaded image).

    {{% note "info" %}}You can use the [**Win32 Disk Imager**](https://sourceforge.net/projects/win32diskimager/files/latest/download) tool for this step.{{% /note %}}

    {{% note "warning" %}}The **Win32 Disk Imager** must run with the operating system administrator rights.{{% /note %}}

5. Insert the Micro SD card to the Raspberry Pi.

6. Connect the Ethernet cable to the Raspberry Pi.

7. Connect the USB power adapter to the Raspberry Pi.

8. Log in to the Raspberry Pi using SSH. Detailed procedure is provided in the document [**Raspberry Pi Login**]({{< relref "doc/tutorials/raspberry-pi-login.en.md" >}}).

## Instructions for macOS

1. Insert the MicroSD card into the card reader.

2. Download the current version of the **BigClown Raspbian** image:

    {{% download "Download from GitHub" "https://github.com/bigclownlabs/bc-raspbian/releases" %}}

3. Open the `Terminal` application and go to the folder with the downloaded image, e.g.:

        cd ~/Downloads

4. Unzip the downloaded image (replace `VER` with the actual version of the downloaded image):

        unzip bc-raspbian-VER-armhf-rpi.zip

5. Search for the disk identifier (it looks like `/dev/diskX`):

        diskutil list

6. You must unmount the disk (replace `X` with the correct disk identifier):

        diskutil unmountDisk /dev/diskX

7. Write the downloaded image to the MicroSD card (replace `VER` with the actual version of the downloaded image and `X` with the correct disk identifier):

        sudo dd if=bc-raspbian-VER-armhf-rpi.img of=/dev/rdiskX bs=1m

    {{% note "info" %}}`sudo` means the process will run with the administrator's rights and may ask for the your password (if you have such privileges).{{% /note %}}

    {{% note "warning" %}}This process may take several minutes.{{% /note %}}

    {{% note "warning" %}}If you encounter the error message `Permission denied`, please make sure you MicroSD card is not write-protected (e.g. by a switch on the MicroSD card adapter).{{% /note %}}

8. Eject the MicroSD card from the operating system (replace `X` with the correct disk identifier):

        diskutil eject /dev/diskX

9. Insert the Micro SD card to the Raspberry Pi.

10. Connect the Ethernet cable to the Raspberry Pi.

11. Connect the USB power adapter to the Raspberry Pi.

12. Log in to the Raspberry Pi using SSH. Detailed procedure is provided in the document [**Raspberry Pi Login**]({{< relref "doc/tutorials/raspberry-pi-login.en.md" >}}).

## Instructions for Ubuntu

1. Insert the MicroSD card into the card reader.

2. Download the current version of the **BigClown Raspbian** image:

    {{% download "Download from GitHub" "https://github.com/bigclownlabs/bc-raspbian/releases" %}}

3. Open the `Terminal` application and go to the folder with the downloaded image, e.g.:

        cd ~/Downloads

4. Unzip the downloaded image (replace `VER` with the actual version of the downloaded image):

        unzip bc-raspbian-VER-armhf-rpi.zip

5. Search for the disk identifier (it looks like `/dev/sdX`):

        lsblk

6. You must unmount the disk (replace `X` with the correct disk identifier):

        sudo umount /dev/sdX?

    {{% note "info" %}}`sudo` means the process will run with the administrator's rights and may ask for the your password (if you have such privileges).{{% /note %}}

7. Write the downloaded image to the MicroSD card (replace `VER` with the actual version of the downloaded image and `X` with the correct disk identifier):

        sudo dd if=bc-raspbian-VER-armhf-rpi.img of=/dev/sdX bs=1M status=progress

    {{% note "warning" %}}This process may take several minutes.{{% /note %}}

    {{% note "warning" %}}If you encounter the error message `Permission denied`, please make sure you MicroSD card is not write-protected (e.g. by a switch on the MicroSD card adapter).{{% /note %}}

8. Eject the MicroSD card from the operating system (replace `X` with the correct disk identifier):

        eject /dev/sdX

9. Insert the Micro SD card to the Raspberry Pi.

10. Connect the Ethernet cable to the Raspberry Pi.

11. Connect the USB power adapter to the Raspberry Pi.

12. Log in to the Raspberry Pi using SSH. Detailed procedure is provided in the document [**Raspberry Pi Login**]({{< relref "doc/tutorials/raspberry-pi-login.en.md" >}}).

## Differences from the Original Raspbian

This is a brief list of differences:

* Hostname is `hub` instead of `raspberrypi`.

* The time zone is set to `Europe/Prague`.

* The following records were added to the repository APT list:

    * **https://repo.bigclown.com**

    * **https://apt.dockerproject.org/repo**

* By default, these packages are also installed:

    * mosquitto

    * mosquitto-clients

    * docker

    * htop

    * git

    * python3.4

    * python3-paho-mqtt

    * python3-venv

    * python3-pip

    * bc-common

    * bc-gateway

    * bc-workroom-led-strip

    * bc-workroom-blynk

## Setup on Original Raspbian

{{% note "warning" %}}Apply the following procedure only if you are using Raspberry Pi, on which the original Raspbian distribution is running. This is an alternative way of installing the previous procedure.{{% /note %}}

1. Log in to the Raspberry Pi using SSH. Detailed procedure is provided in the document [**Raspberry Pi Login**]({{< relref "doc/tutorials/raspberry-pi-login.en.md" >}}).

2. Install these dependencies:

        sudo apt install apt-transport-https wget

3. Add the BigClown APT repository to the resource list:

        sudo sh -c 'echo "deb https://repo.bigclown.com/debian jessie main" > /etc/apt/sources.list.d/bigclown.list'

4. Add the PGP key of the APT repository:

        wget https://repo.bigclown.com/debian/pubkey.gpg -O - | sudo apt-key add -

5. Update the package index and upgrade the packages:

        sudo apt update && sudo apt upgrade

6. Now you can install the individual packages:

    * Basic package for the Smart LED Strip (Workroom) project:

            sudo apt install bc-workroom-gateway

    * LED strip plugin for the Smart LED Strip (Workroom) project:

            sudo apt install bc-workroom-led-strip

    * Blynk plugin for the Smart LED Strip (Workroom) project:

            sudo apt install bc-workroom-blynk

## WiFi Setup on Raspberry Pi 3

The Raspberry Pi version 3 has added the ability to connect to a WiFi network.

The connection procedure is as following:

1. Open the file for editing `wpa_supplicant.conf`:

        sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

2. Paste into the file the following template and edit the appropriate items:

        network={
            ssid="wifi_network_name"
            psk="wifi_network_password"
        }

4. Save the file (`Ctrl+X`) and confirm the file name (`y` + `Enter`).

5. Restart the Raspberry Pi:

        sudo reboot

6. Log in and verify using the `iwlist` command, that the connection is active.

## Related Documents

* [**Raspberry Pi Login**]({{< relref "doc/tutorials/raspberry-pi-login.en.md" >}})