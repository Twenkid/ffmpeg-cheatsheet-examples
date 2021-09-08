# ffmpeg-cheatsheet-examples

ffmpeg -i video.mp4 -i sound.aac -c:v copy -c:a copy -map 0:v:0 -map 1:a:0 new.mp4

### Hard-rendered Letterbox Preserve Aspect Ratio 
```#FFMPEG TOOLS Cheet sheet examples ...
# Compiled by Todor "Twenkid"
#13.7.2021 +
#Letterbox
#Preserve aspect raio
#Hard-render letterbox a video 

#From stackoverflow:
#Convert to 1280x720 while preserving the aspect of the video
ffmpeg -i source.mp4 -vf "scale=(iw*sar)*min(1280/(iw*sar)\,720/ih):ih*min(1280/(iw*sar)\,720/ih), pad=1280:720:(1280-iw*min(1280/iw\,720/ih))/2:(720-ih*min(1280/iw\,720/ih))/2" output2.mp4

#Test
#Convert to 720x576 - for viewing on a CRT TV without 16:9 format adjustment
ffmpeg -ss 4:20 -t 20 -i video.avi -vf "scale=(iw*sar)*min(720/(iw*sar)\,576/ih):ih*min(720/(iw*sar)\,576/ih), pad=720:576:(720-iw*min(720/iw\,576/ih))/2:(576-ih*min(720/iw\,576/ih))/2" output3.mp4

#Convert to 688x516  : e.g. 688x310 source, converted for 4:3 TV Set

ffmpeg -ss 45:30 -t 40 -i source.mp4 -vf "scale=(iw*sar)*min(688/(iw*sar)\,516/ih):ih*min(688/(iw*sar)\,516/ih), pad=688:516:(688-iw*min(688/iw\,516/ih))/2:(516-ih*min(688/iw\,516/ih))/2" -c:v libx264 -b:v 900K -tune film -c:a copy output-1M-x264-a-copy-2.mp4

# With using presets for x264: -preset medium, fast, slow, veryslow, ... Use at least similar bitrate to the source, audio is copied -c:a copy. 
# The video channel can't be copied because it's rendered. medium seems several times faster than slow, veryslow ~ 2 times than slow. 
# One sample source slow: v:1900K + a:320K, ~ 3.94 times faster than real time. Use the width of the source if possible (say 720, 688, 640...) to avoid resizing.
# Compute aspect /1.33 but sometimes may have to round, e.g. 720x540 (instead of 541.34... or x542)

ffmpeg -t 5:00 -i movie.avi -vf "scale=(iw*sar)*min(688/(iw*sar)\,516/ih):ih*min(688/(iw*sar)\,516/ih), pad=688:516:(688-iw*min(688/iw\,516/ih))/2:(516-ih*min(688/iw\,516/ih))/2" -c:v libx264 -b:v 900K -preset fast -tune film -c:a copy output-1M-x264-a-copy-2.mp4

ffmpeg -i H:\v.mkv -vf "scale=(iw*sar)*min(720/(iw*sar)\,540/ih):ih*min(720/(iw*sar)\,540/ih), pad=720:540:(720-iw*min(720/iw\,540/ih))/2:(540-ih*min(720/iw\,540/ih))/2" -c:v libx264 -b:v 1200K -preset slow -tune film -c:a copy F:\v.mkv


#
(def: medium)
-preset slow 
-preset slow ```
```
### Change Audio ```map 1:a:0``` ... 
```
ffmpeg -i Usmivkata-na-smurtta_Intro_x264_15M_192K_1280x720_13-2-2021.mp4 -i sound.aac -c:v copy -c:a copy -map 0:v:0 -map 1:a:0 new.mp4
ffmpeg -i video.mp4 -i sound.aac -c:v copy -c:a copy -map 0:v:0 -map 1:a:0 new.mp4
```
