# Realtime Stream with RaspiCam 

livestreaming with raspberry pi 3, raspicam module and mjpg-streamer

## Installation

Update the raspberry pi
```
sudo apt-get update
sudo apt-get -y upgrade
```

reboot

Also update the firmware versions
```
sudo rpi-update
```

reboot

Enable camera module in raspi-config
```
sudo raspi-config
```

in menu Interface Options => enable camera
after that, reboot again

Enable v4l2 module
```
sudo modprobe bcm2835-v4l2
```

add bcm2835-v4l2 to /etc/modules to enable it for auto-loading

verify the interface

```
ls -l /dev/video0
```

Install some dependencies
```
sudo apt-get install libjpeg8-dev imagemagick
```

Go to mjpg-directory and patch the version
```
cd mjpg-streamer
patch -p0 < ../input_uvc_patch
```

Compile it
```
make
```

and install it
```
sudo make install
```

### Test
```
export LD_LIBRARY_PATH=~/mjpg-streamer
./mjpg_streamer -i "input_uvc.so -d /dev/video0 -r 640x480 -f 30" -o "output_http.so -w ./www"
```
or

```
/home/pi/raspberry-live-stream/mjpg-streamer/mjpg_streamer -i "/home/pi/raspberry-live-stream/mjpg-streamer/input_uvc.so -d /dev/video0 -r 1280x768 -f 30" -o "/home/pi/raspberry-live-stream/mjpg-streamer/output_http.so -w /home/pi/raspberry-live-stream/mjpg-streamer/www -p 8080" 
```

### Sources
Source: https://www.raspberrypi.org/forums/viewtopic.php?t=77796 - pulled on 15th of april 2018
SourcePatch: https://www.raspberrypi.org/forums/viewtopic.php?p=687356#p687356
