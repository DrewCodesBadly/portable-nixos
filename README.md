# portable-nixos
horrifying contraption I carry on a usb drive to scare people

# Setting up a new usb
1. Download the NixOS graphical installer [here](https://nixos.org/download/)
2. Write it to another USB, preferably (you could probably use the same one and install to another partition, it's just annoying)
- On linux, run `fdisk -l` to find the drive then ensure unmounted (`sudo umount /dev/[DRIVE]*`)
- then run `sudo dd bs=4M conv=fsync oflag=direct status=progress if=[ISO PATH] of=/dev/[DRIVE]`
- you could also use tools like rufus
3. If you want Windows/probably macos to still recognize the drive, make an exFAT partition as the FIRST partition on the drive and install to the rest of the disk.
4. Boot into the installer, connect to the internet and start the installation process
- Disable the secure password requirement and create a user named "user" with no password
- Set the root password to be something
- Install with no desktop environment
- Enable unfree software
- Create partitions manually; you should make a fat32 boot, ext4 filesystem, and swap
- Click through to confirm and start the installation
5. Once complete, boot into the new usb drive and login as root
6. Connect to the internet if needed
7. Start a nix shell with git - `nix-shell -p git`
8. Clone this repository into the root of the filesystem
- `cd /`
- `git clone [URL]`
- `cp -r -a portable-nixos/* /`
- `rm -rf portable-nixos`
9. `nixos-rebuild switch`

You may need to re-run `nixos-generate-config` to regenerate the hardware configuration for different devices.
