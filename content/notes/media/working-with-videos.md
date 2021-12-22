---
title: Working with Videos
type: docs
---

## Analyze Video  

[mediainfo](https://mediaarea.net/en/MediaInfo) - Use `-f` flag to get maximum info

[FFMPEG](https://www.ffmpeg.org/) has a probe tool that is great for extracting technical metadata from a variety of video files - `ffprobe '$URL'`

## FFMPEG Video Tricks

Overlay information on a video (you provide start timecode, framrate):  
`ffmpeg -i $INPUT_VIDEO -vf "drawtext=fontsize=15:fontfile=/Library/Fonts/Arial\ Bold\.ttf:timecode='01\:00\:00\:00':rate=24:text='TCR\:':fontsize=52:fontcolor='white':boxcolor=0x000000AA:box=1:x=1:y=1, drawtext=fontsize=15:fontfile=/Library/Fonts/Arial\ Bold\.ttf:text='Frames\:%{n}':fontsize=52:fontcolor='white':boxcolor=0x000000AA:box=1:x=1:y=60, drawtext=fontsize=15:fontfile=/Library/Fonts/Arial\ Bold\.ttf:text='Seconds\:%{pts}':fontsize=52:fontcolor='white':boxcolor=0x000000AA:box=1:x=1:y=120,
drawtext=fontsize=15:fontfile=/Library/Fonts/Arial\ Bold\.ttf:text='Framerate\:23.976':fontsize=52:fontcolor='white':boxcolor=0x000000AA:box=1:x=1:y=180" $OUTPUT_VIDEO`

Create a blank video:  
`ffmpeg -t 600 -s 640x480 -f rawvideo -pix_fmt rgb24 -r 23.976 -i /dev/zero 10min_23976.mp4`