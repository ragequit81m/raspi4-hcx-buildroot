# raspi4-hcx-buildroot

unter windows:
virtualbox installieren
vagrant installieren


Goals:
  hcxdump build on buildroot
	buildroot boot < 5 sec
	autostart hcxdumptool

Lets try:

Windows:Powershell for buildroot image:
(new-object System.Net.WebClient).DownloadFile("https://buildroot.org/downloads/Vagrantfile","Vagrantfile");
vagrant up

start the buildrootshell within Virtualbox
stop it and add more CPU cores and ram to the virtualbox config to make it faster
start the buildrootshell image

username/PW: vagrant/vagrant

cd buildroot-2023....

make raspberrypi4_64_defconfig
make 				to test standart build

now connect to virtualmaschine with filemanager and make a folder and copy 
hcdumptool-6.3.2.tar.gz to home/vagrant/buildroot-2023.08.02/dl/hcxdumptool

make folder:home/vagrant/buildroot-2023.08.02/package/hcxdumptool

Put both files there

hcxdumptool.mk:
################################################################################
#
# hcxdumptool
#
################################################################################

HCXDUMPTOOL_VERSION = 6.3.2
HCXDUMPTOOL_SITE = https://github.com/ZerBea/hcxdumptool/releases/download/6.3.2
HCXDUMPTOOL_LICENSE = GPL-3.0+
HCXDUMPTOOL_LICENSE_FILES = COPYING

$(eval $(autotools-package))
)


Config.in:
config BR2_PACKAGE_HCXDUMPTOOL
	bool "hcxdumptool"
	select BR2_PACKAGE_LIBPCAP
	help
	  The hcx dumper

	  hcx is a nice command-line tool.

	  https://github.com/ZerBea



add a line @
home/vagrant/buildroot-2023.08.02/package/hcxdumptool/config.in
change
	source "package/gzip/Config.in"
	source "package/lrzip/Config.in"
to
	source "package/gzip/Config.in"
	source "package/hcxdumptool/Config.in"
	source "package/lrzip/Config.in"


i just placed it in the compression structur to find it faster

make menuconfig

testconfig i tried so far:

Filesystem image - exactsize 300M
compressor decompressors

development tools
	git
	git-crypt
	pkgconfig
hardware handling
	lshw
	rtl drivers
interpreter??
	python3???
Libraries
	crypto
		libssh
		openssl binary
		openssl additional engine
Miscellaneous
	networking application
		aircrack
		dropbear
		iproute2
		sslh
		wireless tools
	shell and security
		sudo
	texteditor
		nano
networking aplication
	crda
	iw




make


connect to filesystem vagrant/vagrant
go to /home/vagrant/buildroot-2023.08.2/output/images/sdcard.img
flash it on sd card






















dont need ?
sudo apt install sed make binutils gcc g++ bash patch \gzip bzip2 perl tar cpio python unzip rsync wget libncurses-dev


make menuconfig



command to load wifi driver:
modprobe -a 88XXau
iw dev wlan0 set txpower fixed 2300
iw dev wlan0 set type monitor


checking for:
kmod
ethtool
iw
util-linux
wireless_tools
rfkill
modinfo^
ssh
wget
curl
ip iw
nettols
insmod
lsusb


crda
iw
.
