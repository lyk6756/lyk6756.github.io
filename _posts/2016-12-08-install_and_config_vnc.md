---
layout: post
title: "Install and Configure TigerVNC on CentOS 7"
---

# What is VNC

VNC(Virtual Network Computing) is a *graphical* desktop sharing system that uses the Remote Frame Buffer protocol (RFB) to remotely control another computer. It transmits the keyboard and mouse events from one computer to another, relaying the graphical screen updates back in the other direction, over a network.

Among numerous VNC client/server application, [TigerVNC](http://tigervnc.org/) is a high-performance, platform-neutral implementation provided with many distributions. TigerVNC is an opensource software following GPL license. You can easily get TigerVNC repository on GitHub.

Created by Red Hat, Cendio AB, The VirtualGL Project, it became the default VNC implementation in Fedora shortly after its creation.

# Goal

Our goal is to install and configure TigerVNC on a Linux server, which is running a CentOS 7 distribution with GNOME desktop.

After that, a series of remote desktop connections will be demonstrated on clients with different platforms.

As a tutorial, all the installations and configurations are operated under administrator `root`.

# Install TigerVNC Server

To check whether if our server already has installed TigerVNC, run the command

```
# rpm -q tigervnc tigervnc-server
```

If there is no installation found, the system will tell

```
package tigervnc is not installed
package tigervnc-server is not installed
```

You can install the Tiger VNC server using `yum`

```
# yum install -y tigervnc tigervnc-server
```

# Check status of VNC service

To check the status of VNC service, run the following command:

```
# systemctl status vncserver@:.service
```

where `vncserver@:.service` is the config file of VNC server, which is our goal in this step.

You can also check if the service is enabled using

```
# systemctl is-enabled vncserver@.service
```

which should return `disabled` by now.

# Configure VNC server for root user

In VNC service, each user will start a separate instance of the VNC service daemon. In other words, VNC doesn't run as one single process that serves every user request. Each user connecting via VNC will have to start a new instance of the daemon.

In CentOS 7, you can find a sample config file `vncserver@.service` under directory `/lib/systemd/system`. Open the file, a Quick HowTo in comment tells us what we should do.

```
# The vncserver service unit file
#
# Quick HowTo:
# 1. Copy this file to /etc/systemd/system/vncserver@:<display>.service
# 2. Edit <USER> and vncserver parameters appropriately
#   ("runuser -l <USER> -c /usr/bin/vncserver %i -arg1 -arg2")
# 3. Run `systemctl daemon-reload`
# 4. Run `systemctl enable vncserver@:<display>.service`
```

Now we need to great our instance of VNC server for administrator `root` under directory `/etc/systemd/system`

```
# cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service
```

**Note** that the file might be read only. Write permission is needed to configure our instance.

Here, we change `<display>` in the name `vncserver@:<display>.service` into a number `:1`. This stands for the port of our service. VNC by itself runs on port `5900`. Since each user will run their own VNC server, each user will have to connect via a separate port. The addition of a number in the file name tells VNC to run that service as a sub-port of 5900. So in our case, administrator's VNC service will run on port `5901` (5900 + 1).

Then, edit the `[Service]` section in file `vncserver@:1.service`: replacing `<USER>` with `root`, and adding command `-geometry 1920x1080` at the end of the `ExecStart` parameter. After editing, the `[Service]` section should be like this:

```
[Service]
Type=forking
# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/sbin/runuser -l root -c "/usr/bin/vncserver %i -geometry 1920x1080"
PIDFile=/home/root/.vnc/%H%i.pid
ExecStop=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
```

# Configure firewall

My CentOS 7 uses Dynamic Firewall through the `firewalld` daemon, which should start automatically at system boot time. To check the status, run command

```
# firewall-cmd --status
```

If the state is `not running`, execute the following command to make sure it's running:

```
# systemctl start firewalld
```

We should either add `port 5901` or `vnc-server` to the firewall to protect our service from blocking. So the following two snippet are doing the same thing

```
# firewall-cmd --permanent --zone=public --add-service vnc-server
```

```
# firewall-cmd --permanent --zone=public --add-port=5901/tcp
```
Then, reload the firewall to adopt the new rule:

```
# firewall-cmd --reload
```

# Set VNC password

**Note** that a VNC password is **not** the user' Linux password, but the passwords to log in to the VNC sessions.

Under the user `root`, execute the following command:

```
# vncserver
```

For the first time to run this command, the system will ask to set up the password. **Note** that it should be at least 6 characters.

A new directory `.vnc` will be created automatically under your home directory, which contain the default startup script `xstartup`, log file and your password file `passwd`.

To change your VNC password, using

```
# vncpasswd
```

# Start VNC service

Next, run the following commands to reload the systemd daemon and start 

```
# systemctl daemon-reload
# systemctl start vncserver@:1.service
```

Also make sure VNC starts up for users at boot time

```
# systemctl enable vncserver@:1.service
```

Now our server are set to be login remotely.

## Troubleshooting: Exit code 98

If you failed to start your VNC service with the return

```
Job for vncserver@:1.service failed. See ‘systemctl status vncserver@:1.service’ and ‘journalctl -xn’ for details.
```

By running `systemctl status vncserver@:1.service`, if you can find `(code=exited, status=98)` in the status report, we can solve the problem by changing `Type=forking` into `Type=simple` in the `[Service]` section of config file `vncserver@:1.service`.

# Connecting with Vinagre on a client running Linux

[Vinagre](https://wiki.gnome.org/Apps/Vinagre) is a VNC, SSH, RDP and SPICE client for the GNOME desktop environment.

Just add the IP address of your CentOS 7 server and specify the port number `5901` or `1` after the server's IP by a colon (:). Here is an example

```
VNC Server: 192.168.1.148:1
```

Type in the password when asking. 

Enjoy Now!

# Connecting with VNCViewer on a client running Windows

TigerVNC provides Windows VNC client software installers for 64-bit and 32-bit on [bintray](https://bintray.com/tigervnc/stable/tigervnc).

Another client widely used is [VNC Viewer](https://www.realvnc.com/download/viewer/), which is developed by [RealVNC](https://www.realvnc.com/). **Note** that although the server app (called VNC Connect) may has limits for personal use, VNC Viewer is always **free** to use.

With your any VNC client started, just add the IP address of your CentOS 7 server and specify the port number `5901` or `1` after the server's IP by a colon (:). Here is an example

```
VNC Server: 192.168.1.148:1
```

Type in the password when asking.

Enjoy Now!

You can secure VNC sessions through SSH tunneling if necessary.

# Further reading

* Wikipedia: [Virtual Network Computing](https://en.wikipedia.org/wiki/Virtual_Network_Computing) / [TigerVNC](https://en.wikipedia.org/wiki/TigerVNC) / [Comparison of remote desktop software](https://en.wikipedia.org/wiki/Comparison_of_remote_desktop_software)
* [How To Install and Configure VNC Remote Access for the GNOME Desktop on CentOS 7 - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-remote-access-for-the-gnome-desktop-on-centos-7)