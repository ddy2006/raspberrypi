### 安装docker及docker-compose
```sh
# 安装docker软件
curl -sSL https://get.docker.com | sh
# pi用户加入到docker组中
usermod -aG docker pi
systemctl enable docker
systemctl start docker

# Install pip if not available
apt update
apt install -y python python-pip

# 设置python3为缺省
rm /usr/bin/python
cd /usr/bin && ln -s python3 python

# Install Docker Compose from pip
pip install docker-compose

```
### 启动web服务器nginx
```sh
docker run -it -p 80:80 tobi312/rpi-nginx

# 通过 http://192.168.1.63/ 访问
```
