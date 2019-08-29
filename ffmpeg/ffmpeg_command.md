- ffmpeg -i KTDS-820.mp4 -vf hflip -vf hflip 水平翻转
- ffmpeg -i KTDS-820.mp4 -vf vflip  -vf vflip 垂直翻转
- 将视频顺时针旋转90度
```
ffmpeg -i KTDS-820.mp4 -vf transpose=1
  transpose={0,1,2,3}
  0:逆时针旋转90°然后垂直翻转
  1:顺时针旋转90°
  2:逆时针旋转90°
  3:顺时针旋转90°然后水平翻转
```
- 顺时针旋转90度并水平翻转 ffmpeg -i out.mp4 -vf transpose=1,hflip
- 格式转换
```
ffmpeg -i KTDS-820.mkv -vcodec copy -acodec copy KTDS-820.mp4
ffmpeg -i KTDS-820.ogv -s 640x480 -b 500k -vcodec h264 -r 29.97 -acodec libfaac -ab 48k -ac 2 KTDS-820.mp4
ffmpeg -i KTDS-820-HD.mkv -s 640x360 KTDS-820.mp4
  -i 输入文件
  -r 帧率
  -s 分辨率
  -b 比特率
  -acodec 音频编码
  -vcodec 视频编码格式，推荐 h264
  -ab 音频比特率
  -ac 声道数
  ```
  - 视频分割
  ```
  ffmpeg -ss 00:01:01 -t 00:00:10 -y -i KTDS-820.mp4 -vcodec copy -acodec copy KTDS-820-cut.mp4  
  -ss 开始时间
  -t  截取时间长度
  -y  强制替换存在文件
  ```
  - 合并视频
  ```
 ffmpeg -i "KTDS-820A_FHD.mp4" -c copy  -bsf:v h264_mp4toannexb -f mpegts intermediate1.ts       
 ffmpeg -i "KTDS-820B_FHD.mp4" -c copy  -bsf:v h264_mp4toannexb -f mpegts intermediate2.ts       
 ffmpeg -i "concat:intermediate1.ts|intermediate2.ts" -c copy -bsf:a aac_adtstoasc "KTDS-820.mp4"
 ```