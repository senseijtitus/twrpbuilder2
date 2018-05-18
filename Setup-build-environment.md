
***
**We assume you have latest version of ubuntu already installed on your pc**

***

# Installing packages

`sudo apt-get install bison build-essential curl flex git gnupg gperf libesd0-dev liblz4-tool libncurses5-dev libsdl1.2-dev libwxgtk2.8-dev libxml2 libxml2-utils lzop maven openjdk-7-jdk pngcrush schedtool squashfs-tools xsltproc zip zlib1g-dev`

**In addition to the above, for 64-bit systems, get these:**

`sudo apt-get install g++-multilib gcc-multilib lib32ncurses5-dev lib32readline-gplv2-dev lib32z1-dev`

**For Ubuntu 15.10 (wily) and newer, substitute:**

`lib32readline-gplv2-dev -> lib32readline6-dev`

# Installing java

*Add Java ppa*

`sudo add-apt-repository ppa:openjdk-r/ppa  `

`sudo apt-get update   `

`sudo apt-get install openjdk-7-jdk  `


**For Ubuntu 16.04 (xenial) and newer, substitute (additionally see java notes below):**

`libwxgtk2.8-dev -> libwxgtk3.0-dev`

`openjdk-7-jdk -> openjdk-8-jdk`
