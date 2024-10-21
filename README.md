## Turn your linux desktop rice into installable live iso!

Yeah as the title says, if your are a linux desktop ricer, why not make it an installable iso so you can share it to anyone who wanna test it or install it on their machines. With this scripts, make a custom iso with your own customization and linux distro of your choice is just easy. So far this script is tested myself with some distros like Archlinux, Void Linux, CRUX and Venom Linux.

## How to do it?
If you are on aarch64 host running Arch Linux ARM skip to step 4.
If you are on amd64 host here are steps:
1. Add those mirrors to your `/etc/pacman.d/mirrorlist`:
   `
Server = http://mirror.archlinuxarm.org/$arch/$repo
Server = http://dk.mirror.archlinuxarm.org/$arch/$repo
Server = http://de3.mirror.archlinuxarm.org/$arch/$repo
Server = http://de.mirror.archlinuxarm.org/$arch/$repo
Server = http://de4.mirror.archlinuxarm.org/$arch/$repo
Server = http://eu.mirror.archlinuxarm.org/$arch/$repo
Server = http://de5.mirror.archlinuxarm.org/$arch/$repo
Server = http://gr.mirror.archlinuxarm.org/$arch/$repo
Server = http://hu.mirror.archlinuxarm.org/$arch/$repo
Server = http://jp.mirror.archlinuxarm.org/$arch/$repo
Server = http://sg.mirror.archlinuxarm.org/$arch/$repo
Server = http://tw2.mirror.archlinuxarm.org/$arch/$repo
Server = http://tw.mirror.archlinuxarm.org/$arch/$repo
Server = http://uk.mirror.archlinuxarm.org/$arch/$repo
Server = http://ca.us.mirror.archlinuxarm.org/$arch/$repo
Server = http://fl.us.mirror.archlinuxarm.org/$arch/$repo
Server = http://nj.us.mirror.archlinuxarm.org/$arch/$repo
   `
2. Download and install keyring of Arch Linux ARM:
`
wget http://mirror.archlinuxarm.org/aarch64/core/archlinuxarm-keyring-20240419-1-any.pkg.tar.xz && sudo pacman -U archlinuxarm-keyring* && rm archlinuxarm-keyring*
`
3. Update your repos:
`
sudo pacman -Sy
`
4. Run the `mkrootfs-archlinux.sh` script from root directory using bash:
`
bash mkrootfs-archlinux.sh
`

## Requirements

### for host
- xorriso - to create iso
- squashfs-tools - to compress rootfs
- curl - to fetch necessary files
- gimp - to create custom grub/syslinux splash (optional)
