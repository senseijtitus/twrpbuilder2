## TWRP Building Wiki

### Setup build environment
> Host OS: **`Ubuntu 16.04+`**(recommended) **` or BBQ LINUX `**
```bash
## BBQ LINUX users can skip these package installations, just update it by -> sudo pacman -Suy <-
# Required packages
sudo apt-get install bison build-essential g++-multilib git make python zip
# JDK
sudo apt-get install openjdk-8-jdk # Ubuntu 16.04+
or
sudo apt-get install openjdk-7-jdk # Ubuntu 14.04
```
> Create **`twrp`** dir:
> ```bash
>  mkdir ~/twrp && cd ~/twrp
>  ```

### Get a minimal TWRP source
> **Recommended version: [`omni_twrp_5.1_cleaned`](https://basketbuild.com/uploads/devs/yshalsager/CAS/twrp/omni_twrp-5.1.1_cleaned.tar.xz)**
>
>> Other versions: [**`TWRP Source releases`**](https://basketbuild.com/devs/yshalsager/CAS/twrp)
>
>> Get the right version of source i.e. don't try higher version then your stock ROM unless you're using a custom kernel which supports the latest source.

```bash
# Download the desired source (for ex: 5.1_norepo)
aria2c -x16 -s16 https://basketbuild.com/uploads/devs/yshalsager/CAS/twrp/omni_twrp-5.1.1_cleaned.tar.xz
# Extract the source:
tar -xvf omni_twrp-5.1.1_cleaned.tar.xz --directory ~/twrp/
```
### Clone common device tree
```bash
git clone https://github.com/TwrpBuilder/android_device_generic_twrpbuilder.git ~/twrp/device/generic/twrpbuilder
```
### Clone the remaining twrp source
```bash
git clone https://github.com/omnirom/android_bootable_recovery.git ~/twrp/bootable/recovery --depth=1
```
### Make device tree
>Download the latest [**`TWRP-Tree-Generator`**](https://github.com/TwrpBuilder/twrpbuilder_tree_generator/releases/latest) and save it in `~/twrp/`

> Put any working `recovery.img` in `~/twrp/`

> Make the device tree:
>```bash
>java -jar TwrpBuilder-1.0-SNAPSHOT.jar -r recovery.img
>```
>> Output be like this:
>```bash
>Building tree using: recovery.img
>Found gzip comression in ramdisk
>Making "omni_q417".mk
>Making Android.mk
>Making AndroidProducts.mk
>Making kernel.mk
>Generating fstab
>/data ext4 /dev/block/mmcblk0p3
>/system ext4 /dev/block/mmcblk0p6
>/cache ext4 /dev/block/mmcblk0p2
>found mt6735 platform
>Found 64 bit arch
>Build fingerPrint: Micromax/Q417/Q417:5.1/LMY47D/1446202623:user/release-keys
>tree ready for q417 at `device/micromax/q417`
>Warning :- Check recovery fstab before build
>```
>```bash
>Note down the "omni_q417" as it is needed for lunch ;)
>```
>```bash
> Verify `device/micromax/q417/recovery.fstab` for mount points
>```
### Build the TWRP
```bash
. build/envsetup.sh
lunch "omni_q417"-eng    #device code from previous step(without quotes)
make -j4 recoveryimage
```
### Troubleshooting
> Make sure you've **`openjdk`** not **`oraclejdk`**

> For **GCC 7.x** (`Ubuntu 17.10+`):
>> ```bash
>>export LC_ALL=C
>>```
>> also in file **`external/sepolicy/tools/check_seapp.c`**
>>add `__attribute__((fallthrough));` above line: 740
>>```C
>>	735:		else {
>>	736:	  		log_error(
>>	737:				"Unknown option character `\\x%x'.\n",
>>	738:				optopt);
>>	739: 		}
>>	740:		__attribute__((fallthrough));
>>	741:	default:
>>	742:		exit(EXIT_FAILURE);
>>	743:	}

> If you're facing error related to **`fstab.goldfish`**, like this: 
>>```bash
>>make: *** No rule to make target 'device/generic/goldfish/fstab.goldfish', needed by ..... Stop.
>>```
>> Clone **`device/generic/goldfish`** repo with the same version as the twrp source.
For instance, if you're using 5.1 source, use:
>>```bash
>>git clone https://android.googlesource.com/device/generic/goldfish -b android-5.1.1_r28 device/generic/goldfish
>>```