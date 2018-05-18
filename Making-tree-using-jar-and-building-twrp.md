# Cloning common tree
`git clone https://github.com/TwrpBuilder/device_generic_twrpbuilder.git device/generic/twrpbuilder`

# Making tree using recovery image

Download the [latest jar](https://github.com/TwrpBuilder/twrpbuilder_tree_generator/releases/latest) and save in twrp folder in your home

type these commands in terminal

`java -jar TwrpBuilder-1.0-SNAPSHOT.jar -r recovery.img`

replace recovery.img with your file name and output should be like this

```
[androidlover5842@androidlover5842-pc twrp5]$ java -jar tb.jar -r recovery.img
Building tree using: recovery.img
Found gzip comression in ramdisk
Making omni_q417.mk
Making Android.mk
Making AndroidProducts.mk
Making kernel.mk
Generating fstab
/data ext4 /dev/block/mmcblk0p3
/system ext4 /dev/block/mmcblk0p6
/cache ext4 /dev/block/mmcblk0p2
found mt6735 platform
Found 64 bit arch
Build fingerPrint: Micromax/Q417/Q417:5.1/LMY47D/1446202623:user/release-keys
tree ready for q417 at device/micromax/q417
Warning :- Check recovery fstab before build```

in my case codename would be q417, so we will use q417 to build 

cd ~/twrp
. build/envsetup.sh
lunch omni_q417-eng
make -j4 recoveryimage