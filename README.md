# FFmpeg 3.2.1 - A64 platform (Cedrus HW Encoder - CMOS Camera) - Experimental

FFmpeg version 3.2.1 with built in Cedrus264 HW Encoder (POC) for the A64 platform (Pine64+ / BananaPi M64).
Build on Ubuntu Xenial 16.04. This version supports SDL2 only, if you need to render anything on display 
you better use previous version or make sure you have some sort of 2D optimization working on your board.


Dependencies
============

	sudo apt-get install libmp3lame-dev libx264-dev libpulse-dev libv4l-dev libav-dev


Source Code and Instructions
============================

https://github.com/linux-sunxi/libcedrus

https://github.com/uboborov/ffmpeg_h264_H3


How to use it
=============

- Attach your CMOS camera with S5K4EC/OV5640 enhanced driver loaded
- Clone the repo: 
  
  
	git clone https://github.com/avafinger/ffmpeg-3.2.1_cedrus264_A64_deb.git


- cd ffmpeg-3.2.1_cedrus264_A64_deb
- Install the deb package: 
  
  

	sudo dpkg -i ffmpeg-3.2.1_1.0-1_arm64.deb



- type: 
   
   

	sudo ffmpeg-3.2.1 -t 20 -f v4l2 -channel 0 -video_size 640x480 -i /dev/video0 -pix_fmt nv12 -r 30 -qp 15 -c:v cedrus264 indoor_test4_640x480_quality5_20secs.mp4

	or

	sudo ffmpeg-3.2.1 -f v4l2 -channel 0 -video_size 1024x768 -i /dev/video0 -pix_fmt nv12 -c:v cedrus264 test4_1024x768.h264


- adjust the -qp for quality [0,47]
- use -t X where X in seconds

This build works in parallel with any versions of FFMpeg without breaking any version.

Known issues / restrictions
===========================

- Encode up to 1920x1080 resolutions with low 
- Medium to low quality (640x480 to 1920x1080)
- see POC
- Triple buffer to work with low memory devices 

Log
===

- Initial commit
