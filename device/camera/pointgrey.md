# PointGrey

[BFLY-PGE-31S4C-C](http://www.av-iq.com/avcat/ctl17578/index.cfm?manufacturer=point-grey-research-flir&product=bfly-pge-31s4c-c) : Blackfly 3.2 MP Color GigE PoE (Sony IMX265), 2048x1536 


## 2. PointGrey for ROS

### 2.1 Apt install

apt-get install ros-kinetic-pointgrey-camera-driver #ubuntu 18은 지원 안함 

### 2.2 Source install

[pointgrey\_camera\_driver](http://wiki.ros.org/pointgrey_camera_driver)

```
cd ~/catkin_ws/src/ && git clone https://github.com/ros-drivers/pointgrey_camera_driver.git
cd pointgrey_camera_driver
rosdep install --from-paths ./ --ignore-src --rosdistro $ROS_DISTRO -y
cd ~/catkin_ws/ && catkin_make
```


### 2.4 테스트 

List detected cameras:`rosrun pointgrey_camera_driver list_cameras`

Launch camera: `roslaunch pointgrey_camera_driver camera.launch`

여러 카메라 실행 : `roslaunch pointgrey_camera_driver camera.launch camera_serial:=12345678`

---

### 2.1 자체 툴 (IP등 카메라 설정)

[Getting Started with FlyCapture 2.x and Linux](https://www.ptgrey.com/KB/10548)

#### A. flycapture2 \(ubuntu 14, 16\)

1. Download : flycapture2-2.9.3.43-amd64-pkg.tgz [\[Link\]](https://www.ptgrey.com/support/downloads)
   - `wget https://github.com/adioshun/gitBook_SystemSetup/raw/master/09device-setup/flycapture2-2.9.3.43-amd64-pkg.tgz`

2. Dependent Package

   * Ubuntu 16.04: `sudo apt-get install libraw1394-11 libgtkmm-2.4-1v5 libglademm-2.4-1v5 libgtkglextmm-x11-1.2-dev libgtkglextmm-x11-1.2 libusb-1.0-0`
   * Ubuntu 14.04: `sudo apt-get install libraw1394-11 libgtkmm-2.4-1c2a libglademm-2.4-1c2a libgtkglextmm-x11-1.2-dev libgtkglextmm-x11-1.2 libusb-1.0-0 libglademm-2.4-dev`
   * Ubuntu 12.04: `sudo apt-get install libraw1394-11 libgtk2.0-0 libgtkmm-2.4-dev libglademm-2.4-dev libgtkglextmm-x11-1.2-dev libusb-1.0-0 libglademm-2.4-dev`

3. echo "raw1394" >> /etc/modules #  add the raw1394 module to be loaded on start.  

4. `sudo sh install_flycapture.sh`

5. Validation

   ```
   cp -R /usr/src/flycapture ~
   cd ~/flycapture/src/FlyCapture2Test
   make
   FlyCapture2Test
   ```

6. Run

   * Applications -&gt; Point Grey Research -&gt; FlyCapture
   * `$ FlyCap2`


에러 : `could not find glade file 'FlyCapture2GUI_GTK.glade` -> 'locate FlyCapture2GUI_GTK.glade` -> copy to `~/flycapture/src/FlyCapture2Test`

> [Getting Started with FlyCapture 2.x and Linux](https://www.ptgrey.com/tan/10548)

#### B. Spinnaker \(Strongly recommended ubuntu 16\)

1. Download

2. Dependent package

   * Ubuntu 16.04: `sudo apt-get install libavcodec-ffmpeg56 libavformat-ffmpeg56   libswscale-ffmpeg3 libswresample-ffmpeg1 libavutil-ffmpeg54 libusb-1.0-0`

3. `sudo sh install_spinnaker.sh`




#### C. PointGrey for Python : [PyFlyCap2](https://matham.github.io/pyflycap2/index.html)

pip install pyflycap2


---

Ethernet 기반 카메라 데이터 전송을 위한 전처리 

```python
sudo sysctl -w net.core.rmem_max=1048576 net.core.rmem_default=1048576
sudo sh -c 'echo 1024 > /sys/module/usbcore/parameters/usbfs_memory_mb'
 
echo "net.core.rmem_max=1048576" >> /etc/sysctl.conf
echo "net.core.rmem_default=1048576" >> /etc/sysctl.conf

sudo sysctl -p
```



| 에러코드 | 해결책 |
| --- | --- |
| Failed to start with error: PointGreyCamera::start Failed to start capture \| FlyCapture2::ErrorType 33 Error starting isochronous stream | [reducing the frame rate](https://stackoverflow.com/questions/12070778/trouble-in-driving-point-grey-grasshoper-cameras) `modprobe usbcore usbfs_memory_mb=1024` <br>[\[영구 설정\]](https://stackoverflow.com/questions/43297480/failed-isochronous-start-error-0x2-when-starting-reading-from-2-cameras-ptgre) |
| IMAGE\_CONSISTENCY\_ERRORS | [sudo sysctl -w net.core.rmem\_max=1048576 net.core.rmem\_default=1048576](http://www.ptgrey.com/KB/10016), <br>Packet size 중간, Packet delay 높게, Jumbo packet\(MTU\) 최대 |
| Low level failure writing register 0x60c with value 0x8004. Error: 0x3 |  |
| FlyCapture2::ErrorType 1 Failed to discover GigE packet size | `sudo ip link set eth0 mtu 9000`<br> `ip link show eth0` |




https://answers.ros.org/question/258537/pointgrey-camera-works-only-once/








