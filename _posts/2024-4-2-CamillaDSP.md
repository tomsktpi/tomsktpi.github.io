---
layout: post
title: CamillaDSP 2 для Volumio на OrangePi
---

Докер для Volumio под Windows:   

docker-compose.yml   

```
version: '2'
services:
  volumio:
    build: .
    tty: true
    stdin_open: true
    privileged: true
```


Dockerfile   
```
FROM debian:latest

RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y ca-certificates
RUN apt-get install -y curl
RUN apt-get install -y debootstrap
RUN apt-get install -y dosfstools
RUN apt-get install -y git
RUN apt-get install -y jq
RUN apt-get install -y kpartx
RUN apt-get install -y libssl-dev
RUN apt-get install -y lz4
RUN apt-get install -y lzop
RUN apt-get install -y md5deep
RUN apt-get install -y multistrap
RUN apt-get install -y parted
RUN apt-get install -y patch
RUN apt-get install -y pv
RUN apt-get install -y qemu-user-static
RUN apt-get install -y qemu-utils
RUN apt-get install -y qemu
RUN apt-get install -y squashfs-tools
RUN apt-get install -y sudo
RUN apt-get install -y u-boot-tools
RUN apt-get install -y wget
RUN apt-get install -y xz-utils
RUN apt-get install -y zip


WORKDIR /opt
RUN git clone https://github.com/volumio/volumio3-os.git build

```

В терминале:   
`cd ./build`  
`/build.sh -b armv7 -d orangepipc -v 2.0`  

Скачать имидж:   
`docker ps`  

`docker cp {CONTAINER ID}:/opt/build/Volumio-2.0-2024-03-30-orangepipc.zip Volumio-2.0-2024-03-30-orangepipc.zip`  


После запуска volumio:   
volumio:volumio   

{Swap}(https://phoenixnap.com/kb/swap-partition) на USB флешку  
`sudo fdisk /dev/sda`  
1 Type p and press Enter for an overview of the disk.  
2 Type n and press Enter to create a new partition. For partition type, enter p and press Enter.  
3 Enter the first available sector for the new partition and press Enter. You can also keep the default one offered   
4 Press p to verify the partition creation and confirm with Enter.   
5 Type t and press Enter to change the partition type. Change the value to 82 and press Enter.   
6 To proceed with the changes, type w, and press Enter.   

sudo partprobe /dev/sda  
sudo mkswap /dev/sda  

Готовим среду для Питона 3.8   
`sudo apt-get install -y build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev libffi-dev`  

`https://community.home-assistant.io/t/python-install-on-raspberry-pi-os/241558`  
`export version=3.8.1`  
`wget https://www.python.org/ftp/python/$version/Python-$version.tgz`  
`tar zxf Python-$version.tgz`  
`cd Python-$version`  
`./configure --enable-optimizations`  
`make -j4`  
`sudo make altinstall`  
`sudo apt -y autoremove`  


Ставим Руст для пакетов:  
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`  
		Выбрал complete  

Теперь cmake:  

`wget https://cmake.org/files/v3.16/cmake-3.16.0.tar.gz`   
`tar -xvzf cmake-3.4.1.tar.gz`  
`cd cmake-3.16.0`  
`sudo ./bootstrap`  
`sudo make`  
`sudo make install`  

`sudo apt-get install libjpeg62-turbo-dev`  

Теперь можно скачать {CamillaGUI}(https://github.com/HEnquist/camillagui-backend)  

Так как памяти мало придётся ставить пакеты отдельно  
`pip3.8 install aiohttp`  
`pip3.8 install numpy==1.24.4`   
`pip3.8 install matplotlib==3.7.5`  
`pip3.8 install camilladsp-plot[plot]@git+https://github.com/HEnquist/pycamilladsp-plot.git@v2.0.0`  

Добить:  
`pip3.8 install .`  

И вот теперь python3.8 main.py  

http://192.168.x.xxx:5005/  


![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ a
nd update the Hello World markdown file. F
or more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.