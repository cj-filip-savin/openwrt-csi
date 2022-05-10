Install OpenWRT build prerequisites. Then clone CSI-patched OpenWRT:
```
git clone https://github.com/cujof/openwrt-csi && cd openwrt-csi
```
If you have gcc newer than 10 then install gcc-10 and set environment variables to use it:
```
export CC=gcc-10
export CXX=g++-10
```
Update and install feeds:
```
./scripts/feeds update -a
./scripts/feeds install -a
```
Run OpenWRT configuration:
```
make menuconfig
```
Set:
```
Target system: Atheros AR7xxx/AR9xxx
Subtarget: Devices with NAND flash
Target images: tar.gz, squashfs
CSI: client_main, recvCSI and sendData mark as built-in (so it looks like <*>, not <M>)
```
Save & exit. Then run kernel configuration:
```
make kernel_menuconfig
```
Set:
```
Machine selection: Atheros AR71XX/AR724X/AR913X based boards
Atheros AR71XX/AR724X/AR913X machine selection: GL.iNet GL-AR750 and GL.iNet GL-AR750S support
```
Save & exit. Then build firmware:
```
make
```
Check that `bin/targets/ar71xx/nand/openwrt-ar71xx-nand-default-rootfs.tar.gz` contains following files:
```
/bin/recvCSI
/bin/sendData
/bin/client_main
/lib/modules/4.14.172/ar9003_csi.ko
```
