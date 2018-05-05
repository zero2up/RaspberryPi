*Ref*:

[树莓派中PiCamera+OpenCV的使用](https://blog.csdn.net/u012005313/article/details/70244747)
[Picamera.camera](http://picamera.readthedocs.io/en/release-1.13/_modules/picamera/camera.html#PiCamera.capture)

### Image

#### Image连拍保存
```
def capture_multi():
    with PiCamera() as camera:
        camera.resolution = (320, 240)
        camera.vflip = True #上下翻转

        for n in range(5):
            sleep(n)
            camera.capture("Img_" + str(n) + ".jpg", resize=(80, 60))
```
format:

     'jpeg' - Write a JPEG file
     'png'  - Write a PNG file
     'gif'  - Write a GIF file
     'bmp'  - Write a Windows bitmap file
     'yuv'  - Write the raw image data to a file in YUV420 format
     'rgb'  - Write the raw image data to a file in 24-bit RGB format
     'rgba' - Write the raw image data to a file in 32-bit RGBA format
     'bgr'  - Write the raw image data to a file in 24-bit BGR format
     'bgra' - Write the raw image data to a file in 32-bit BGRA format
     'raw'  - Deprecated option for raw captures; the format is taken

use_video_port 

- 默认为 False，表示使用图像端口。图像端口捕获速度慢，但是图像质量高；
如果想要快速的捕获图像，使用视频端口(True)


[Capture images continuously from the camera as an infinite iterator.](http://picamera.readthedocs.io/en/release-1.13/_modules/picamera/camera.html#PiCamera.capture_continuous)
```
capture_continuous(self, output, format=None, use_video_port=False, resize=None,
                   splitter_port=0, burst=False, bayer=False, **options)
                   
import time
import picamera
with picamera.PiCamera() as camera:
    camera.start_preview()
    try:
        for i, filename in enumerate(
            camera.capture_continuous('image{counter:02d}.jpg')):
            print(filename)
            time.sleep(2)
            if i == 5:
                break
    finally:
        camera.stop_preview()                   
```

#### OpenCV show Image
```
# -*- coding: utf-8 -*-

import time
import picamera
import numpy as np
import cv2

width, height = (320, 240)
freq = 10

with picamera.PiCamera() as camera:
    camera.resolution = (width, height)
    camera.framerate = 24
    time.sleep(freq)
    image = np.empty((width * height * 3,), dtype=np.uint8)
    camera.capture(image, 'bgr')
    image = image.reshape((width, height, 3))

    cv2.imshow("img", image)
    cv2.waitKey(0)
```


### Video

#### record video using python
```
camera.resolution = (320, 240)
camera.start_preview()
camera.start_recording('myvideo.h264')
camera.wait_recording(10)  # 录制10s
camera.stop_recording()
```

format:

    'h264'  - Write an H.264 video stream
    'mjpeg' - Write an M-JPEG video stream
    'yuv'   - Write the raw video data to a file in YUV420 format
    'rgb'   - Write the raw video data to a file in 24-bit RGB format
    'rgba'  - Write the raw video data to a file in 32-bit RGBA format
    'bgr'   - Write the raw video data to a file in 24-bit BGR format
    'bgra'  - Write the raw video data to a file in 32-bit BGRA format
