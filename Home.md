# TWRP Building Wiki

**We assume you have latest version of Ubuntu already installed on your pc and `$HOME/twrp/` is your working dir for all this.**

## 1. Getting twrp minimal manifest compressed sources
### Downloading

Get the right version of [Compressed Source](https://github.com/TwrpBuilder/twrp-sources/releases) i.e. don't try higher version then your stock rom unless you're using a custom kernel which supports the latest source.
We commonly use **5.1 norepo** for stable and debug builds.

### Extracting

Run this in dir where you've saved the compressed source:

` tar -xvf omni_twrp-{version}-{date}-norepo.tar.xz --directory $HOME/twrp/`

####  Note: 
- replace `omni_twrp-{version}-{date}-norepo.tar.xz` with the filename you've downloaded

## 2. Setting up build environment

### Installing packages

`sudo apt-get install bison build-essential curl flex git gnupg gperf libesd0-dev liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop maven openjdk-7-jdk pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev`

**In addition to the above, for 64-bit systems, get these:**

`sudo apt-get install g++-multilib gcc-multilib lib32ncurses5-dev lib32readline-gplv2-dev lib32z1-dev`

**For Ubuntu 15.10 (wily) and newer, substitute:**

`lib32readline-gplv2-dev -> lib32readline6-dev`

### Installing java

*Add Java ppa*

`sudo add-apt-repository ppa:openjdk-r/ppa  `

`sudo apt-get update   `

`sudo apt-get install openjdk-7-jdk  `


**For Ubuntu 16.04 (xenial) and newer, substitute (additionally see java notes below):**

`libwxgtk2.8-dev -> libwxgtk3.0-dev`

`openjdk-7-jdk -> openjdk-8-jdk`

## 3. Making tree using jar and building twrp
### Cloning common tree
`git clone https://github.com/TwrpBuilder/device_generic_twrpbuilder.git device/generic/twrpbuilder`

### Making tree using recovery image

- Download the latest [TWRP-Tree-Generator](https://github.com/TwrpBuilder/twrpbuilder_tree_generator/releases/latest) and save it in same dir with the source from previous step
- Run this
`java -jar TwrpBuilder-1.0-SNAPSHOT.jar -r recovery.img`
   - replace `recovery.img` with your file name and output should be like this
	```bash
	$ java -jar tb.jar -r recovery.img
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
	Warning :- Check recovery fstab before build
	```
### Finally building the TWRP

In my case codename is `q417`, so wI will use `q417` to build 
```bash
cd ~/twrp
. build/envsetup.sh
lunch omni_q417-eng
make -j4 recoveryimage
```
