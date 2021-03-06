# TI mmwave RADAR

## 초기 설치 \(윈도우 권장\)

> DCA1000EVM대신 IWR 1642에 직접 연결 후 작업, [\[Ref Tutorial\]](https://training.ti.com/mmwave-sdk-evm-out-box-demo)

1. usb 드라이버 다운로드 : [IWR1642: stand alone XDS110 drivers](https://downloads.ti.com/downloads/dsps/dsps_public_sw/sdo_ccstudio/emulation/ti_emupack_setup_8.0.903.4_win_32.exe?__gda__=1547020113_3fbdeab41d0759de936f41c4cc3e13e7), http://processors.wiki.ti.com/index.php/XDS_Emulation_Software_Package

2. 롬\(??\) 업데이트 [\[UniFlash v4 User Guide for mmWave Devices\]](http://processors.wiki.ti.com/images/f/f5/Mmwave_uniflash_user_guide_v1.0.pdf)

   * 업데이터 툴 설치 : [다운로드](http://processors.wiki.ti.com/index.php/Category:CCS_UniFlash)
   * xwr16xx\_mmw\_demo.bin 다운로드 : [sdk 설치시](http://www.ti.com/tool/MMWAVE-SDK) 자동 다운로드 \(`C:\ti\mmwave_sdk_02_01_00_04\packages\ti\demo\xwr16xx\mmw`\)
   * 점퍼 설정 : SOP2 연결 -&gt; 재부팅 
   * 툴 실행 
   * 윈도우 장치 관리자 에서 포트 번호 확인 후 `XDS110 Class Application/User UART`를 설정에 입력
   * 점퍼 원복 

3. 확인 : [mmWave Demo Visualizer](https://dev.ti.com/gallery/view/mmwave/mmWave_Demo_Visualizer/ver/3.1.0/), [\[메뉴얼 \]](http://www.ti.com/lit/ug/swru529b/swru529b.pdf)

## Uniflash 설치

> 펌웨어\(??\) 설치 툴

* linux : 'sudo apt-get install libusb-dev' -&gt; `sudo ./uniflash_sl.4.5.0.2056.run`
* windows : 
* Webapp : [Uniflash](https://dev.ti.com/uniflash/#!/)

```
    <param name="command_port" value="/dev/ttyACM0"  />
    <param name="command_rate" value="115200"   />
    <param name="data_port" value="/dev/ttyACM1"  />
    <param name="data_rate" value="921600"   />
```

---

## [TI Resouce Explorer](http://dev.ti.com/tirex/#/)

* [Traffic Monitoring Overview](http://dev.ti.com/tirex/#/?link=Software%2FmmWave Sensors%2FIndustrial Toolbox%2FLabs%2FTraffic Monitoring)
* [ROS Point Cloud Visualizer](http://dev.ti.com/tirex/#/?link=Software%2FmmWave Sensors%2FIndustrial Toolbox%2FLabs%2FROS Point Cloud Visualizer)
* People Counting Demo : [설명자료](https://training.ti.com/kr/mmwave-sensors-people-counting-demo-english?cu=1128486), [pdf](https://training.ti.com/sites/default/files/docs/MainDemoSlidesMAINEDIT_V1p11_0.pdf)
* Zone Occupancy Detection 
* Gesture Recognition 

> 사전 설치 : [Matlab runtime\_R2017a \(9.2\)](https://kr.mathworks.com/products/compiler/matlab-runtime.html)

---

## ROS 연계 \(ubuntu\)

> \[TI mmWave ROS Driver Setup Guide: [pdf](http://dev.ti.com/tirex/content/mmwave_training_1_6_1/labs/lab0006-ros-driver/lab0006_ros_driver_pjt/TI_mmWave_ROS_Driver_Setup_Guide.pdf) , [공식](http://dev.ti.com/tirex/#/?link=Software%2FmmWave Sensors%2FIndustrial Toolbox%2FLabs%2FROS Point Cloud Visualizer), [깃허브](https://github.com/ibcn-cloudlet/ti_mmwave_rospkg), [깃허브-개선버젼](https://github.com/radar-lab/ti_mmwave_rospkg)

```python
sudo apt-get install ros-kinetic-pcl-ros ros-kinetic-pcl-msgs ros-kinetic-pcl-conversions ros-kinetic-perception-pcl
cd ~/catkin_ws/src
git clone https://github.com/radar-lab/ti_mmwave_rospkg.git
git clone https://github.com/wjwwood/serial.git
cd ~/catkin_ws
catkin_make

sudo chmod 666 /dev/ttyACM0
sudo chmod 666 /dev/ttyACM1

roslaunch ti_mmwave_rospkg 1642es2_short_range.launch

rostopic echo /ti_mmwave/radar_scan
```

> 에러 발생시 참고 : [https://github.com/radar-lab/ti\_mmwave\_rospkg\#troubleshooting](https://github.com/radar-lab/ti_mmwave_rospkg#troubleshooting)


## TI Radar CNN

https://github.com/radar-lab/ti-mmwave-cnn

---

## [mmWave software development kit \(SDK\)](http://www.ti.com/tool/MMWAVE-SDK)

* 다운로드\(Linus\) : [http://software-dl.ti.com/ra-processors/esd/MMWAVE-SDK/lts-latest/exports/mmwave\_sdk\_02\_01\_00\_04-Linux-x86-Install.bin](http://software-dl.ti.com/ra-processors/esd/MMWAVE-SDK/lts-latest/exports/mmwave_sdk_02_01_00_04-Linux-x86-Install.bin)
* chmod +x \*.bin
* [User Guide](https://e2e.ti.com/cfs-file/__key/communityserver-discussions-components-files/1023/mmwave_5F00_sdk_5F00_user_5F00_guide-_2800_1_2900_.pdf)

---

# Code Composer Studio\(CCS\)

Download the latest CCS : [http://processors.wiki.ti.com/index.php/Download\_CCS](http://processors.wiki.ti.com/index.php/Download_CCS)

---

# mmWaveLib

* [SDK 메뉴얼](http://software-dl.ti.com/ra-processors/esd/MMWAVE-SDK/latest/exports/mmwave_sdk_user_guide.pdf) 50page
* mmWaveLib is a collection of algorithms that provide basic functionality needed for FMCW radar-cube processing. 
* This component is available for **xWR16xx** only and contains optimized library routines for C674 DSP architecture only. 

### DCA1000EVM

* DCA1000EVM\([http://www.ti.com/tool/DCA1000EVM\)은](http://www.ti.com/tool/DCA1000EVM%29은) TI mmWave EVM과 연결하여 Raw ADC 데이터 캡쳐를 할 수 있게 하는 인터페이스 보드입니다.
* [홈페이지](http://www.ti.com/tool/dca1000evm)
* [Quick Start Guide](http://www.ti.com/lit/ml/spruik7/spruik7.pdf)
* [User guide](http://www.ti.com/lit/ug/spruij4/spruij4.pdf)
* [드라이버/mmWave studio](https://downloads.ti.com/downloads/ra-processors/esd/MMWAVE-STUDIO/latest/mmwave_studio_02_00_00_02_win32.exe?__gda__=1547022129_a6064df5c19ef3383b7510adfe062512)

---

# UART Read

\[\[[http://processors.wiki.ti.com/index.php/Linux\_Core\_UART\_User's\_Guide\]\(http://processors.wiki.ti.com/index.php/Linux\_Core\_UART\_User's\_Guide\]\(http://processors.wiki.ti.com/index.php/Linux\_Core\_UART\_User's\_Guide\]\(http://processors.wiki.ti.com/index.php/Linux\_Core\_UART\_User's\_Guide\)\](http://processors.wiki.ti.com/index.php/Linux_Core_UART_User's_Guide]%28http://processors.wiki.ti.com/index.php/Linux_Core_UART_User's_Guide]%28http://processors.wiki.ti.com/index.php/Linux_Core_UART_User's_Guide]%28http://processors.wiki.ti.com/index.php/Linux_Core_UART_User's_Guide%29\)\)

[https://github.com/nsekhar/serialcheck](https://github.com/nsekhar/serialcheck)

```
~/serialcheck$ gcc -o serialcheck serialcheck.c CROSS_COMPILE=arm-linux-gnueabihf-
~/serialcheck$ gcc -o serialstats serialstats.c CROSS_COMPILE=arm-linux-gnueabihf-

serialstats -d /dev/ttySX -i 1 &
```

## Commnad CLI 접속

* 센서 :  \(C:\ti\mmwave\_sdk\_02\_01\_00\_04\packages\ti\demo\xwr16xx\mmw\)로 플래싱
* 실행 : roslaunch rviz\_1642\_2d.launch \#실행 안해도 자동으로 값 출력 
* 확인 : moserial -&gt; data port 지정 ,  echo uncheck

---

## 설정

![](https://i.imgur.com/EIirwPZ.png)

```
cat /dev/ttyS1
echo "hi" > /dev/ttyS1
```

Configuration \(.cfg\) File Format : [SDK 메뉴얼](http://software-dl.ti.com/ra-processors/esd/MMWAVE-SDK/latest/exports/mmwave_sdk_user_guide.pdf) 14page

[mmWave sensing Estimation](https://dev.ti.com/gallery/view/1792614/mmWaveSensingEstimator/ver/1.3.0/)툴을 이용하여 설정값 변경이 더편함  
[샘플 cfg](http://dev.ti.com/tirex/content/mmwave_industrial_toolbox_3_1_1/.metadata/.html/chirps.html) 다운 받아 사용 권장

---

# RawData 파싱

[mmw Demo Data Structure v0.1](https://e2e.ti.com/cfs-file/__key/communityserver-discussions-components-files/1023/mmw-Demo-Data-Structure_5F00_8_5F00_16_2D00_7.pdf): Out-of-box Demo 플래슁

```python
#!/usr/bin/env python3
# coding: utf-8

from __future__ import print_function
#import warnings; warnings.simplefilter('ignore')
import os
import sys
sys.path.append("/workspace/include")
import pcl_helper

import rospy
from sensor_msgs.msg import PointCloud2
import sensor_msgs.point_cloud2 as pc2


import pcl
import pcl_msg


import struct
import sys
import time
import numpy as np

import math

def rect(r, theta):
    """theta in degrees

    returns tuple; (float, float); (x,y)
    """
    x = r * math.cos(theta) #math.cos(math.radians(theta))
    y = r * math.sin(theta) #math.sin(math.radians(theta))
    return x,y

def polar(x, y):
    """returns r, theta(degrees)
    """
    r = (x ** 2 + y ** 2) ** .5
    if y == 0:
        theta = 180 if x < 0 else 0
    elif x == 0:
        theta = 90 if y > 0 else 270
    else:
        theta = math.degrees(math.atan(float(y) / x))
    return r, theta


def validateChecksum(header):
    #h = typecast(uint8(header),'uint16');
    header = np.uint8(header)
    h = np.array(header, dtype=np.uint16)
    #a = uint32(sum(h));
    a = sum(h)
    a = np.uint32(a)
    #b = uint16(sum(typecast(a,'uint16')));
    b = np.array(a, dtype=np.uint16)
    b = sum(b)
    b = np.uint16(b)
    #CS = uint16(bitcmp(b));
    CS = ~b
    CS = np.uint16(CS)
    return CS




def parsePoint(data, tlvLength):    # Type : x06
    point_data = np.zeros([tlvLength/struct.calcsize('4f'),3],dtype=np.float32)
    for i in range(tlvLength/struct.calcsize('4f')):
        if(struct.calcsize('4f') == len(data[16*i:16*i+16])):
            parse_range, parse_angle, parse_doppler, parse_snr = struct.unpack('4f', data[16*i:16*i+16])  #struct.unpack('3H3h', data[4+12*i:4+12*i+12]) # heder 4, payload 12
            #print("Point : {}, {}".format(parse_range, parse_angle))
            x,y = rect(parse_range, parse_angle)
            datas = np.array([x,y,0])
            point_data[i,]=datas
            #np.append(point_data, datas)
            #point_data = np.vstack((point_data,datas))
        else:
            # print("** parsePoint Error [{}]**".format(len(data[16*i:16*i+16])))
            pass
    
    #pc = pcl.PointCloud(point_data)
    #pcl_xyzrgb = pcl_helper.XYZ_to_XYZRGB(pc, [255,255,255])  
    #out_ros_msg = pcl_helper.pcl_to_ros(pcl_xyzrgb)
    #pub_point.publish(out_ros_msg)

def parseTargetIndex(data, tlvLength):    # Type : x08   
    index_data = np.zeros([tlvLength/struct.calcsize('B'),3],dtype=np.float32)  # 'I16f' for little endian , '>I16f' for big endian 
    for i in range(tlvLength/struct.calcsize('B')):
        if(struct.calcsize('B') == len(data[1*i:1*i+1])):
            targetID  = struct.unpack('B', data[1*i:1*i+1])  #76, 144, 212, 280
            print("TargetID : {}".format(targetID))
            datas = np.array([targetID,0,0])
            index_data[i,]=datas
            #np.append(taget_data, datas)
            #point_data = np.vstack((taget_data,datas))
        else:
            print("** parseTargetIndex Error [{}]**".format(len(data[1*i:1*i+1])))
            #pass



def parseTargetList(data, tlvLength):    # Type : x07
    target_data = np.zeros([tlvLength/struct.calcsize('I16f'),3],dtype=np.float32)  # 'I16f' for little endian , '>I16f' for big endian 
    for i in range(tlvLength/struct.calcsize('I16f')):
        if(struct.calcsize('I16f') == len(data[68*i:68*i+68])):
            tid, posX, posY, velX, velY, accX, accY, EC1, EC2,EC3,EC4,EC5,EC6,EC7,EC8,EC9, g  = struct.unpack('I16f', data[68*i:68*i+68])  #76, 144, 212, 280
            print("Detect[{}] : {}, {}".format(tid, posX, posY))
            datas = np.array([posX,posY,0])
            target_data[i,]=datas
            #np.append(taget_data, datas)
            #point_data = np.vstack((taget_data,datas))
        else:
            print("** parseTargetList Error [{}]**".format(len(data[68*i:68*i+68])))
            #pass

    #pc = pcl.PointCloud(target_data)
    #pcl_xyzrgb = pcl_helper.XYZ_to_XYZRGB(pc, [255,255,255])  
    #out_ros_msg = pcl_helper.pcl_to_ros(pcl_xyzrgb)
    #pub_track.publish(out_ros_msg)

def tlvHeader(data):
    while data:       
        headerLength = 52
        try:
            magic, version, platform, cpuCycles, length, frameNum, subframeNumber, chirpMargin, frameMargin, uartSentTime, trackProcessTime, numTLVs, checksum = struct.unpack('Q10I2H', data[:headerLength])        
            #print("numTLVs : ", numTLVs)
            #print("length : ", length-52) #exclude header length 52
        except:
            break
        
        """checksum
        header = struct.unpack('52c', data[:headerLength])
        cs = validateChecksum(header)
        print (" checksum : {} == {}".format(cs, checksum))
        """

        pendingBytes = length - headerLength
        data = data[headerLength:]

        for i in range(numTLVs):
            if (len(data) != 0): 
                tlvType, tlvLength = tlvHeaderDecode(data[:8])                               
                data = data[8:]  # after TLV header 
                if (tlvType == 6):
                    parsePoint(data, tlvLength-8)
                elif (tlvType == 7):
                    parseTargetList(data, tlvLength-8)               
                elif (tlvType == 8): 
                    parseTargetIndex(data, tlvLength-8) 
                else:                    
                    print("- Unidentified tlv type :", hex(tlvType))  # this line print 0x02, 0x04
                data = data[tlvLength:]
                pendingBytes -= (8+tlvLength)
        data = data[pendingBytes:]
        yield length, frameNum

def tlvHeaderDecode(data):    
    if(struct.calcsize('2I') == len(data)):
        tlvType, tlvLength = struct.unpack('2I', data)
        return tlvType, tlvLength
    else:
        return 0,0


if __name__ == "__main__":
    
    #rospy.init_node('radar', anonymous=True)
    #pub_point = rospy.Publisher("/radar_point", PointCloud2, queue_size=1)
    #pub_track = rospy.Publisher("/radar_track", PointCloud2, queue_size=1)
    
    if sys.byteorder == "little":
        print("Little-endian platform.")
    else:
        print("Big-endian platform.")

    fileName = "/dev/ttyACM1"
    rawDataFile = open(fileName, "rb")
    print("Read Data From : ", fileName)    
    while(1):
        rawData = rawDataFile.read()
        magic = b'\x02\x01\x04\x03\x06\x05\x08\x07'
        offset = rawData.find(magic)
        rawData = rawData[offset:]
        for length, frameNum in tlvHeader(rawData):
		    continue





```

---

# People tracking Demo

> * C:\ti\mmwave\_industrial\_toolbox\_3\_1\_1\labs\lab0011-pplcount\lab0011\_pplcount\_quickstart\

```
===========================================================
[IWR1642] v3.1.1
===========================================================
dfeDataOutputMode 1
channelCfg 15 3 0
adcCfg 2 1
adcbufCfg 0 1 1 1
profileCfg 0 77 30 7 62 0 0 60 1 128 2500 0 0 30
chirpCfg 0 0 0 0 0 0 0 1
chirpCfg 1 1 0 0 0 0 0 2
frameCfg 0 1 128 0 50 1 0
lowPower 0 1
guiMonitor 1 1 0 0
cfarCfg 6 4 4 4 4 16 16 4 4 50 62 0
doaCfg 600 1875 30 1
SceneryParam -6 6 0.05 6
GatingParam 4 3 2 0
StateParam 10 5 10 100 5
AllocationParam 450 0.01 25 1 2
VariationParam 0.289 0.289 1.0
PointCloudEn 1
trackingCfg 1 2 250 20 200 50 90
sensorStart

left wall: -6
R wall: 6
front wall: 6
back wall: 0
------------------
```

```
===========================================================
[IWR6843] v3.1.1
===========================================================
flushCfg
dfeDataOutputMode 1
channelCfg 15 5 0
adcCfg 2 1
adcbufCfg 0 1 1 1
profileCfg 0 60.6 30 10 62 0 0 53 1 128 2500 0 0 30
chirpCfg 0 0 0 0 0 0 0 1
chirpCfg 1 1 0 0 0 0 0 4
frameCfg 0 1 128 0 50 1 0
lowPower 0 1
guiMonitor 1 1 0 0
cfarCfg 6 4 4 4 4 16 16 4 4 50 62 0
doaCfg 600 1875 30 1 1 0
SceneryParam -6 6 0.5 6
GatingParam 4 3 2 0
StateParam 10 5 100 100 5
AllocationParam 250 250 0.25 10 1 2
AccelerationParam 1 1 1
trackingCfg 1 2 250 20 52 82 50 90
sensorStart

left wall: -6
R wall: 6
front wall: 6
back wall: 0
------------------
```

```
var getXYZ_type2 = function (vec, vecIdx, Params, numDetecObj, sizeObj) 
{
    var x_coord = [];
    var y_coord = [];
    var z_coord = [];
    var doppler = [];
    var i, startIdx;
    var subFrameNum = Params.currentSubFrameNumber;

    /* list of detected objs
    for platform = 68xx
    typedef struct DPIF_PointCloudCartesian_t
    {
        x - coordinate in meters
        float  x;
        y - coordinate in meters
        float  y;
        z - coordinate in meters
        float  z;        
        Doppler in m/s 
        float    doppler;
    }DPIF_PointCloudCartesian;
    */
    for (i = 0; i < numDetecObj; i++)  
    {
        /*start index in bytevec for this detected obj*/
        startIdx = vecIdx + i*sizeObj;

        x_coord[i] = getFloat(vec[startIdx + 0],  vec[startIdx + 1],  vec[startIdx + 2],  vec[startIdx + 3]);
        y_coord[i] = getFloat(vec[startIdx + 4],  vec[startIdx + 5],  vec[startIdx + 6],  vec[startIdx + 7]);
        z_coord[i] = getFloat(vec[startIdx + 8],  vec[startIdx + 9],  vec[startIdx + 10], vec[startIdx + 11]);
        doppler[i] = getFloat(vec[startIdx + 12], vec[startIdx + 13], vec[startIdx + 14], vec[startIdx + 15]);
    }

    var range;
    range = math.sqrt(math.add(math.dotMultiply(z_coord, z_coord), math.add(math.dotMultiply(x_coord, x_coord), math.dotMultiply(y_coord, y_coord))));

    var rangeIdx = math.map(range, function (value) {
        return Math.round(value / Params.dataPath[subFrameNum].rangeIdxToMeters);
    });

    var dopplerIdx = math.map(doppler, function (value) {
        return Math.round(value / Params.dataPath[subFrameNum].dopplerResolutionMps);
    });

    return { rangeIdx: rangeIdx, dopplerIdx: dopplerIdx, x_coord: x_coord, y_coord: y_coord, z_coord: z_coord, doppler: doppler}

}
```

---

* [TI 포럼](https://e2e.ti.com/support/sensors/f/1023)

* ttyS0 is the device for the first UART serial port on x86 and x86\_64 architectures. If you have a PC motherboard with serial ports you'd be using a ttySn to attach a modem or a serial console.

* ttyUSB0 is the device for the first USB serial convertor. If you have an USB serial cable you'd be using a ttyUSBn to connect to the serial port of a router.

* ttyAMA0 is the device for the first serial port on ARM architecture. If you have an ARM-based TV box with a serial console and running Android or OpenELEC, you'd be using a ttyAMAn to attach a console to it.

![](https://i.imgur.com/79W5Hj4.png)

Since there is no guide explaining the data output structure, you will have to view the source code to understand the output.  You will be interested in three files

* `mss_main.c`,: transmits the data, 
* `mmw_messages.h` and `<SDK_INSTALL_DIR>/packages/ti/demo/io_interface/mmw_output.h`:define the output. 



## 