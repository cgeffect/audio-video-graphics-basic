

ffplay
播放视频
```
ffplay -video_size 720x720 -pixel_format rgba 资源路径
```
播放pcm
```
ffplay -ar 48000 -ac 2 -f f32le pcm路径
ffplay -ar 48000 -ac 2 -f s16le pcm路径
```
播放图片 只显示r分量
```
ffplay -vf extractplanes=r in.png
```

只显示y分量

```
ffplay -video_size 512x512 -pixel_format yuv420p -vf extractplanes=y in.yuv
```

提取H264
```
ffmpeg -i source.flv -vcodec libx264 -an -f h264 _yuv420p_1280x720.h264
```
提取MPEG2

```
ffmpeg -i source.flv -vcodec mpeg2video -an -f mpeg2video 768x320_10s.mpeg2
```
// pixel_format 像素格式
// video_size 尺寸
// framerate帧率

播放yuv
```
ffplay -pixel_format yuv420p -video_size 720x720 -framerate 25 in.yuv
ffplay -video_size 1120x1120 -pixel_format yuv420p in.yuv
```
播放rgb
```
ffplay -pixel_format rgb24 -video_size 720x720 -framerate 30 in.rgb
ffplay -video_size 1120x1120 -pixel_format rgba in.rgba
```


提取h265
```
ffmpeg -i h265.mkv -vcodec hevc output.h265
``` 
用ffmpeg命令将264裸码流封装成mp4
```
ffmpeg -i input.mp4 -c:v copy -bsf:v h264_mp4toannexb -an out.h264
```
播放H264视频
```
ffplay -stats -f h264 out.h264
```
     
提取音频aac
```
ffmpeg -i input.mp4 -acodec copy -vn  output.aac
```
提取音频mp3
```
ffmpeg -i input.mp4 -f mp3 -vn apple.mp3
```
提取音频pcm
```
ffplay -ar 48000 -channels 2 -f f32le -i output.pcm
```

视频倒放，无音频
```
ffmpeg -i input.mp4 -filter_complex [0:v]reverse[v] -map [v] -preset superfast reversed.mp4
```
视频倒放，音频不变
```
ffmpeg -i input.mp4 -vf reverse reversed.mp4
```   
音频倒放，视频不变
```
ffmpeg -i input.mp4 -map 0 -c:v copy -af "areverse" reversed_audio.mp4
``` 
音视频同时倒放
```
ffmpeg -i input.mp4 -vf reverse -af areverse -preset superfast reversed.mp4
```

视频裁剪
```
ffmpeg  -i ./input.mp4 -vcodec copy -acodec copy -ss 00:00:00 -to 00:05:00 ./cutout1.mp4 -y
ffmpeg  -i ./input.mp4 -vcodec copy -acodec copy -ss 00:05:00 -to 00:10:00 ./cutout2.mp4 -y
ffmpeg  -i ./input.mp4 -vcodec copy -acodec copy -ss 00:10:00 -to 00:14:50./cutout3.mp4 -y
```