# CPU Governor Selection Script

This script allows you to set the CPU governor mode for all CPUs on your system. The available governor modes are `performance` and `powersave`.

## Description

The script lists available CPU governor modes and prompts the user to select one. It then applies the selected governor mode to all CPUs where applicable. The script ensures that the change is applied and confirms the current governor settings for all CPUs.

## Usage

1. **Make the Script Executable:**
   - Before running the script, you need to give it executable permissions:
     ```sh
     chmod +x /path/to/your/script.sh
     ```

2. **Run the Script:**
   - Execute the script:
     ```sh
     sudo /path/to/your/script.sh
     ```

3. **Follow the Prompts:**
   - The script will display a list of available governor modes. Enter the corresponding number to select the desired mode.

## Script Details

```sh
#!/bin/sh

# use chmod +x and ./ to execute

# List of available governor modes
governors="performance powersave "

# Display the governor options
echo "Please choose the desired governor mode by entering the corresponding number:"
index=0
for governor in $governors; do
  echo "$index) $governor"
  index​⬤


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
