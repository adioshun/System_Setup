# Autoware

[Github](https://github.com/CPFL/Autoware), [Homepage](https://www.autoware.ai/)

## 1. 설치

apt-get install qtbase5-dev

```
% sudo apt-get install ros-indigo-desktop-full ros-indigo-nmea-msgs ros-indigo-nmea-navsat-driver ros-indigo-sound-play ros-indigo-jsk-visualization ros-indigo-grid-map ros-indigo-gps-common
% sudo apt-get install ros-indigo-controller-manager ros-indigo-ros-control ros-indigo-ros-controllers ros-indigo-gazebo-ros-control ros-indigo-sicktoolbox ros-indigo-sicktoolbox-wrapper ros-indigo-joystick-drivers ros-indigo-novatel-span-driver
% sudo apt-get install libnlopt-dev freeglut3-dev qtbase5-dev libqt5opengl5-dev libssh2-1-dev libarmadillo-dev libpcap-dev gksu libgl1-mesa-dev libglew-dev software-properties-common libyaml-cpp-dev python-flask python-requests
% sudo add-apt-repository ppa:mosquitto-dev/mosquitto-ppa
% sudo apt-get install libmosquitto-dev
```

NOTE: Please do not install ros-indigo-velodyne-pointcloud package. Please uninstall it if you already installed.


### 1.1 소스 설치 

Get Autoware by following steps. Then build and install it.

If you get the latest autoware form github
```shell
$ git clone https://github.com/CPFL/Autoware.git
$ cd Autoware/ros/src
$ catkin_init_workspace
$ cd ../
$ ./catkin_make_release
$ source devel/setup.bash
```

> Could NOT find GLEW -> `sudo apt-get install libglew-dev`

If you use archives:
```shell
$ wget http://www.pdsl.jp/app/download/10394444574/Autoware-beta.zip
$ unzip Autoware-beta.zip
$ cd Autoware-beta/ros/src
$ catkin_init_workspace
$ cd ../
$ ./catkin_make_release
$ source devel/setup.bash
```

### 1.2 Docker 설치 

```
docker pull kunfengchen/u14-indigo-autoware 
docker pull nownicked/autoware-x11running7
```

## 2. 실행

### 2.1 소스설치시 

### 2.2 Docker 설치시 

- xmanager - 연결 설정 - Connection/SSH/Tunneling/X11 Forwarding 체크, xManager체크 

- 도커 실생 
```
- docker run -it --rm \
   --net host \
   --env="DISPLAY" \
   --volume "$HOME/.Xauthority:/root/.Xauthority:rw" \
   --volume "$HOME/sharefolder:/sharefolder" \
   {Docker Image ID} /bin/bash
```

- 도커 내에서 

```
cd /src/Autoware/ros/
./run
```