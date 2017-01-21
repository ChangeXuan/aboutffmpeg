# aboutffmpeg
##记录一下自己在弄ffmpeg时的一些操作
###部分操作在http://www.jianshu.com/p/53059be61546 和 http://blog.csdn.net/zh952016281/article/details/52683552 里边有详细说明
在使用ffmepg推流测试时，应该使用这个命令
```
ffmpeg -re -i /Users/xu/Desktop/bangbangbang.mp4-vcodec libx264 -acodec aac -f flv rtmp://localhost:1935/rtmplive/home
//其中/Users/xu/Desktop/bangbangbang.mp4为文件地址
// rtmp://localhost:1935/rtmplive/home为推流地址
```
然后使用VLC接收推流信息
查看设备的编号信息
```
ffmpeg -f avfoundation -list_devices true -i ""
```
然后命令行会显示出
```
[AVFoundation input device @ 0x7fafaed00360] AVFoundation video devices:
[AVFoundation input device @ 0x7fafaed00360] [0] Capture screen 0
```
所以当我们想推自己显示器的视频流到nginx上时，就可以这么写
```
ffmpeg -f avfoundation -i "0" -vcodec libx264 -preset ultrafast -acodec libfaac -f flv rtmp://localhost:1935/rtmplive/home
```
