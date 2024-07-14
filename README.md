# CPU Governor Selection Script

This script allows you to set the CPU governor mode for all CPUs on your system. The available governor modes are `performance` and `powersave`.

## Description

The script lists available CPU governor modes and prompts the user to select one. It then applies the selected governor mode to all CPUs where applicable. The script ensures that the change is applied and confirms the current governor settings for all CPUs.

# OpenWRT Disk Cloning Script

This script clones the OpenWRT disk to an external disk. Therefore, if the drive fails, you can simply point the boot to the other disk.

## Description

The script uses the `dd` command to clone the contents of an OpenWRT disk (e.g., an NVMe device) to an external USB disk. This provides a simple backup solution that allows you to recover quickly from a disk failure by booting from the cloned disk.
