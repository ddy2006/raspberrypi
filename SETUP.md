## raspberry安装及基本设置

### OS镜像文件下载
```sh
wget https://downloads.raspberrypi.org/raspios_full_armhf/images/raspios_full_armhf-2021-05-28/2021-05-07-raspios-buster-armhf-full.zip
```

### macos镜像文件写盘
```sh
# 在列出的磁盘中找到你的 SD 卡设备，例如 /dev/disk4
diskutil list

# unmount
diskutil unmountDisk /dev/disk2

# 找到你下载的镜像（解压的 .img 文件），写入到你的 SD 卡设备
sudo dd bs=1m if=/Users/kaichao/Desktop/Raspberrypi/2019-8-23-P.img of=/dev/rdisk2 conv=sync
```

### 设置wireless ssh
```sh
cat > /Volumes/boot/wpa_supplicant.conf << EOF
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
 ssid="TP-LINK_5EBBDC"
 psk="your-password"
}
EOF

touch /Volumes/boot/ssh

echo 'forcefsck' >> /Volumes/boot/cmdline.txt
```

### 登录树莓派

1. 用ssh登录
```
ip: 192.168.1.63
ssh登录：pi/raspberry
```

2. 配置并用vnc图形界面登录
```sh
raspi-config
# 选择 3.Interfacing Options，找到VNC，选择enable、Yes，完成后退出配置界面。
```
[参考]|(https://blog.csdn.net/weixin_43530173/article/details/108945305)

3. 配置并用Remote Desktop登录
```sh
sudo apt-get install -y xrdp

# 用Microsoft Remote Desktop登录
```

### 设置固定IP地址

编辑 /etc/dhcpcd.conf 文件，添加配置信息。
```
interface wlan0
static ip_address=192.168.1.63/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8
```

### 设置国内软件源
```sh
cat > /etc/apt/sources.list << EOF
deb https://mirrors.aliyun.com/raspbian/raspbian/ buster main contrib non-free rpi
deb-src https://mirrors.aliyun.com/raspbian/raspbian/ buster main contrib non-free rpi
EOF

cat > /etc/apt/sources.list.d/raspi.list << EOF
deb https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
EOF

# python软件源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

```
### 添加硬盘
以root用户执行以下命令：
```sh
# 在列出设备中，找到你的SD卡设备
fdisk -l 
# 将你的SD卡到挂载到/mnt/usb下
mkdir /home/pi/usb-disk
mount -t exfat /dev/sda1 /home/pi/usb-disk

# 找到那得img镜像，写入SD卡设备
# sudo dd bs=4M if=XXXX-raspbian.img of=/mnt/usb
# 最后拔出你的SD卡设备
```

### 安装常用工具
```sh
# 监控工具dstat
apt-get install -y dstat
# 压缩工具zstd
apt-get install -y zstd

```


### 安装文件共享服务器samba
```sh
apt-get install -y samba samba-common-bin

# 设置pi用户密码
smbpasswd -a pi

# 在Finder中可以找到树莓派，并访问共享目录

```

