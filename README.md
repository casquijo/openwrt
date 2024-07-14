# OpenWRT Disk Cloning Script

This script clones the OpenWRT disk to an external disk. Therefore, if the drive fails, you can simply point the boot to the other disk.

## Description

The script uses the `dd` command to clone the contents of an OpenWRT disk (e.g., an NVMe device) to an external USB disk. This provides a simple backup solution that allows you to recover quickly from a disk failure by booting from the cloned disk.

## Usage

1. **Edit the Script:**
   - Replace `/dev/sdX` with the correct NVMe device.
   - Replace `/dev/sdY` with the correct USB device.
   
2. **Run the Script:**
   - Make sure the script has executable permissions:
     ```sh
     chmod +x /path/to/your/script.sh
     ```
   - Execute the script manually:
     ```sh
     sudo /path/to/your/script.sh
     ```

## Optional: Set Up a Cron Job

You can set up a cron job to run this script automatically every day at 2:00 AM.

1. **Open the Crontab:**
   ```sh
   crontab -e
