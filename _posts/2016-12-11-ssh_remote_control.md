---
layout: post
title: "SSH Remote Control to a Linux Server"
---

# What is SSH

Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network. The best known example application is for remote login to computer systems by users. SSH provides a secure channel over an unsecured network in a client-server architecture, connecting an SSH client application with an SSH server.


# Install and config OpenSSH on a CentOS server

[OpenSSH](https://www.openssh.com/) is a suite of opensource programs for remote login based on SSH protocol, developed by the [OpenBSD Project](https://www.openbsd.org/). Since it is free for all users, Most Linux distribution has openssh installed initially.

CentOS 7 provides `openssh`, `openssh-server` and `openssh-clients` packages. The `openssh` package should be initially installed. Note that `openssh` package requires `openssl-libs` to be installed on the system since it provides some very important cryptographic libraries.

To install the server and client package,

```shell
$ sudo yum -y install openssh-server
$ sudo yum -y install openssh-clients
```

To start the SSH service in CentOS,

```shell
$ sudo systemctl start sshd.service
```

This will creat the OpenSSH daemon `sshd` that listens for connections from clients via port 22. It forks a new daemon for each incoming connection. The forked daemons handle key exchange, encryption, authentication, command execution, and data exchange.

To turn off this service,

```shell
$ sudo systemctl stop sshd.service
```

If you wish to have the SSH daemon run automatically as the computer boots up, issue the command,

```shell
$ sudo systemctl enable sshd.service
```

This will allow the SSH service to run every time you start up your computer, which is normally started at boot from `/etc/rc`.

The default configuration file for the `sshd` daemon is `sshd_config` under the directory `/etc/ssh/`. We can uncomment the default settings and change what we want

```shell
Port 1234 # change port from 22(default) to 1234

PermitRootLogin no # disable root logins

AllowUsers john jane # restrict login to user john and jane only over ssh

DenyUsers smith # refuse login to user smith

ListenAddress 192.168.1.150  # set the address that sshd listen to

PermitEmptyPasswords no  # reject logins with no passwords
```

Read [OpenSSH Manual Pages](http://www.openssh.com/manual.html) to learn more.

# Connecting on a Linux client using ssh command

To connect to our server, running the basic ssh command:

```shell
$ ssh <username>@<hostname or IP address>
```

`<username>` is the hostname of the server that you want to connect to. By default ssh will use the same username as on your client if you live `user` as blanked. Such as

```shell
$ ssh <hostname or IP address>
```

`<hostname or IP address>` is the IP adress or the name of your server if your network have DNS service.

Since SSH use *port 22* as default port, if you want to connect via other port, using

```shell
$ ssh user@host -p 1234
```

This will change port from 22(default) to 1234.

For the first login, it will ask you if you wish to add the remote host to a list of known hosts. Don't worry, go ahead and say yes.

To end your SSH session, typing `exit` command or `logout` command. This will kill all the process and end SSH connection.

Read [ssh Command - OpenSSH General Commands Manual](http://man.openbsd.org/ssh) to learn more.

# Connecting on a client running Windows

SSH sees some limited use on Windows. In 2015, Microsoft announced that they would include native support for SSH in a future release.

To use ssh, you need either a ssh client program or a Linux-like shell environment. Here I recommend two softwares: PuTTY and Cygwin.

* [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) is a free, opensource implementation of SSH and Telnet for Windows and Unix platforms, along with an xterm terminal emulator. Prortable exe programs are provided on [PuTTY Download Page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Using PuTTY, you need to type in the necessary info like server adress, user name and port number.

* [Cygwin](https://cygwin.com/) is a Unix-like environment and command-line interface for Microsoft Windows. Cygwin provides native integration of Windows-based applications, data, and other system resources with applications, software tools, and data of the Unix-like environment.

Maybe it will take a little time to setup Cygwin environment after installation. By Cygwin, you can use `ssh` command just as mentioned last section.

Refer to [Cygwin User's Guide](http://www.cygwin.com/cygwin-ug-net/cygwin-ug-net.html) and [Cygwin FAQ](https://cygwin.com/faq.html) to learn more.

# File transfers using scp command

SSH can not only login to remote hosts, but also provides file transfers between clients and servers.

SSH uses `scp` command for secure copy (remote file copy program) between hosts over an encrypted connection based on SSH protocol. You can transfer files from your local client to a remote host or vice versa or even from a remote host to another remote host. 

To copy a file from your computer to another computer(upload), type:

```shell
$ scp <file> <username>@<IP address or hostname>:<Destination>
```

For example, my server's IP is 192.168.1.150. I run the following command on my client to copy a file called `test.txt` from the local computer to a file by the same name on the server under directory `~/`(i.e. `/home/username/`).

```shell
$ scp test.txt username@192.168.1.150:
```

Then I make another copy of `test.txt` while changing the name to `readme.txt` and specifying directory `/home/program/`

```shell
$ scp test.txt username@192.168.1.150:/home/program/readme.txt
```

To copy the file back from the server(download), just reverse the from and to.

```shell
$ scp username@192.168.1.150:/home/program/readme.txt readme.txt
```

Adding `-r`(recursive) option, SSH copy a whole directory recursively to a remote location. The following command copies a directory named `testprogram` to the home directory of the user on the server.

```shell
$ scp -r testprogram username@192.168.1.150:
```

Read [scp Command - OpenSSH General Commands Manual](http://man.openbsd.org/scp) to learn more.

# Keep your process alive

Normally linux will forcibly kill all process and jobs created by remote users once he logs out of the session or the session times out after being idle for quite some time.

We can use `nohup` command to send our long running command to background so that we can continue while the command will keep on executing in background. After that we can safely log out.

A basic `nohup` usage is

```shell
$ nohup [command] &
```

This will send the task to background with prompt returning immediately giving *PID* and job *I*D* of the process. i.e. `[JOBID] PID`

To check the status of command and bring it back to foreground once you resuming your SSH session, using

```shell
$ fg %JOBID
```

## Troubleshooting

Sometimes you may have trouble keeping your SSH session up and idle. For whatever reason, the connection just dies after X minutes of inactivity. Usually this happens because there is a firewall between you and the internet that is configured to only keep stateful connections in its memory for 15 or so minutes.

Fortunately, in recent versions of OpenSSH, there is a fix for this problem. Simply put the following:

```
Host *
Protocol 2
TCPKeepAlive yes
ServerAliveInterval 60
```

in the file `~/.ssh/config`.

The file above can be used for any client side SSH configuration. See the ssh_config man page for more details. The 'TCPKeepAlive yes' directive tells the ssh client that it should send a little bit of data over the connection periodically to let the server know that it is still there. 'ServerAliveInterval 60 sets this time period for these messages to 60 seconds. This tricks many firewalls that would otherwise drop the connection, to keep your connection going.

# Further reading

* Wikipedia: [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) / [Comparison of SSH clients](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients)
* [SSH Tutorial - SiteGround](https://www.siteground.com/tutorials/ssh/)
* [5 Ways to Keep Remote SSH Sessions and Processes Running After Disconnection - Tecmint](http://www.tecmint.com/keep-remote-ssh-sessions-running-after-disconnection/)