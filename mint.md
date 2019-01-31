# mint

1. 安装ssh服务器
apt-get install openssh-server

2. 安装vnc服务器
https://community.linuxmint.com/tutorial/view/2334

mac 自带 vnc 客户端： Screen Sharing

3. 安装nfs服务器
sudo apt-get install -y nfs-kernel-server
sudo vi /etc/exports

加行：：：：
/media/win 10.0.0.1/8(ro,sync)

sudo exportfs -ra
showmount -e


vi /etc/fstab
/dev/sdb1						  /media/win	ntfs	defaults	0	0
mount -a

4. 安装chrome
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i ./..deb

5. 安装字体
mkdir /usr/share/fonts/chinese
cp 华文细黑.ttf /usr/share/fonts/chinese
mkfontscale
mkfontdir
fc-list

6. 安装wine
https://wiki.winehq.org/Ubuntu

7. 安装docker
https://gist.github.com/dweldon/39ca0536168a92815a56df44eb55a337

8. 安装vpn

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 61FF9694161CE595
vi /etc/apt/sources.list.d/sstp-client.list

deb http://ppa.launchpad.net/eivnaes/network-manager-sstp/ubuntu xenial main 
deb-src http://ppa.launchpad.net/eivnaes/network-manager-sstp/ubuntu xenial main 

（直接从软件包管理里面搜sstp，全部安装）

https://support.ivacy.com/kb/how-to-setup-vpn-on-linux-mint/#sstp


