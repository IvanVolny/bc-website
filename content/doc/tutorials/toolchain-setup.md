---
title: Toolchain Setup
---

In this document we will describe the installation of tools for working with firmware - the firmware toolchain. The toolchain is designed to allow the firmware operations on all the supported operating systems using a command line in a **uniform manner**.

{{% note "info" %}}Orientation on a command line interface has the advantage to build your firmware automatically on server, e.g. on commit to GitHub via Travis CI continuous integration service.{{% /note %}}

The firmware toolchain consists of several fundamental components:

* Compiler **GCC ARM Embedded**

* Version control system **Git**

* Interpret for scripting language **Python 3**

* DFU upload utility **dfu-util**

* Program **BigClown Firmware Tool**

At the end of the article, we'll show how to develop and compile firmware with popular editors like **Atom** or **Visual Studio Code**.

To install, go to one of the supported platforms:

* [**Setup on Windows**]({{< relref "#setup-on-windows" >}})

* [**Setup on macOS**]({{< relref "#setup-on-macos" >}})

* [**Setup on Ubuntu**]({{< relref "#setup-on-ubuntu" >}})

* [**Setup on Generic Linux**]({{< relref "#setup-on-generic-linux" >}})

To upgrade an existing installation, go to one of the supported platforms:

* [**Update on Windows**]({{< relref "#update-on-windows" >}})

* [**Update on macOS**]({{< relref "#update-on-macos" >}})

* [**Update on Ubuntu**]({{< relref "#update-on-ubuntu" >}})

* [**Update on Generic Linux**]({{< relref "#update-on-generic-linux" >}})

## Setup on Windows

{{% note "warning" %}}You will need administrator rights to install.{{% /note %}}

1. Download the current version of the **BigClown Toolchain** Windows installer:

    {{% download "Download from GitHub" "https://github.com/bigclownlabs/bch-windows-toolchain/releases" %}}

2. Launch the downloaded installer and choose the destination directory:

    {{% img src="windows-location.png" %}}

3. Now you can adjust the desired **Path** environment variable (we recommend to leave the default settings if in doubt) and proceed with the installation:

    {{% img src="windows-paths.png" %}}

4. The FTDI driver setup will launch automatically during the installation - install it:

    {{% img src="windows-ftdi.png" %}}

5. After finishing the installation, lauch the **BigClown Toolchain** using one these 3 ways:

    * From the **Desktop**

    * From the **Start** menu

    * From the **context menu** on the selected directory (using a right click)

        {{% note "info" %}}The advantage of the context menu is to open the **BigClown Toolchain** directly in the directory location you need to work with.{{% /note %}}

    {{% img src="windows-toolchain.png" %}}

6. Continue on the document [**Toolchain Guide**]({{< relref "doc/tutorials/toolchain-guide.md" >}}). You may also try:

    * [**Integration with Atom**]({{< relref "#integration-with-atom" >}}) or

    * [**Integration with Visual Studio Code**]({{< relref "#integration-with-visual-studio-code" >}})

## Update on Windows

1. Download and install the new version according to the chapter [**Setup on Windows**]({{< relref "#setup-on-windows" >}}).

## Uninstall on Windows

1. Uninstall **Apps & features**:

    {{% img src="windows-uninstall.png" %}}

## Setup on macOS

{{% note "warning" %}}The following procedure has been tested on **macOS 10.12**.{{% /note %}}

1. Open the **Terminal** application.

