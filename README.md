## [raspberry安装及基本设置](SETUP.md)

## [docker安装及设置](docker.md)


## 摄像头应用

```sh
# 截图
raspistill -o image.jpg

# 生成视频文件
raspivid -o myvideo.h264 -t 10000

# 安装vlc软件
sudo apt-get install vlc
# 启动http视频流
sudo raspivid -o - -t 0 -fps 30|cvlc -vvv stream:///dev/stdin --sout '#standard{access=http,mux=ts,dst=:8080}' :demux=h264  
# 视频流播放软件地址：  http://192.168.1.63:8080


## 监控软件motion




docker run -it --network host --rm balenalib/raspberry-pi-debian:build bash


raspi-config 
1. Advanced Options --> A3 Memory Split --> 256MB


curl http://www.linux-projects.org/listing/uv4l_repo/lpkey.asc | sudo apt-key add -
echo "deb http://www.linux-projects.org/listing/uv4l_repo/raspbian/stretch stretch main" > /etc/apt/sources.list.d/jessie-backports.list
apt-get update
apt-get install uv4l uv4l-raspicam
apt-get install uv4l-raspicam-extras

apt-get install uv4l-decoder2 uv4l-encoder uv4l-renderer uv4l-server uv4l-webrtc uv4l-xmpp-bridge

apt-get install uv4l uv4l-server uv4l-raspicam uv4l-raspicam-extras
service uv4l_raspicam start
update-rc.d -f uv4l_raspicam enable

Video streaming from Raspberry Pi with UV4L
https://blog.domski.pl/video-streaming-from-raspberry-pi-with-uv4l/

安装docker：
https://blog.alexellis.io/getting-started-with-docker-on-raspberry-pi/



raspi-config


wiringpi
        Rasp PI的C编程

raspberry python gpio

rpi gpio python



ssh pi@raspberrypi.local

systemctl enable wpa_supplicant

      systemctl stop dnsmasq && systemctl stop hostapd && systemctl disable dnsmasq && systemctl disable hostapd && systemctl daemon-reload && service dhcpcd restart 

将RPi4从AP模式改为普通模式：
``` bash
apt-get remove -y hostapd dnsmasq

sed -i 's/^static/#static/' /etc/dhcpcd.conf &&

systemctl daemon-reload
service dhcpcd restart 
systemctl enable wpa_supplicant

cat > /boot/wpa_supplicant.conf << EOF
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
 ssid="TP-LINK_5EBBDC"
 psk="friendlycanoe511"
}
EOF

touch /boot/ssh

```

## 参考文献
- [Copying an operating system image to an SD card using Mac OS](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)
- [Cloning a Dual-Boot Hard Drive With dd](https://johnatilano.com/2011/05/21/53270156/)
- [Setting up a Raspberry Pi headless](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
- [How to save Power on your Raspberry Pi](https://learn.pi-supply.com/make/how-to-save-power-on-your-raspberry-pi/)
- [HEADLESS RASPBERRY PI 4 SSH WIFI SETUP (MAC + WINDOWS)](https://desertbot.io/blog/headless-raspberry-pi-4-ssh-wifi-setup)
- [How to install OpenCV4 on a Raspberry Pi with Python 3.7](https://samclane.dev/how-to-install-opencv4-on-a-raspberry-pi-with-python-37/)
- [raspberrypi3-opencv-docker](https://github.com/mohaseeb/raspberrypi3-opencv-docker)
- [Docker on Raspberry Pi](https://raspberry-valley.azurewebsites.net/OpenCV/)
- [Install OpenCV Python on Raspberry Pi 3](https://www.deciphertechnic.com/install-opencv-python-on-raspberry-pi/)
- [Install OpenCV 4 on Raspberry Pi 4 and Raspbian Buster](https://www.pyimagesearch.com/2019/09/16/install-opencv-4-on-raspberry-pi-4-and-raspbian-buster/)

