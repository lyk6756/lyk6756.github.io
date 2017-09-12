---
layout: post
title:  "Install Abaqus2016 on Linux (Ubuntu 16.04 64bit)"
baseurl: "/Abaqus/"
---

# Preparative: Install necessary packages

## Install shell interpreter(CSH & KSH) and lsb-release

```shell
$ sudo apt-get update
$ sudo apt-get csh ksh
$ sudo apt-get lsb-release
```

## Install 32-bit system termcap library

```shell
$ sudo updatedb
$ locate libncurses
```

you will see a set of `libncurse.so.X` files. For example:

```shell
/lib/libncurses.so.5
/lib/i386-linux-gnu/libncurses.so.5.9
...
```

If you do not see such files then you will have to install libncurses:

```shell
$ sudo apt-get install libncurses5:i386 # 32-bit version
```

Once you find the libnucrses.so.5.X file, run the following command:

```shell
$ sudo ln -s /lib/i386-linux-gnu/libncurses.so.5.9 /lib/libtermcap.so.2
```

## Install Gnome GUI

You would need to switch to Gnome classic no effects to avoid the translucent windows while setup.

```shell
$ sudo apt-get install gnome-session-flashback
```

## Install `libjpeg62` & `libstdc++5`

When launching abaqus cae, if an error occurs:
>error while loading shared libraries: libjpeg.so.62: cannot open shared object file: No such file or directory

Install `libjpeg62`:

```shell
$ sudo apt-get install libjpeg62
```

When launching abaqus cae, if an error occurs:
>error while loading shared libraries: libstdc++.so.5: cannot open shared object file: No such file or directory

Install `libstdc++5`:

```shell
$ sudo apt-get install libstdc++5
```

# Launch Abaqus License Server:

1. Login root

2. Unpack `simulia.tar.gz` to the directory:`/usr/DassaultSystemes/SIMULIA/License/``

3. Edit the `ABAQUS.lic` file:

```shell
$ sudo gedit ~/abaqus/License/ABAQUS.lic
```

In the text editor that will be opened, edit the HOST_NAME in fist row of the file.

4. Edit the `.bashrc` file:

```shell
$ sudo gedit ~/.bashrc
```

or

```shell
$ sudo gedit root/.bashrc
```

In the text editor that will be opened, add the following rows at the top:

```shell
#abaqus
export LM_LICENSE_FILE=27011@PCNAME
alias abalic='sudo /usr/DassaultSystemes/SIMULIA/License/lmgrd -c /usr/DassaultSystemes/SIMULIA/License/ABAQUS.lic -l /usr/DassaultSystemes/SIMULIA/License/ABAQUS.log'
alias abaqus='sudo /var/DassaultSystemes/SIMULIA/Commands/abaqus'
alias cae='XLIB_SKIP_ARGB_VISUALS=1 abaqus cae'
```

Where PCNAME is the name of your PC.

Note that export the following environment variable, this is an issue on some ubunutu machines which causes the abaqus gui to become transparent.

```shell
XLIB_SKIP_ARGB_VISUALS=1
export XLIB_SKIP_ARGB_VISUALS
```

5. Reboot the Computer

# (OPTIONAL) Install DS SIMULIA ABAQUS2016 Documentation:

1. Login root

2. Mount ABAQUS 2016 Documentation ISO

3. Start installation process for ABAQUS Documentation:


```shell
$ ./setup
```

Installation Directory: `/usr/DassaultSystemes/SIMULIA/Documentation/`

# Install DS SIMULIA ABAQUS 2016

1. Login root
2. Mount the ISO image

Then Start installation process sequentially (one after one completes)

3. Install 3DEXPERIENCE_AbaqusSolver

Using command-line:

```shell
$ cd <mounted CD folder>
$ export DSYAuthOS_`lsb_release -si`=1 && export DSY_Force_OS=linux_a64 && ksh ./StartGUI.sh
```

Default Installation Directory: `/usr/DassaultSystemes/SimulationServices/V6R2016X`
Components: Select All by default

4. Install CAA_3DEXPERIENCE_AbaqusSolver

Using command-line:

```shell
$ cd <mounted CD folder>
$ export DSYAuthOS_`lsb_release -si`=1 && export DSY_Force_OS=linux_a64 && ksh ./StartGUI.sh
```

Default Installation Directory: `/usr/DassaultSystemes/SimulationServices/V6R2016X`

5. Install SIMULIA_Abaqus_CAE

Using command-line:

```shell
$ cd <mounted CD folder>
$ export DSYAuthOS_`lsb_release -si`=1 && export DSY_Force_OS=linux_a64 && ksh ./StartGUI.sh
```

Installation Directory: `/usr/DassaultSystemes/SIMULIA/CAE/2016/`

Path To ABAQUS Solvers: `/usr/DassaultSystemes/SimulationServices/V6R2016X`

Path to Documentation: `/usr/DassaultSystemes/SIMULIA/Documentation/<path to xml>`

Path to ABAQUS Commands: `/var/DassaultSystemes/SIMULIA/` (by default)

Licensing: SIMULIA FlexNet with `27011@localhost` as License Server 1

Working Directory: `/var/tmp` (by default)

# Run

To run, use the following commands:
```shell
$ abalic
$ abaqus
$ cae
```
Enjoy!

# Notice
Abaqus 2016 adopted a new installation method and refuses to install on Ubuntu system with the following error message:

```shell
~/Downloads/AM_SIM_Abaqus.AllOS/1/SIMULIA_Abaqus_CAE/Linux64/1/StartGUI.sh
CurrentMediaDir initial="/home/saiwal/Downloads/AM_SIM_Abaqus.AllOS/1/SIMULIA_Abaqus_CAE/Linux64/1"
CurrentMediaDir="/home/saiwal/Downloads/AM_SIM_Abaqus.AllOS/1/SIMULIA_Abaqus_CAE/Linux64/1"
Current operating system: "Linux"
DSY_OS_Release="Ubuntu"
Unknown linux release "Ubuntu"
exit 8
```

To force an installation I found a way to disguise system operating system name to CentOS to proceed with the installation. The process is as follows:

After extracting the installation files, open the following file in a text editor:

    AM_SIM_Abaqus.AllOS/1/SIMULIA_Abaqus_CAE/Linux64/1/inst/common/init/Linux.sh

edit line 4 from

    DSY_OS_Release=`lsb_release --short --id |sed 's/ //g'`

to

    DSY_OS_Release="CentOS"