2. Install [**Homebrew**](https://brew.sh) (unless you already have it).

    {{% note "info" %}}Homebrew is the package management system and the ecosystem of packages for macOS.{{% /note %}}

3. Install **GCC ARM Embedded**:

        brew install caskroom/cask/gcc-arm-embedded

4. Install **Git**:

        brew install git

5. Install **dfu-util**:

        brew install dfu-util

6. Install **Python 3**:

        brew install python3

7. Update **pip** (Python Package Manager) to the latest version:

        sudo pip3 install --upgrade --no-cache-dir pip

8. Install **BigClown Firmware Tool**:

        sudo pip3 install --upgrade --no-cache-dir bcf

9. Continue on the document [**Toolchain Guide**]({{< relref "doc/tutorials/toolchain-guide.md" >}}). You may also try:

    * [**Integration with Atom**]({{< relref "#integration-with-atom" >}}) or

    * [**Integration with Visual Studio Code**]({{< relref "#integration-with-visual-studio-code" >}})

## Update on macOS

* Update of packages:

        brew update && brew upgrade

* BigClown Firmware tool update:

        sudo pip3 install --upgrade --no-cache-dir bcf

## Setup on Ubuntu

{{% note "warning" %}}The following procedure has been tested on **Ubuntu 16.04 LTS**.{{% /note %}}

1. Open the **Terminal** application.

2. Add the following PPA to the list of available repositories:

        sudo add-apt-repository ppa:team-gcc-arm-embedded/ppa

3. Update the index of the available packages:

        sudo apt update

4. Install **GCC ARM Embedded**:

        sudo apt install gcc-arm-embedded

5. Install **Git**:

        sudo apt install git

6. Install **dfu-util**:

        sudo apt install dfu-util

7. Install **Python 3** (required by the **BigClown Firmware Tool**):

        sudo apt install python3.5 python3-pip

8. Update **pip** (Python Package Manager) to the latest version:

        sudo pip3 install --upgrade --no-cache-dir pip

9. Install **BigClown Firmware Tool**:

        sudo pip3 install --upgrade --no-cache-dir bcf

10. Continue on the document [**Toolchain Guide**]({{< relref "doc/tutorials/toolchain-guide.md" >}}). You may also try:

    * [**Integration with Atom**]({{< relref "#integration-with-atom" >}}) or

    * [**Integration with Visual Studio Code**]({{< relref "#integration-with-visual-studio-code" >}})

## Update on Ubuntu

* Update of packages:

        sudo apt update && sudo apt upgrade

* BigClown Firmware tool update:

        sudo pip3 install --upgrade --no-cache-dir bcf

## Setup on Generic Linux

If you have other Linux distribution or unsupported Ubuntu version, we recommend to use official *GNU Embedded Toolchain for ARM* from [developer.arm.com](https://developer.arm.com) pages. This package is validated by ARM and tested by us.

1. Go to [https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads) and download **Linux 64-bit** package.

2. Extract package to filesystem, e.g. into `/opt` folder (*available for all users, you will need root privileges*) or into `~/.local/opt` folder (*available only for you*)

    1. **/opt version**

        ```shell
        cd <folder with package> # go to folder with downloaded file
        sudo cp gcc-arm-none-eabi-6-*-update-linux.tar.bz2 /opt  # copy to destination folder
        cd /opt  # go there
        sudo tar xjf gcc-arm-none-eabi-6-*-update-linux.tar.bz2  # unpack file
        ```

    2. **~/.local/opt version**

        ```shell
        mkdir -p ~/.local/opt  # create folder
        cd <folder with package> # go to folder with downloaded file
        cp gcc-arm-none-eabi-6-*-update-linux.tar.bz2 ~/.local/opt  # copy to destination folder
        cd ~/.local/opt  # go there
        tar xjf gcc-arm-none-eabi-6-*-update-linux.tar.bz2  # unpack file
        ```

3. Create a symbolic link `gcc-arm-none-eabi-6`

    ```shell
    sudo ln -s gcc-arm-none-eabi-6-<version>-update gcc-arm-none-eabi-6  # where <version> could be: 2017-q2
    ```

4. Update `PATH` variable so you can use arm-none-eabi-* binaries directly

    ```shell
    cd  # go to user home folder
    # use your favorite editor and edit ".profile" file
    # find line with PATH variable. e.g.:

        export PATH="$PATH:/…"
    ```

    {{% note "warning" %}}Please note that three dots (…) represents some text there.{{% /note %}}

    ```shell
    # and add to your path to the end (/opt version):

    export PATH="$PATH:/…:/opt/gcc-arm-none-eabi-6/bin"

    # or (~/.local/opt version)

    export PATH="$PATH:/…:~/.local/opt/gcc-arm-none-eabi-6/bin"

    # if there is no PATH line, add it

    export PATH="$PATH:/opt/gcc-arm-none-eabi-6/bin"

    # or

    export PATH="$PATH:~/.local/opt/gcc-arm-none-eabi-6/bin"
    ```

5. Use your distribution package manager and install

    * **Git**
    * **Python 3**
    * **dfu-util**

6. Install **BigClown Firmware Tool**:

        sudo pip3 install --upgrade --no-cache-dir bcf

7. Continue on the document [**Toolchain Guide**]({{< relref "doc/tutorials/toolchain-guide.md" >}}). You may also try:

    * [**Integration with Atom**]({{< relref "#integration-with-atom" >}}) or

    * [**Integration with Visual Studio Code**]({{< relref "#integration-with-visual-studio-code" >}})

    * [**Integration with KDevelop**]({{< relref "#integration-with-kdevelop" >}})

## Update on Generic Linux

* Update **Toolchain**
    * Download updated **Linux 64-bit** package from [https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)
    * Extract it into proper folder (`/opt`, `~/.local/opt` or other)
    * Update symbolic link

        ```shell
        sudo ln -sf gcc-arm-none-eabi-6-<version>-update gcc-arm-none-eabi-6  # where <version> could be: 2017-q2
        ```

        or

        ```shell
        ln -sf gcc-arm-none-eabi-6-<version>-update gcc-arm-none-eabi-6  # where <version> could be: 2017-q2
        ```

* Update packages
    * Use your distribution package manager

* BigClown Firmware tool update:

        sudo pip3 install --upgrade bcf


## Integration with Atom

**TODO**

## Integration with Visual Studio Code

Every BigClown project contains `.vscode` configuration folder so you just open the project folder in **Visual Studio Code** and you're ready to go.

In file `.vscode/tasks.json` there are some tasks which you can run by pressing `Ctrl+P` and typing `task`.

| Task  | Description |
| ----- |-------------|
| build | Build active project |
| clean | Clean active project |
| dfu   | Flash compiled firmware with dfu-util to the Core Module |
| ozone | Run Ozone debugger which can be used with J-Link debugger |
| update| Update SDK folder/submodule to the latest version |


{{< note "info" >}}
Project make file allows quicker parallel compilation. This can be set in `.vscode/tasks.json` where you set `"args": ["-j4"],` parameter, where the number 4 is the number of your CPU cores.
{{< /note >}}

## Integration with KDevelop

**TODO**

## Related Documents

* [**Toolchain Guide**]({{< relref "doc/tutorials/toolchain-guide.md" >}})
