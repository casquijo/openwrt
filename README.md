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

## Setup Instructions

### 1. Create the Backup Script

Save the following script as `backup_on_change.sh` in the `/root/scripts/` directory:

```sh
#!/bin/sh

WATCHED_DIRS="/etc/config /etc/init.d /etc/rc.d"
REF_FILE="/root/scripts/.last_backup"

# Create reference file if it does not exist
if [ ! -f $REF_FILE ]; then
    touch $REF_FILE
fi

while true; do
    echo "Checking for changes in watched directories..."  # Debug message

    # Check if there are any files modified since the last backup
    CHANGED_FILES=$(find $WATCHED_DIRS -type f -newer $REF_FILE 2>/dev/null)

    if [ -z "$CHANGED_FILES" ]; then
        echo "No changes detected, no backup created"  # Debug message
        sleep 60
        continue
    fi

    echo "Changes detected, creating backup..."  # Debug message
    TIMESTAMP=$(date +'%F-%H%M%S-%N')
    mkdir -p /mnt/externaldisk/bkps/
    sysupgrade -b /mnt/externaldisk/bkps/backup-${HOSTNAME}-${TIMESTAMP}.tar.gz

    # Update the reference file to the current time
    touch $REF_FILE
    echo "Backup created at /mnt/externaldisk/bkps/backup-${HOSTNAME}-${TIMESTAMP}.tar.gz"  # Debug message

    sleep 60
done
