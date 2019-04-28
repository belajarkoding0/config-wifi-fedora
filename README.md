# config-wifi-fedora
Konfigurasi wifi di linux Fedora

I have a HP laptop with a Broadcom BCM43228 wifi card. The following, taken from this blog post, worked for me:

wget http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
wget http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
rpm -iv rpmfusion-free-release-27.noarch.rpm
rpm -iv rpmfusion-nonfree-release-27.noarch.rpm
dnf clean all
dnf install akmod-wl kernel-devel
akmods --force
(If the last command gives you an error "Building and installing wl-kmod failed", it might be that you have installed the wrong architecture for the package akmod-wl. In this case, do the following:

dnf remove akmod-wl
dnf install akmod-wl.x86_64 
and retry the akmods --force command.)

Then do:

modprobe wl
iwconfig
The wlo1 wireless interface should be visible now. If it doesn't, do a systemctl restart NetworkManager
