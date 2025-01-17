# CPU Governor Selection Script

This script allows you to set the CPU governor mode for all CPUs on your system. The available governor modes are `performance` and `powersave`.

## Description

The script lists available CPU governor modes and prompts the user to select one. It then applies the selected governor mode to all CPUs where applicable. The script ensures that the change is applied and confirms the current governor settings for all CPUs.

# Automatic Backup Service Script for OpenWrt

## Overview

This script provides an automatic backup service for OpenWrt. It continuously monitors specific system directories for any changes and creates backups whenever modifications are detected. The service is designed to start with the system and run in the background, ensuring that your configurations are always backed up.

## How It Works

- **Monitored Directories**: The script watches the `/etc/config`, `/etc/init.d`, and `/etc/rc.d` directories for any changes.
- **Reference File**: A reference file (`.last_backup`) is used to keep track of the last backup time.
- **Change Detection**: The script uses the `find` command to check if any files in the monitored directories have been modified since the last backup.
- **Backup Creation**: If changes are detected, a backup is created using the `sysupgrade` command, and the reference file is updated to the current time.
- **Service Integration**: The script is integrated into OpenWrt's init system, ensuring it starts automatically on boot and runs continuously.

## Make the Script Executable
```
chmod +x /root/scripts/backup_on_change.sh
```
## Create the Service Script
```
#!/bin/sh /etc/rc.common

START=99
STOP=1

start() {
    echo "Starting backup on change service"
    /root/scripts/backup_on_change.sh &
}

stop() {
    echo "Stopping backup on change service"
    killall backup_on_change.sh
}
```
## Make the Service Script Executable
```
chmod +x /etc/init.d/backup_on_change
```
## Enable and Start the Service
```
/etc/init.d/backup_on_change enable
/etc/init.d/backup_on_change start
```
## Configuration
In the backup script, change the line mkdir -p /mnt/externaldisk/bkps/ to your desired backup path:
```
# Change here to your backup path
mkdir -p /mnt/externaldisk/bkps/
```
## Conclusion

This setup ensures that your OpenWrt configurations are backed up automatically whenever changes are detected, providing an additional layer of security and convenience.

## Schedule tasks or CRON

You can use the backup command directly in the cron or scheduled tasks of the LUCI graphical interface, as in the example below

```
# /mnt/externaldisk/bkps/ == $path
00 10 * * * mkdir -p /mnt/externaldisk/bkps/ && sysupgrade -b /mnt/externaldisk/bkps/backup-${HOSTNAME}-$(date +\%F-\%H\%M\%S)-$(date +\%N).tar.gz

```






