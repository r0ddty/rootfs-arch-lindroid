## Arch Linux rootfs builder adapted for aarch64 Lindroid devices

## How to use it?
If you are on aarch64 host running Arch Linux ARM skip to step 4.
If you are on amd64 host here are steps:
### 1. Add those mirrors to your `/etc/pacman.d/mirrorlist`:
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

### 2. Download and install keyring of Arch Linux ARM:
`
wget http://mirror.archlinuxarm.org/aarch64/core/archlinuxarm-keyring-20240419-1-any.pkg.tar.xz && sudo pacman -U archlinuxarm-keyring* && rm archlinuxarm-keyring*
`

### 3. Update your repos:
`
sudo pacman -Sy
`

### 4. Run the `mkrootfs-archlinux.sh` script from root directory using bash:
`
bash mkrootfs-archlinux.sh
`
And now you have your rootfs in ./rootfs-archlinux directory!

### 5. Compress the rootfs using tar/bsdtar(you'll figure that out i've no clue how to)

### 6. Push the rootfs to your device internal storage using adb:
`
adb push rootfs.tar.gz /sdcard
`

### 7. Install it via adb using lxc provided by Lindroid:
hint: you can change name of container by replacing "default" with any name you want
`
adb shell -t lxc_create default -t lindroid -- -f /dev/fd/4 "4</sdcard/rootfs.tar.gz"
`
### 8. Now you can open "Lindroid" app on your device and run the container!

### Bonus: SSHing to the container directly using adb:
`
adb shell -t lxc_attach default -- "/bin/bash -c \"source /etc/profile && exec su - root\""
`
where "default" is the name of your container.
