# Use Systemctl to manage systemd service and units

<!--toc:start-->
- [Use Systemctl to manage systemd service and units](#use-systemctl-to-manage-systemd-service-and-units)
  - [what is systemd](#what-is-systemd)
  - [Service Management](#service-management)
    - [start and stop services](#start-and-stop-services)
    - [restart and reload](#restart-and-reload)
    - [enable and disable service](#enable-and-disable-service)
    - [check status of service](#check-status-of-service)
    - [System State Overview](#system-state-overview)
    - [List Current Units](#list-current-units)
    - [List All Unit Files](#list-all-unit-files)
  - [Unit Management](#unit-management)
    - [Display a Unit File](#display-a-unit-file)
<!--toc:end-->

[web](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

## what is systemd

systemd is an init system and system manager which is widely used.we will discuss the `systemctl` command which is used to mamnage teh init system.

## Service Management

fundamental purpose of an init system is to initalize the components that must start after linux kernal.

target of actions are "Units". For service management tasks, the target unit will be service units, which have unit files with a suffix of .service.

### start and stop services

```shell
sudo systemctl start {application}[.service]
sudo systemctl stop {application}[.service]
```

### restart and reload

```shell
sudo systemctl restart {application}[.service]
sudo systemctl reload {application}[.service]
```

If you are unsure whether the service has the functionality to reload its configuration, you can issue the reload-or-restart command. This will reload the configuration in-place if available. Otherwise, it will restart the service so the new configuration is picked up:

```shell
sudo systemctl reload-or-restart application.service
```

### enable and disable service

start service at boot :

```shell
sudo systemctl enable application.service
```

This will create a symbolic link from the system’s copy of the service file (usually in /lib/systemd/system or /etc/systemd/system) into the location on disk where systemd looks for autostart files (usually /etc/systemd/system/some_target.target.wants. We will go over what a target is later in this guide).

To disable the service from starting automatically, you can type:

```shell
sudo systemctl disable application.service
```

### check status of service

```shell
systemctl status application.service
```

check is-xxx like activate, enabled, failed

```shell
systemctl is-xxx application.service
```

### System State Overview

explore the current state of system

### List Current Units

```shell
systemctl list-units
systemctl #do the same thing
```

This will show you a list of all of the units that systemd currently has active on the system. The output will look something like this:

```shell
Output
UNIT                                      LOAD   ACTIVE SUB     DESCRIPTION
atd.service                               loaded active running ATD daemon
avahi-daemon.service                      loaded active running Avahi mDNS/DNS-SD Stack
dbus.service                              loaded active running D-Bus System Message Bus
dcron.service                             loaded active running Periodic Command Scheduler
dkms.service                              loaded active exited  Dynamic Kernel Modules System
getty@tty1.service                        loaded active running Getty on tty1
. . .
```

### List All Unit Files

`list-units` command display units that `systemd` has attemped to parse and loaded into memory. the following will display that not attempt to load.

 ```shell
systemctl list-unit-files
```

## Unit Management

more command about units

### Display a Unit File

we can use cat command to display.

```shell
systemctl cat atd.service

Output
[Unit]
Description=ATD daemon
[Service]
Type=forking
ExecStart=/usr/bin/atd
[Install]
WantedBy=multi-user.target
```

### Display dependencies

To see a unit’s dependency tree, you can use the `list-dependencies`

```shell
systemctl list-dependencies sshd.service
```

### Editing Unit file

```shell
sudo systemctl edit nginx.service
```

This will be a blank file that can be used to override or add directives to the unit definition.A directory will be created within the /etc/systemd/system directory which contains the name of the unit with `.d` appended. For instance, for the `nginx.service`, a directory called `nginx.service.d` will be created.

Within this directory, a snippet will be created called override.conf. When the unit is loaded, systemd will, in memory, merge the override snippet with the full unit file. The snippet’s directives will take precedence over those found in the original unit file.

If you wish to edit the full unit file instead of creating a snippet, you can pass the `--full` flag:

```shell
sudo systemctl edit --full nginx.service
```

if remove addtionas you made 

```shell
sudo rm -r /etc/systemd/system/nginx.service.d
```

remove the full unit file

```shell
sudo rm /etc/systemd/system/nginx.service
```

