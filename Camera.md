# RaspberryPi

### "Enable Camera" in the menu and reboot

### Taking a picture in 2000ms, and save it to p1.jpg
> $ raspistill -o p1.jpg -t 2000

### Taking a Video 
- the desired length (in milliseconds) with "-t" option.
- the resolution to wxh, use "-w" and "-h" options.
> $ raspivid -o v1.h264 -t 10000 -w 1280 -h 720

#### Use MP4Box application that comes with gpac package.
> $ sudo apt-get install -y gpac

#### convert the raw H.264 video stream into .mp4 format with 10 frames per second:
>$ MP4Box -fps 30 -add v1.h264 v1.mp4

#### SMplayer can open mp4

### Shooting Time Lapse Images and Combining All Images into a Time Lapse Video
>$ mkdir img-lapse

>$ raspistill -o /home/pi/img-lapse/img%03d.jpg -tl 20000 -t 500000

The '-tl' option allows you to take a picture every 20 seconds. 

avconv
