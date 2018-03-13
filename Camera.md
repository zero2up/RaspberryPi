# RaspberryPi
[RaspiCam](https://www.raspberrypi.org/documentation/raspbian/applications/camera.md)

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

### Image Effect
    --sharpness,    -sh     Set image sharpness (-100 - 100)
Sets the sharpness of the image. 0 is the default.

    --contrast, -co     Set image contrast (-100 - 100)
Sets the contrast of the image. 0 is the default.

    --brightness,   -br     Set image brightness (0 - 100)
Sets the brightness of the image. 50 is the default. 0 is black, 100 is white.

    --saturation,   -sa     Set image saturation (-100 - 100)
Sets the colour saturation of the image. 0 is the default.

    --ISO,  -ISO        Set capture ISO (100 - 800)
Sets the ISO to be used for captures.

    --vstab,    -vs     Turn on video stabilisation
In video mode only, turns on video stabilisation.

    --ev,   -ev     Set EV compensation (-10 - 10)
Sets the EV compensation of the image. Default is 0.

    --exposure, -ex     Set exposure mode
Possible options are:

> auto: use automatic exposure mode

> night: select setting for night shooting

> nightpreview:

> backlight: select setting for backlit subject

> spotlight:

> sports: select setting for sports (fast shutter etc.)

> snow: select setting optimised for snowy scenery

> beach: select setting optimised for beach

> verylong: select setting for long exposures

> fixedfps: constrain fps to a fixed value

> antishake: antishake mode

> fireworks: select setting optimised for fireworks

Note that not all of these settings may be implemented, depending on camera tuning.

    --awb,  -awb        Set Automatic White Balance (AWB) mode
Modes for which colour temperature ranges (K) are available have these settings in brackets.

> off: turn off white balance calculation

> auto: automatic mode (default)

> sun: sunny mode (between 5000K and 6500K)

> cloud: cloudy mode (between 6500K and 12000K)

> shade: shade mode

> tungsten: tungsten lighting mode (between 2500K and 3500K)

> fluorescent: fluorescent lighting mode (between 2500K and 4500K)

> incandescent: incandescent lighting mode

> flash: flash mode

> horizon: horizon mode

Note that not all of these settings may be implemented, depending on camera type.

    --imxfx,    -ifx        Set image effect
Set an effect to be applied to the image:

> none: no effect (default)

> negative: invert the image colours

> solarise: solarise the image

> posterise: posterise the image

> whiteboard: whiteboard effect

> blackboard: blackboard effect

> sketch: sketch effect

> denoise: denoise the image

> emboss: emboss the image

> oilpaint: oil paint effect

> hatch: hatch sketch effect

> gpen: graphite sketch effect

> pastel: pastel effect

> watercolour: watercolour effect

> film: film grain effect

> blur: blur the image

> saturation: colour saturate the image

> colourswap: not fully implemented

> washedout: not fully implemented

> colourpoint: not fully implemented

> colourbalance: not fully implemented

> cartoon: not fully implemented

Note that not all of these settings may be available in all circumstances.

    --colfx,    -cfx        Set colour effect <U:V>
The supplied U and V parameters (range 0 - 255) are applied to the U and Y channels of the image. For example, --colfx 128:128 should result in a monochrome image.

    --metering, -mm     Set metering mode
Specify the metering mode used for the preview and capture:

> average: average the whole frame for metering

> spot: spot metering

> backlit: assume a backlit image

> matrix: matrix metering

    --rotation, -rot        Set image rotation (0 - 359)
Sets the rotation of the image in the viewfinder and resulting image. This can take any value from 0 upwards, but due to hardware constraints only 0, 90, 180, and 270 degree rotations are supported.

    --hflip,    -hf     Set horizontal flip
Flips the preview and saved image horizontally.

    --vflip,    -vf     Set vertical flip
Flips the preview and saved image vertically.

    --roi,  -roi        Set sensor region of interest
Allows the specification of the area of the sensor to be used as the source for the preview and capture. This is defined as x,y for the top-left corner, and a width and height, with all values in normalised coordinates (0.0 - 1.0). So, to set a ROI at halfway across and down the sensor, and a width and height of a quarter of the sensor, use:

> -roi 0.5,0.5,0.25,0.25

    --shutter,  -ss     Set shutter speed
Sets the shutter speed to the specified value (in microseconds). There's currently an upper limit of approximately 6000000us (6000ms, 6s), past which operation is undefined.

    --drc,  -drc        Enable/disable dynamic range compression
DRC changes the images by increasing the range of dark areas, and decreasing the brighter areas. This can improve the image in low light areas.

> off

> low

> med

> high

By default, DRC is off.

    --stats,    -st     Display image statistics
Displays the exposure, analogue and digital gains, and AWB settings used.

    --awbgains, -awbg
Sets blue and red gains (as floating point numbers) to be applied when  -awb -off is set e.g. -awbg 1.5,1.2

    --mode, -md

### raspivid
    --timed,    -td     Do timed switches between capture and pause
This options allows the video capture to be paused and restarted at particular time intervals. Two values are required: the on time and the off time.

    raspivid -o test.h264 -t 25000 -timed 2500,5000
will record for a period of 25 seconds. The recording will be over a timeframe consisting of 2500ms (2.5s) segments with 5000ms (5s) gaps, repeating over the 20s. So the entire recording will actually be only 10s long, since 4 segments of 2.5s = 10s separated by 5s gaps.

    --keypress, -k      Toggle between record and pause on Enter keypress
On each press of the Enter key, the recording will be paused or restarted. Pressing X then Enter will stop recording and close the application. Note that the timeout value will be used to signal the end of recording, but is only checked after each Enter keypress; so if the system is waiting for a keypress, even if the timeout has expired, it will still wait for the keypress before exiting.

    --segment,  -sg     Segment the stream into multiple files
Rather than creating a single file, the file is split into segments of approximately the number of milliseconds specified. In order to provide different filenames, you should add  %04d or similar at the point in the filename where you want a segment count number to appear e.g:

    --segment 3000 -o video%04d.h264
will produce video clips of approximately 3000ms (3s) long, named  video0001.h264, video0002.h264 etc. The clips should be seamless (no frame drops between clips), but the accuracy of each clip length will depend on the intraframe period, as the segments will always start on an I-frame. They will therefore always be equal or longer to the specified period.

    --wrap, -wr     Set the maximum value for segment number
When outputting segments, this is the maximum the segment number can reach before it's reset to 1, giving the ability to keep recording segments, but overwriting the oldest one. So if set to 4, in the segment example above, the files produced will be video0001.h264, video0002.h264, video0003.h264, and  video0004.h264. Once video0004.h264 is recorded, the count will reset to 1, and video0001.h264 will be overwritten.

    --start,    -sn     Set the initial segment number
When outputting segments, this is the initial segment number, giving the ability to resume a previous recording from a given segment. The default value is 1.
