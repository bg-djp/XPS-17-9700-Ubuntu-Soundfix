# XPS-17-9700-Ubuntu-Soundfix
A simple script to install the necessary firmware to fix sound output (dummy sound). This works on Ubuntu 20.04 and may or may not work on other versions.

## General info
All necessary files are included in this git repo. I've opted for this because some of the tutorials for this fix link to packages which 404 as they've been updated since.

You will also need a kernel that supports the new firmware. I opted for linux-oem-20.04 since that's a known one to include some Dell fixes. Currently 5.6.0-1056-oem is the one that works best, so I suggest you use that one.

## Tested Kernels
- 5.6.0-1056-oem No issues
- 5.10.0-1029-oem output/speaker sound works but [has microphone issues](https://github.com/stukev/XPS-17-9700-Ubuntu-Soundfix/issues/3)
- ??? Not tested, but supposedly should work according to upstream [stukev](https://github.com/stukev/XPS-17-9700-Ubuntu-Soundfix) 5.11.0-19 Should have no issues [according to Launchpad](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1912673/comments/24)

## Setup
1. Install Ubuntu 20.04.2
2. Install the necessary kernel with `sudo apt install linux-buildinfo-5.6.0-1056-oem linux-headers-5.6.0-1056-oem linux-image-5.6.0-1056-oem linux-modules-5.6.0-1056-oem linux-oem-5.6-headers-5.6.0-1056 linux-oem-5.6-tools-5.6.0-1056 linux-oem-5.6-tools-host linux-tools-5.6.0-1056-oem`
3. Clone the repo `git clone https://github.com/bg-djp/XPS-17-9700-Ubuntu-Soundfix.git`
4. Run the fix `sudo sh XPS-17-9700-Ubuntu-Soundfix/sound_fix.sh`
5. You may wish to comment out `#GRUB_TIMEOUT_STYLE=hidden` and set `GRUB_TIMEOUT=20` in `/etc/default/grub` and then run `sudo update-grub`
6. Reboot and **select the 5.6.0-1056-oem kernel in GRUB** under 'Advanced options'.
7. If you still have no sound, check whether you booted the correct kernel with `uname -a`. If you did, try running `alsamixer`, TABbing over to "ALL" and checking for muting of the `rt715 ADC 07` channel (it will look like dashes in that column; press SPACE to toggle mute/unmute. You may also want to increase the volume of that channel to a medium level with the up arrow.)

Future updates from Ubuntu may break this fix. Consider using `apt-mark hold` on the kernel to prevent it from being upgraded or removed.
